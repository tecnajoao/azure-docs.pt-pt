---
title: Preparar servidores VMware no local para a recuperação após desastre de VMs de VMware para o Azure | Microsoft Docs
description: Saiba como preparar servidores VMware no local para a recuperação após desastre para o Azure com o serviço Azure Site Recovery.
services: site-recovery
author: rayne-wiselman
manager: carmonm
ms.service: site-recovery
ms.topic: tutorial
ms.date: 04/08/2019
ms.author: raynew
ms.custom: MVC
ms.openlocfilehash: 1095a80ba05aa3e0ae6dfcd526db7ffd18fb9d4d
ms.sourcegitcommit: 43b85f28abcacf30c59ae64725eecaa3b7eb561a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/09/2019
ms.locfileid: "59359363"
---
# <a name="prepare-on-premises-vmware-servers-for-disaster-recovery-to-azure"></a>Preparar servidores VMware no local para a recuperação após desastre para o Azure

Este artigo descreve como preparar servidores VMware no local para a recuperação após desastre para o Azure com o [do Azure Site Recovery](site-recovery-overview.md) serviços. 

Este artigo é o segundo tutorial de uma série que lhe mostra como configurar a recuperação após desastre no Azure para VMs do VMware no local. No primeiro tutorial, [configurámos os componentes do Azure](tutorial-prepare-azure.md) necessários para a recuperação após desastre do VMware.


Neste artigo, vai aprender a:

> [!div class="checklist"]
> * Prepare uma conta no vCenter server ou vSphere ESXi no anfitrião, para automatizar a deteção de VMS.
> * Prepare uma conta para a instalação automática do serviço de mobilidade em VMs de VMware.
> * Reveja o servidor VMware e os requisitos de VM e suporte.
> * Prepare-se a ligação para as VMs do Azure após a ativação pós-falha.

> [!NOTE]
> Tutoriais mostram-lhe o caminho de implantação mais simples para um cenário. Utilizam opções predefinidas sempre que possível e não mostram todas as definições e caminhos possíveis. Para obter instruções detalhadas, consulte o artigo na seção como a do Site Recovery sumário.

## <a name="before-you-start"></a>Antes de começar

Certifique-se de que já preparou a Azure conforme descrito no [primeiro tutorial nesta série](tutorial-prepare-azure.md).

## <a name="prepare-an-account-for-automatic-discovery"></a>Preparar uma conta para a deteção automática

O Site Recovery precisa de ter acesso a servidores VMware para:

- Detetar automaticamente VMs. É necessária, pelo menos, uma conta só de leitura.
- Orquestrar a replicação, a ativação pós-falha e a reativação pós-falha. Precisa de uma conta com capacidade para executar operações como criar e remover discos, e ligar VMs.

Crie a conta da seguinte forma:

1. Para utilizar uma conta dedicada, crie uma função ao nível do vCenter. Dê um nome à função, como **Azure_Site_Recovery**.
2. Atribua à função as permissões resumidas na tabela abaixo.
3. Crie um utilizador no servidor vCenter ou no anfitrião vSphere. Atribua a função ao utilizador.

### <a name="vmware-account-permissions"></a>Permissões de conta de VMware

**Tarefa** | **/ Permissões de função** | **Detalhes**
--- | --- | ---
**Deteção de VMS** | Pelo menos um utilizador só de leitura<br/><br/> Objeto Data Center –> Propagar ao Objeto Subordinado, função=Só de Leitura | Utilizador atribuído ao nível do datacenter, com acesso a todos os objetos no datacenter.<br/><br/> Para restringir o acesso, atribua a função **Sem acesso** com **Propagar ao objeto subordinado** aos objetos subordinados (anfitriões vSphere, arquivos de dados, VMs e redes).
**Total de replicação, ativação pós-falha e reativação pós-falha** |  Criar uma função (Azure_Site_Recovery) com as permissões necessárias e, em seguida, atribuir a função a um grupo ou utilizador de VMware<br/><br/> Objeto Data Center –> Propagar ao Objeto Subordinado, função=Azure_Site_Recovery<br/><br/> Arquivo de Dados -> Alocar espaço, navegar no arquivo de dados, operações de ficheiro de baixo nível, remover ficheiros, atualizar ficheiros de máquinas virtuais<br/><br/> Rede -> Atribuição de rede<br/><br/> Recursos -> Atribuir VM a agrupamento de recursos, migrar VMs desligadas, migrar VMs ligadas<br/><br/> Tarefas -> Criar tarefa, atualizar tarefa<br/><br/> Máquina virtual -> Configuração<br/><br/> Máquina virtual -> Interagir -> responder a perguntas, ligação de dispositivos, configurar suportes de dados em CD, configurar suportes de dados em disquete, desligar, ligar, instalação de ferramentas de VMware<br/><br/> Máquina virtual -> Inventário -> Criar, registar, anular o registo<br/><br/> Máquina virtual -> Aprovisionamento -> Permitir transferência de máquinas virtuais, permitir carregamento de ficheiros de máquinas virtuais<br/><br/> Máquina virtual -> Instantâneos -> Remover instantâneos | Utilizador atribuído ao nível do datacenter, com acesso a todos os objetos no datacenter.<br/><br/> Para restringir o acesso, atribua a função **Sem acesso** com **Propagar ao objeto subordinado** aos objetos subordinados (anfitriões vSphere, arquivos de dados, VMs e redes).

## <a name="prepare-an-account-for-mobility-service-installation"></a>Preparar uma conta para a instalação do serviço de Mobilidade

