---
title: Tutorial - criar um gateway de aplicação com uma firewall de aplicações web - portal do Azure | Documentos da Microsoft
description: Saiba como criar um gateway de aplicação com uma firewall de aplicações web com o portal do Azure.
services: application-gateway
author: vhorne
manager: jpconnock
editor: tysonn
tags: azure-resource-manager
ms.service: application-gateway
ms.topic: article
ms.workload: infrastructure-services
ms.date: 03/25/2019
ms.author: victorh
ms.openlocfilehash: 1284ddec4cd9cea3ea53c20d437550405dd614d9
ms.sourcegitcommit: 9f4eb5a3758f8a1a6a58c33c2806fa2986f702cb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/03/2019
ms.locfileid: "58905873"
---
# <a name="create-an-application-gateway-with-a-web-application-firewall-using-the-azure-portal"></a>Criar um gateway de aplicação com uma firewall de aplicações web no portal do Azure

> [!div class="op_single_selector"]
>
> - [Portal do Azure](application-gateway-web-application-firewall-portal.md)
> - [PowerShell](tutorial-restrict-web-traffic-powershell.md)
> - [CLI do Azure](tutorial-restrict-web-traffic-cli.md)
>
> 

Este tutorial mostra-lhe como utilizar o portal do Azure para criar uma [gateway de aplicação](application-gateway-introduction.md) com um [firewall de aplicações web](application-gateway-web-application-firewall-overview.md) (WAF). A WAF utiliza regras de [OWASP](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) para proteger a sua aplicação. Estas regras incluem a proteção contra ataques, tais como injeção SQL, ataques de scripts entre sites e assunção de controlo de sessão sem autorização. Depois de criar o gateway de aplicação, teste-lo para se certificar de que está a funcionar corretamente. Com o Gateway de aplicação do Azure, direcionar o tráfego da web de aplicação a recursos específicos, a atribuição de serviços de escuta a portas, criação de regras e adicionar recursos a um agrupamento de back-end. Para simplificar, este artigo utiliza uma configuração simples com um IP público de front-end, um serviço de escuta básico para alojar um site único neste gateway de aplicação, duas máquinas virtuais utilizadas para o conjunto de back-end e uma regra de encaminhamento de pedido básico.

Neste artigo, vai aprender a:

> [!div class="checklist"]
> * Criar um gateway de aplicação com a WAF ativada
> * Criar as máquinas virtuais utilizadas como servidores de back-end
> * Criar uma conta de armazenamento e configurar o diagnóstico

![Exemplo de firewall de aplicações Web](./media/application-gateway-web-application-firewall-portal/scenario-waf.png)

[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]

## <a name="sign-in-to-azure"></a>Iniciar sessão no Azure

