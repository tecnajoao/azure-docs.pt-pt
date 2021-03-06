---
title: Configurar e gerir políticas de replicação para a recuperação de desastre do VMware para o Azure com o Azure Site Recovery | Documentos da Microsoft
description: Descreve como configurar as definições de replicação para a recuperação de desastre do VMware para o Azure com o Azure Site Recovery.
author: sujayt
manager: rochakm
ms.service: site-recovery
ms.topic: conceptual
ms.date: 04/08/2019
ms.author: sutalasi
ms.openlocfilehash: b60d8a8fb9b9300a6914ad33b2f760fb5adde3b4
ms.sourcegitcommit: 62d3a040280e83946d1a9548f352da83ef852085
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59278229"
---
# <a name="configure-and-manage-replication-policies-for-vmware-disaster-recovery-to-azure"></a>Configurar e gerir políticas de replicação para a recuperação de desastre do VMware para o Azure
Este artigo descreve como configurar uma política de replicação quando estiver a replicar VMs de VMware para o Azure, utilizando [do Azure Site Recovery](site-recovery-overview.md).

## <a name="create-a-policy"></a>Criar uma política

1. Selecione **Gerir** > **Infraestrutura do Site Recovery**.
2. Na **para o VMware e máquinas físicas**, selecione **políticas de replicação**.
3. Clique em **+ política de replicação**e especifique o nome da política.
4. No **limiar RPO**, especifique o limite RPO. Os alertas são gerados quando a replicação contínua excede este limite.
5. Na **retenção do ponto de recuperação**, especifique (em horas) a duração da janela de retenção para cada ponto de recuperação. As máquinas protegidas podem ser recuperadas para qualquer ponto numa janela de retenção. É suportada até 24 horas de retenção para máquinas replicadas para o armazenamento premium. É suportada até 72 horas para o armazenamento standard.
6. Na **frequência de instantâneos consistentes com a aplicação**, selecione na lista pendente com que frequência (em horas) devem ser criados os pontos de recuperação que contêm instantâneos consistentes com aplicações. Se pretender desativar a geração de pontos de consistência de aplicações, escolha "Desligado", valor na lista pendente.
7. Clique em **OK**. A política deve ser criada em 30 segundos a 60 segundos.

Quando cria uma política de replicação, uma política de replicação de reativação pós-falha correspondente é criada automaticamente, com o sufixo "reativação pós-falha". Depois de criar a política, pode editá-lo, selecionando-> **editar definições de**.

## <a name="associate-a-configuration-server"></a>Associar um servidor de configuração

Associe a política de replicação com o seu servidor de configuração no local.

1. Clique em **associar**e selecione o servidor de configuração.

    ![Associar o servidor de configuração](./media/vmware-azure-set-up-replication/associate1.png)
2. Clique em **OK**. O servidor de configuração deve ser associado em um ou dois minutos.

    ![Associação do servidor de configuração](./media/vmware-azure-set-up-replication/associate2.png)

## <a name="edit-a-policy"></a>Editar uma política

1. Selecione **gerenciar** > **infraestrutura do Site Recovery** > **políticas de replicação**.
2. Selecione a política de replicação que pretende modificar.
3. Clique em **editar as definições de**e atualize os campos de frequência do RPO/recuperação do limiar ponto retenção horas/Instantâneo consistente da aplicação, conforme necessário.
4. Se pretender desativar a geração de pontos de consistência de aplicações, escolha "Desligado", valor na lista pendente do campo **frequência de instantâneos consistentes com a aplicação**.
5. Clique em **Guardar**. A política deve ser atualizada em 30 a 60 segundos.

## <a name="disassociate-or-delete-a-replication-policy"></a>Desassociação ou eliminar uma política de replicação

1. Escolha a política de replicação.
    a. Para desassociar a política a partir do servidor de configuração, certifique-se de que não existem máquinas replicadas estão a utilizar a política. Em seguida, clique em **desassocie**.
    b. Para eliminar a política, certifique-se de que não está associado com um servidor de configuração. Em seguida, clique em **eliminar**. Deverá demorar 30 a 60 segundos para eliminar.
2. Clique em **OK**.