O Serviço de mobilidade tem de ser instalado em cada computador que queira replicar. O Site Recovery pode efetuar uma instalação push deste serviço quando ativar a replicação para um computador, pode instalá-lo manualmente ou através de ferramentas de instalação.

- Neste tutorial, vamos instalar o Serviço de mobilidade com a instalação push.
- Para a instalação push, tem de preparar uma conta que o Site Recovery pode utilizar para aceder à VM. Esta conta é especificada quando configurar a recuperação após desastre na consola do Azure.

Prepare a conta da seguinte forma:

Prepare um domínio ou uma conta local com permissões para instalar na VM.

- **VMs do Windows**: Para instalar em VMs do Windows se não estiver a utilizar uma conta de domínio, desative o controlo de acesso de utilizador remoto na máquina local. Para fazer isto, no registo > **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, adicione a entrada DWORD **LocalAccountTokenFilterPolicy**, com um valor de 1.
- **VMs do Linux**: Para instalar em VMs do Linux, prepare uma conta raiz no servidor Linux de origem.


## <a name="check-vmware-requirements"></a>Verificar os requisitos de VMware

Certifique-se de que os servidores do VMware e as VM cumprem os requisitos.

1. [Verifique](vmware-physical-azure-support-matrix.md#on-premises-virtualization-servers) os requisitos do servidor do VMware.
2. Para as VMs do Linux, [verifique](vmware-physical-azure-support-matrix.md#linux-file-systemsguest-storage) o sistema de ficheiros e os requisitos de armazenamento. 
3. Verifique a [rede](vmware-physical-azure-support-matrix.md#network) local e o suporte de [armazenamento](vmware-physical-azure-support-matrix.md#storage). 
4. Verifique o que é suportado para [redes do Azure](vmware-physical-azure-support-matrix.md#azure-vm-network-after-failover), [armazenamento](vmware-physical-azure-support-matrix.md#azure-storage), e [computação](vmware-physical-azure-support-matrix.md#azure-compute), após a ativação pós-falha.
5. As suas VM no local que replica para o Azure devem estar em conformidade com os [requisitos de VM do Azure](vmware-physical-azure-support-matrix.md#azure-vm-requirements).
6. Em máquinas virtuais do Linux, nome do dispositivo ou nome do ponto de montagem deve ser exclusivo. Certifique-se de que não existem dois pontos de montagem/dispositivos têm os mesmos nomes. Tenha em atenção que o nome não diferencia maiúsculas de minúsculas. Por exemplo, dois dispositivos de nomenclatura para a mesma VM como _device1_ e _Device1_ não é permitida.


## <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Preparar a ligação para VMs do Azure após a ativação pós-falha

Após a ativação pós-falha, pode querer ligar às VMs do Azure a partir da sua rede no local.

Para ligar às VMs do Windows via RDP após a ativação pós-falha, faça o seguinte:

- **Acesso à Internet**. Antes da ativação pós-falha, ative o protocolo RDP na VM local. Confirme que são adicionadas regras de TCP e UDP ao perfil **Público** e que o protocolo RDP é permitido em **Firewall do Windows** > **Aplicações Permitidas** para todos os perfis.
- **Acesso de rede de VPNs**:
    - Antes da ativação pós-falha, ative o protocolo RDP no computador local.
    - O protocolo RDP deve estar permitido em **Firewall do Windows** -> **Aplicações e funcionalidades permitidas** para redes de **Domínio e Privadas**.
    - Verifique se a política de SAN do sistema operativo está definida como **OnlineAll**. [Saiba mais](https://support.microsoft.com/kb/3031135).
- Não devem haver atualizações do Windows pendentes na VM quando aciona uma ativação pós-falha. Se existirem, não será possível iniciar sessão na máquina virtual enquanto a atualização for concluída.
- Na VM do Azure do Windows após a ativação pós-falha, consulte o **Diagnóstico de arranque**  para ver uma captura de ecrã da VM. Se não conseguir ligar-se, verifique se a VM está em execução e reveja estas [sugestões de resolução de problemas](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

Para ligar às VMs do Linux via SSH após a ativação pós-falha, faça o seguinte:

- No computador local, antes da ativação pós-falha, verifique se o serviço Secure Shell está definido para iniciar automaticamente no arranque do sistema.
- Verifique se as regras de firewall permitem uma ligação SSH.
- Na VM do Azure após a ativação pós-falha, permita ligações de entrada na porta SSH para as regras de grupo de segurança de rede na VM com ativação pós-falha e para a sub-rede do Azure à qual está ligada.
- [Adicione um endereço IP público](site-recovery-monitoring-and-troubleshooting.md) para a VM.
- Pode consultar o **Diagnóstico de arranque** para ver uma captura de ecrã da VM.


## <a name="failback-requirements"></a>Requisitos de reativação pós-falha
Se planear para a reativação pós-falha seu site no local, existem diversas [pré-requisitos para a reativação pós-falha](vmware-azure-reprotect.md##before-you-begin). Pode preparar estes agora, mas não precisa. Pode preparar depois de efetuar a ativação pós-falha para o Azure.



## <a name="next-steps"></a>Passos Seguintes

Configure a recuperação de desastres. Se estiver a replicar várias VMs, planear a capacidade.
> [!div class="nextstepaction"]
> [Configurar a recuperação após desastre para o Azure das VMs VMware](vmware-azure-tutorial.md)
> [efetuar o planeamento de capacidade](site-recovery-deployment-planner.md).