Inicie sessão no portal do Azure em [https://portal.azure.com](https://portal.azure.com)

## <a name="create-an-application-gateway"></a>Criar um gateway de aplicação

Para o Azure comunicar entre os recursos que criar, ele precisa de uma rede virtual. Pode criar uma nova rede virtual ou utilize um já existente. Neste exemplo, iremos criar uma nova rede virtual. Pode criar uma rede virtual ao mesmo tempo que cria o gateway de aplicação. Instâncias de Gateway de aplicação são criadas em sub-redes separadas. Criar duas sub-redes neste exemplo: um para o gateway de aplicação e outro para os servidores de back-end.

Selecione **criar um recurso** no menu da esquerda do portal do Azure. O **New** é apresentada a janela.

Selecione **Networking** e, em seguida, selecione **Gateway de aplicação** no **em destaque** lista.

### <a name="basics-page"></a>Página de noções básicas

1. Sobre o **Noções básicas** página, introduza estes valores para as seguintes definições do gateway de aplicação:
   - **Nome**: Introduza *myAppGateway* para o nome do gateway de aplicação.
   - **Grupo de recursos**: Selecione **myResourceGroupAG** para o grupo de recursos. Se não existir, selecione **criar novo** para criá-lo.
   - Selecione *WAF* para o escalão do gateway de aplicação.![ Criar o novo gateway de aplicação](./media/application-gateway-web-application-firewall-portal/application-gateway-create.png)

Aceite os valores predefinidos para as outras definições e, em seguida, clique em **OK**.

### <a name="settings-page"></a>Página de definições

1. Sobre o **configurações** página, em **configuração de sub-rede**, selecione **escolher uma rede virtual**. <br>
2. Sobre o **escolher rede virtual** página, selecione **criar nova**e, em seguida, introduza valores para as seguintes definições de rede virtual:
   - **Nome**: Introduza *myVNet* para o nome da rede virtual.
   - **Espaço de endereços**: Introduza *10.0.0.0/16* para o espaço de endereços de rede virtual.
   - **Nome da sub-rede**: Introduza *myAGSubnet* para o nome da sub-rede.<br>A sub-rede do gateway de aplicação pode conter apenas os gateways de aplicação. Não existem outros recursos são permitidos.
   - **Intervalo de endereços da sub-rede**: Introduza *10.0.0.0/24* para o intervalo de endereços da sub-rede.![ Criar rede virtual](./media/application-gateway-web-application-firewall-portal/application-gateway-vnet.png)
3. Clique em **OK** para criar a rede virtual e a sub-rede.
4. Escolha o **configuração do IP de front-end**. Sob **a configuração de IP de front-end**, certifique-se **tipo de endereço IP** está definida como **pública**. Sob **endereço IP público**, certifique-se **criar nova** está selecionada. <br>Pode configurar o IP de front-end, seja pública ou privada, de acordo com o seu caso de utilização. Neste exemplo, vamos escolher um IP público de front-end. 
5. Introduza *myAGPublicIPAddress* para o nome do endereço IP público. 
6. Aceite os valores predefinidos para as outras definições e, em seguida, selecione **OK**.<br>Vamos escolher valores predefinidos neste artigo para simplificar, mas pode configurar os valores personalizados para as outras definições consoante o seu caso de utilização 

### <a name="summary-page"></a>Página de resumo

Reveja as definições na **resumo** página e, em seguida, selecione **OK** para criar a rede virtual, o endereço IP público e o gateway de aplicação. Pode demorar vários minutos para o Azure criar o gateway de aplicação. Aguarde até a conclusão da implementação com êxito antes de passar para a secção seguinte.

## <a name="add-backend-pool"></a>Adicionar conjunto back-end

O conjunto de back-end é utilizado para encaminhar pedidos para os servidores de back-end que irão ser que atendeu à solicitação. Conjuntos de back-end podem ser compostos de NICs, conjuntos de dimensionamento de máquinas virtuais, IPs públicos, nomes de IPs interno, de domínio completamente qualificado (FQDN) e back-ends de multi-inquilino, como o serviço de aplicações do Azure. Precisa adicionar seus destinos de back-end para um conjunto de back-end.

Neste exemplo, utilizaremos as máquinas virtuais como o back-end de destino. Pode utilizar máquinas virtuais existentes ou criar novos. Neste exemplo, iremos criar duas máquinas virtuais que utiliza o Azure como servidores de back-end para o gateway de aplicação. Para tal, iremos:

1. Criar uma nova sub-rede *myBackendSubnet*, na qual as novas VMs vão ser criadas. 
2. Criar VMS novas 2, a *myVM* e *myVM2*, para ser utilizada como servidores de back-end.
3. Instale o IIS nas máquinas virtuais para verificar se o gateway de aplicação foi criado com êxito.
4. Adicione os servidores de back-end para o conjunto de back-end.

### <a name="add-a-subnet"></a>Adicionar uma sub-rede

Adicione uma sub-rede para a rede virtual que criou ao seguir estes passos:

1. Selecione **todos os recursos** no menu da esquerda do portal do Azure, introduza *myVNet* na caixa de pesquisa e, em seguida, selecione **myVNet** resultados da pesquisa.

2. Selecione **sub-redes** no menu à esquerda e em seguida, selecione **+ sub-rede**. 

   ![Criar sub-rede](./media/application-gateway-create-gateway-portal/application-gateway-subnet.png)

3. Do **adicionar sub-rede** página, introduza *myBackendSubnet* para o **nome** da sub-rede e, em seguida, selecione **OK**.

### <a name="create-a-virtual-machine"></a>Criar uma máquina virtual

1. No portal do Azure, selecione **criar um recurso**. O **New** é apresentada a janela.
2. Selecione **computação** e, em seguida, selecione **do Windows Server 2016 Datacenter** no **em destaque** lista. O **criar uma máquina virtual** é apresentada a página.<br>Gateway de aplicação pode encaminhar o tráfego para qualquer tipo de máquina virtual utilizada no seu conjunto de back-end. Neste exemplo, vai utilizar um Windows Server 2016 Datacenter.
3. Introduza estes valores no **Noções básicas** separador para as seguintes definições de máquina virtual:
   - **Grupo de recursos**: Selecione **myResourceGroupAG** para o nome do grupo de recursos.
   - **Nome da máquina virtual**: Introduza *myVM* para o nome da máquina virtual.
   - **Nome de utilizador**: Introduza *azureuser* para o nome de utilizador de administrador.
   - **palavra-passe**: Introduza *Azure123456!* a palavra-passe de administrador.
4. Aceite as outras predefinições e, em seguida, selecione **seguinte: Discos**.  
5. Aceite o **discos** separador predefinições e, em seguida, selecione **seguinte: Funcionamento em rede**.
6. No **Networking** separador, certifique-se de que **myVNet** está selecionada para o **rede Virtual** e a **sub-rede** está definido como  **myBackendSubnet**. Aceite as outras predefinições e, em seguida, selecione **seguinte: Management**.<br>Gateway de aplicação pode comunicar com instâncias de fora da rede virtual que está a ser, mas é necessário garantir que existe conectividade IP. 
7. Sobre o **gestão** separador, defina **diagnósticos de arranque** para **desativar**. Aceite as outras predefinições e, em seguida, selecione **rever + criar**.
8. Sobre o **rever + criar** separador, reveja as definições, corrija os erros de validação e, em seguida, selecione **criar**.
9. Aguarde até a criação da máquina virtual concluir antes de continuar.

### <a name="install-iis-for-testing"></a>Instalar o IIS para fins de teste

Neste exemplo, podemos são instalar o IIS nas máquinas virtuais apenas para efeitos de verificar o que Azure foi criado o gateway de aplicação com êxito. 

1. Open [do Azure PowerShell](https://docs.microsoft.com/azure/cloud-shell/quickstart-powershell). Para tal, selecione **Cloud Shell** na barra de navegação superior do portal do Azure e, em seguida, selecione **PowerShell** na lista pendente. 

   ![Instalar uma extensão personalizada](./media/application-gateway-create-gateway-portal/application-gateway-extension.png)

2. Execute o comando seguinte para instalar o IIS na máquina virtual: 

   ```azurepowershell-interactive
   Set-AzVMExtension `
     -ResourceGroupName myResourceGroupAG `
     -ExtensionName IIS `
     -VMName myVM `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
   ```

3. Crie uma segunda máquina virtual e instalar o IIS, utilizando os passos que concluiu anteriormente. Uso *myVM2* para o nome da máquina virtual e para o **VMName** definição do **Set-AzVMExtension** cmdlet.

### <a name="add-backend-servers-to-backend-pool"></a>Adicionar servidores de back-end ao agrupamento de back-end

1. Selecione **todos os recursos**e, em seguida, selecione **myAppGateway**.

2. Selecione **conjuntos de back-end** no menu à esquerda. Azure criado automaticamente um conjunto predefinido, **appGatewayBackendPool**, ao criar o gateway de aplicação. 

3. Selecione **appGatewayBackendPool**.

4. Sob **destinos**, selecione **Máquina Virtual** na lista pendente.

5. Sob **máquina VIRTUAL** e **INTERFACES de rede**, selecione o **myVM** e **myVM2** máquinas virtuais e de suas redes associadas interfaces de listas pendentes.

   ![Adicionar servidores back-end](./media/application-gateway-create-gateway-portal/application-gateway-backend.png)

6. Selecione **Guardar**.

## <a name="create-a-storage-account-and-configure-diagnostics"></a>Criar uma conta de armazenamento e configurar o diagnóstico

### <a name="create-a-storage-account"></a>Criar uma conta de armazenamento

Neste tutorial, o gateway de aplicação utiliza uma conta de armazenamento para armazenar dados para efeitos de deteção e prevenção. Também pode utilizar os registos do Azure Monitor ou o Hub de eventos para gravar dados.

1. Clique em **New** encontrado no canto superior esquerdo do portal do Azure.
2. Selecione **Armazenamento** e selecione **Conta de Armazenamento - blob, ficheiro, tabela, fila**.
3. Introduza o nome da conta de armazenamento, selecione **utilizar existente** para o grupo de recursos e, em seguida, selecione **myResourceGroupAG**. Neste exemplo, é o nome da conta de armazenamento *myagstore1*. Aceite os valores predefinidos para as outras definições e, em seguida, clique em **criar**.

### <a name="configure-diagnostics"></a>Configurar o diagnóstico

Configure o diagnóstico para registar dados nos registos ApplicationGatewayAccessLog, ApplicationGatewayPerformanceLog e ApplicationGatewayFirewallLog.

1. No menu da esquerda, clique em **todos os recursos**e, em seguida, selecione *myAppGateway*.
2. Em monitorização, clique em **registos de diagnóstico**.
3. Clique em **Adicionar definição de diagnóstico**.
4. Introduza *myDiagnosticsSettings* como o nome para as definições de diagnóstico.
5. Selecione **arquivo para uma conta de armazenamento**e, em seguida, clique em **configurar** para selecionar o *myagstore1* conta de armazenamento que criou anteriormente.
6. Selecione os registos do gateway de aplicação para recolher e manter.
7. Clique em **Guardar**.

    ![Configurar o diagnóstico](./media/application-gateway-web-application-firewall-portal/application-gateway-diagnostics.png)

## <a name="test-the-application-gateway"></a>Testar o gateway de aplicação

Embora o IIS não é necessário para criar o gateway de aplicação, a instalou neste início rápido para verificar se o Azure criada com êxito o gateway de aplicação. Utilize o IIS para testar o gateway de aplicação:

1. Encontrar o endereço IP público para o gateway de aplicação na respetiva **descrição geral** página.![ Registar o endereço IP público do application gateway](./media/application-gateway-create-gateway-portal/application-gateway-record-ag-address.png)em alternativa, pode selecionar **todos os recursos**, introduza *myAGPublicIPAddress* na pesquisa caixa e, em seguida, selecione-o na pesquisa resultados. Azure mostra o endereço IP público na **descrição geral** página.
2. Copie o endereço IP público e cole-o na barra de endereço do browser.
3. Verifique a resposta. Uma resposta válida verifica se o gateway de aplicação foi criado com êxito e é capaz de ligar com êxito com o back-end.![Testar o gateway de aplicação](./media/application-gateway-create-gateway-portal/application-gateway-iistest.png)

## <a name="clean-up-resources"></a>Limpar recursos

Quando já não precisar dos recursos que criou com o gateway de aplicação, remova o grupo de recursos. Ao remover o grupo de recursos, também remover o gateway de aplicação e todos os respetivos recursos relacionados. 

Para remover o grupo de recursos:

1. No menu da esquerda do portal do Azure, selecione **grupos de recursos**.
2. Sobre o **grupos de recursos** página, procure **myResourceGroupAG** na lista, em seguida, selecioná-lo.
3. Sobre o **página do grupo de recursos**, selecione **eliminar grupo de recursos**.
4. Introduza *myResourceGroupAG* para **tipo o nome de grupo de recursos** e, em seguida, selecione **eliminar**

## <a name="next-steps"></a>Passos Seguintes

Neste artigo, aprendeu como:

> [!div class="checklist"]
> * Criar um gateway de aplicação com a WAF ativada
> * Criar as máquinas virtuais utilizadas como servidores de back-end
> * Criar uma conta de armazenamento e configurar o diagnóstico

Para saber mais sobre os gateways de aplicação e os recursos associados, avance para os artigos de procedimentos.
