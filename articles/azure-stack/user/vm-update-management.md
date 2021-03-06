---
title: VM atualização e gestão com o Azure Stack | Documentos da Microsoft
description: Saiba como utilizar o Azure Monitor para VMs, gestão de atualizações, controlo de alterações e inventário de soluções na automatização do Azure para gerir o Windows e VMs do Linux que estão implementadas no Azure Stack.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2019
ms.author: jeffgilb
ms.reviewer: rtiberiu
ms.lastreviewed: 03/20/2019
ms.openlocfilehash: cb8258c0f837d0e70ba87a26246f055b0efe5c00
ms.sourcegitcommit: 90dcc3d427af1264d6ac2b9bde6cdad364ceefcc
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/21/2019
ms.locfileid: "58316155"
---
# <a name="azure-stack-vm-update-and-management"></a>Atualização de VM de pilha e gestão do Azure
Pode utilizar os seguintes recursos de solução de automatização do Azure para gerir o Windows e VMs do Linux que são implementadas através do Azure Stack:

- **[Gestão de atualizações](https://docs.microsoft.com/azure/automation/automation-update-management)**. Com a solução de gestão de atualizações, pode rapidamente avaliar o estado das atualizações disponíveis em todos os computadores agente e gerenciar o processo de instalação de atualizações necessárias para estas VMs de Linux e Windows.

- **[Controlo de alterações](https://docs.microsoft.com/azure/automation/automation-change-tracking)**. Alterações ao software instalado, serviços do Windows, registro do Windows e arquivos e os daemons Linux nos servidores monitorizados são enviadas para o serviço do Azure Monitor na cloud para processamento. Lógica é aplicada para os dados recebidos e o serviço em nuvem regista os dados. Ao utilizar as informações no dashboard do controlo de alterações, pode ver facilmente as alterações efetuadas na sua infraestrutura de servidor.

- **[Inventário](https://docs.microsoft.com/azure/automation/automation-vm-inventory)**. O controle para uma máquina virtual do Azure Stack de inventário fornece uma interface de utilizador baseada no browser para definir e configurar a recolha de inventário.

- **[Monitor do Azure para VMs](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)**. Monitor do Azure para VMs monitoriza as suas máquinas de virtuais do Azure e o Azure Stack (VM) e conjuntos de dimensionamento de máquinas virtuais em escala. Ele analisa o desempenho e estado de funcionamento das suas VMs de Linux e Windows e monitoriza os seus processos e as dependências de outros recursos e processos externos. 

> [!IMPORTANT]
> Estas soluções são as mesmas que as utilizadas para gerir VMs do Azure. O Azure e VMs do Azure Stack são geridas da mesma forma, a partir da mesma interface, com as mesmas ferramentas. As VMs de pilha do Azure também são cobradas as mesmas que as VMs do Azure ao utilizar as soluções de gestão de atualizações, controlo de alterações, inventário e máquinas de virtuais de Monitor do Azure com o Azure Stack.

## <a name="prerequisites"></a>Pré-requisitos
Vários pré-requisitos têm de ser cumpridos antes de utilizar estas funcionalidades para atualizar e gerir VMs do Azure Stack. Estes incluem os passos que devem ser levados no portal do Azure, bem como o portal de administração do Azure Stack.

### <a name="in-the-azure-portal"></a>No portal do Azure
Para utilizar o Azure Monitor para VMs, inventário, controlo de alterações e recursos de automatização do Azure de gestão de atualização para as VMs do Azure Stack, primeiro tem de ativar estas soluções no Azure.

> [!TIP]
> Se já tiver estas funcionalidades ativadas para VMs do Azure, pode utilizar as credenciais de área de trabalho LogAnalytics já existentes. Se já tiver um LogAnalytics WorkspaceID e a chave primária que pretende utilizar, avançar diretamente para [a próxima seção](./vm-update-management.md#in-the-azure-stack-administration-portal). Caso contrário, continue nesta secção para criar uma nova conta de área de trabalho LogAnalytics e automação.

É o primeiro passo para estas soluções de ativação [criar uma área de trabalho LogAnalytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace) na sua subscrição do Azure. Uma área de trabalho do Log Analytics é um ambiente de registos do Azure Monitor exclusivo com seu próprio repositório de dados, origens de dados e soluções. Depois de criar uma área de trabalho, tenha em atenção o WorkspaceID e a chave. Para ver estas informações, aceda ao painel de área de trabalho, clique em **definições avançadas**e reveja a **ID de área de trabalho** e **chave primária** valores. 

Em seguida, deve [criar uma conta de automatização](https://docs.microsoft.com/azure/automation/automation-create-standalone-account). Uma conta de automatização é um contentor para os seus recursos de automatização do Azure. Ele fornece uma forma de separar os seus ambientes ou de organizar melhor seus fluxos de trabalho de automatização e os recursos. Depois de criada a conta de automatização, necessárias para ativar o inventário, o controle de alterações e atualizar as funcionalidades de gestão. Para tal, siga estes passos para ativar cada funcionalidade:

1. No portal do Azure, vá para a conta de automatização que pretende utilizar.

2. Selecione a solução para ativar (qualquer um dos **inventário**, **controlo de alterações**, ou **gestão de atualizações**).

3. Utilize o **selecionar área de trabalho...**  na lista pendente para selecionar a área de trabalho do Log Analytics a utilizar.

4. Certifique-se de que todas as restantes informações estão corretas e, em seguida, clique em **ativar** para ativar a solução.

5. Repita os passos 2 a 4 para permitir que todos os três soluções. 

   [![](media/vm-update-management/1-sm.PNG "Ativar funcionalidades de conta de automatização")](media/vm-update-management/1-lg.PNG#lightbox)

### <a name="enable-azure-monitor-for-vms"></a>Ativar o Azure Monitor para VMs

Monitor do Azure para VMs monitoriza máquinas de virtuais do Azure (VM) e conjuntos de dimensionamento de máquinas virtuais em escala. Ele analisa o desempenho e estado de funcionamento das suas VMs de Linux e Windows e monitoriza os seus processos e as dependências de outros recursos e processos externos.

Como uma solução, o Azure Monitor para VMs inclui suporte para as dependências de desempenho e a aplicação de monitorização para as VMs que estão alojados no local ou em outro fornecedor de cloud. Três principais recursos fornecem informações detalhadas:

1. Componentes lógicos de VMs do Azure que executam o Windows e Linux: São medidas em relação a critérios de estado de funcionamento pré-configuradas, e eles alertá-lo quando for cumprida a condição avaliada. 

2. Gráficos de desempenho populares predefinidos: Apresentar as métricas de desempenho do núcleo do sistema de operativo da VM de convidado.

3. Mapa de dependência: Mostra os componentes interconectados com a VM a partir de vários grupos de recursos e subscrições.

Depois de criar a área de trabalho do Log Analytics, terá de ativar os contadores de desempenho na área de trabalho para a coleção em Linux e VMs do Windows, bem como instalar e ativar a solução ServiceMap e InfrastructureInsights na sua área de trabalho. O processo é descrito no [implementar o Azure Monitor para VMs](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#deploy-azure-monitor-for-vms) guia.

### <a name="in-the-azure-stack-administration-portal"></a>No Portal de administração do Azure Stack
Depois de ativar as soluções de automatização do Azure no portal do Azure, em seguida tem de iniciar sessão no portal de administração do Azure Stack como um administrador da nuvem e transfira o **do Azure Monitor, atualização e gestão de configuração** e o **Do azure Monitor, atualização e gestão de configuração para Linux** itens do marketplace extensão do Azure Stack. 

   ![O Azure Monitor, atualização e configuração de gestão extensão item do marketplace](media/vm-update-management/2.PNG) 

Para ativar o Azure Monitor para a solução mapa de VMs e obtenha informações sobre as dependências de rede, precisará também baixar o **agente do Azure Monitor de dependência**:

   ![Azure Monitor Dependency Agent](media/vm-update-management/2-dependency.PNG) 

## <a name="enable-update-management-for-azure-stack-virtual-machines"></a>Ativar a gestão de atualizações para máquinas de virtuais do Azure Stack
Siga estes passos para ativar a gestão de atualizações para as VMs do Azure Stack.

1. Inicie sessão no portal de utilizador do Azure Stack.

2. No portal do Azure Stack utilizador-, aceda ao painel de extensões de máquinas virtuais para o qual pretende ativar estas soluções, clique em **+ adicionar**, selecione a **atualização do Azure e o gerenciamento de configuração** extensão e clique em **criar**:

   [![](media/vm-update-management/3-sm.PNG "Painel de extensão VM")](media/vm-update-management/3-lg.PNG#lightbox)

3. Fornecer o criado anteriormente WorkspaceID e a chave primária para ligar o agente com a área de trabalho LogAnalytics e clique em **OK** para implementar a extensão.

   [![](media/vm-update-management/4-sm.PNG "Fornecer o WorkspaceID e a chave")](media/vm-update-management/4-lg.PNG#lightbox) 

4. Conforme descrito no [documentação de gestão de atualização de automatização](https://docs.microsoft.com/azure/automation/automation-update-management), tem de ativar a solução de gestão de atualizações para cada VM que pretende gerir. Para ativar a solução para todas as VMs de geração de relatórios para a área de trabalho, selecione **gestão de atualizações**, clique em **gerir máquinas**e, em seguida, selecione o **ativar em todas as máquinas disponíveis e futuras,** opção.

   [![](media/vm-update-management/5-sm.PNG "Fornecer o WorkspaceID e a chave")](media/vm-update-management/5-lg.PNG#lightbox) 

   > [!TIP]
   > Repita este passo para ativar cada solução para as VMs de pilha esse relatório para a área de trabalho do Azure. 
  
Depois de ativar a extensão de atualização do Azure e o gerenciamento de configuração, é feita uma análise duas vezes por dia para cada VM gerida. A API é chamada a cada 15 minutos para consultar a hora da última atualização determinar se o estado foi alterado. Se o estado mudou, é iniciada uma análise de conformidade.

Depois das VMs são analisadas, serão apresentados na conta de automatização do Azure na solução de gestão de atualizações: 

   [![](media/vm-update-management/6-sm.PNG "Fornecer o WorkspaceID e a chave")](media/vm-update-management/6-lg.PNG#lightbox) 

> [!IMPORTANT]
> Pode demorar entre 30 minutos e 6 horas para o dashboard apresentar os dados atualizados dos computadores gerenciados.

As VMs do Azure Stack agora podem ser incluídas em implementações de atualização agendada, juntamente com as VMs do Azure.

## <a name="enable-azure-monitor-for-vms-running-on-azure-stack"></a>Ativar o Azure Monitor para VMs em execução no Azure Stack
Assim que a VM tem o **do Azure Monitor, atualização e gestão de configuração** e o **agente de dependência de Monitor do Azure** extensões instaladas, ele começa a reportar dados no [Azure Monitor para VMs](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) solução. 

> [!TIP]
> O **agente do Azure Monitor de dependência** extensão não requer quaisquer parâmetros. O Azure Monitor para agente de dependência de mapa de VMs não transmitir todos os dados em si, e ele não requer alterações às firewalls ou portas. Os dados de mapa sempre são transmitidos pelo agente do Log Analytics para o serviço Azure Monitor, diretamente ou através da [Gateway de OMS](https://docs.microsoft.com/azure/azure-monitor/platform/gateway) se as políticas de segurança de TI não permitir que os computadores na rede para ligar à internet.

Monitor do Azure para VMs inclui um conjunto de gráficos de desempenho que visam vários indicadores chave de desempenho (KPIs) para ajudar a determinar a forma como uma máquina virtual está a efetuar. Os gráficos mostram a utilização de recursos durante um período de tempo para que possa identificar estrangulamentos de anomalias, ou mudar para um ponto de vista listagem cada máquina para ver a utilização de recursos com base na métrica selecionada. Embora haja vários elementos a serem considerados ao lidar com desempenho, relacionados com o Azure Monitor para a indicadores de desempenho de importantes do sistema operativo de monitores de VMs para processador, memória, adaptador de rede e utilização do disco. Complementa a funcionalidade de monitorização de estado de funcionamento de desempenho e ajuda a expor problemas que indiquem uma falha de componente do sistema possíveis, ajuste de suporte e a otimização para alcançar a eficiência ou suportar o planeamento de capacidade.

   ![Guia de desempenho de Monitor do Azure](https://docs.microsoft.com/azure/azure-monitor/insights/media/vminsights-performance/vminsights-performance-aggview-01.png)

Ver os componentes da aplicação detetada no Windows e Linux máquinas de virtuais em execução no Azure Stack pode ser observado de duas formas com o Azure Monitor para as VMs, de uma máquina virtual diretamente ou através de grupos de VMs do Azure Monitor.
O [utilizar o Azure Monitor para VMs (pré-visualização) mapa para compreender os componentes da aplicação](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-maps) artigo o ajudará a compreender a experiência de entre as duas perspetivas e como utilizar a funcionalidade de mapa.

   ![Guia de desempenho de Monitor do Azure](https://docs.microsoft.com/azure/azure-monitor/insights/media/vminsights-maps/map-multivm-azure-monitor-01.png)


## <a name="enable-update-management-using-a-resource-manager-template"></a>Ativar a gestão de atualização utilizando um modelo do Resource Manager
Se tiver um grande número de VMs do Azure Stack, pode utilizar [este modelo do Azure Resource Manager](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/MicrosoftMonitoringAgent-ext-win) implantar mais facilmente a solução em VMs. O modelo implementa a extensão do Microsoft Monitoring Agent para uma VM de pilha do Azure existente e adiciona-o para uma área de trabalho do Azure LogAnalytics existente.
 
## <a name="next-steps"></a>Passos Seguintes
[Otimizar o desempenho da VM do SQL Server](azure-stack-sql-server-vm-considerations.md)




