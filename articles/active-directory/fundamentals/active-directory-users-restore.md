---
title: Restaure ou remover permanentemente um utilizador recentemente eliminado - Azure Active Directory | Documentos da Microsoft
description: Como ver os utilizadores restaurável, restaurar um utilizador eliminado ou eliminar permanentemente um utilizador com o Azure Active Directory.
services: active-directory
author: eross-msft
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.subservice: fundamentals
ms.topic: conceptual
ms.date: 04/01/2018
ms.author: lizross
ms.reviewer: jeffsta
ms.custom: it-pro, seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d69bd931f2f8c72fd1e6fc79c16662ea367617d6
ms.sourcegitcommit: 3341598aebf02bf45a2393c06b136f8627c2a7b8
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/01/2019
ms.locfileid: "58802019"
---
# <a name="restore-or-remove-a-recently-deleted-user-using-azure-active-directory"></a>Restaure ou remover um utilizador eliminado recentemente com o Azure Active Directory
Depois de eliminar um utilizador, a conta permanece num estado suspenso durante 30 dias. Durante esse período de 30 dias, pode ser restaurada a conta de utilizador, juntamente com as respetivas propriedades. Depois de passa essa janela de 30 dias, o utilizador é automaticamente e permanentemente, eliminado.

Pode ver os seus utilizadores restaurável, restaurar um utilizador eliminado ou eliminar permanentemente um utilizador com o Azure Active Directory (Azure AD) no portal do Azure.

>[!Important]
>Nem nem o suporte técnico da Microsoft, pode restaurar um utilizador eliminado permanentemente.

## <a name="required-permissions"></a>Permissões obrigatórias
Tem de ter uma das seguintes funções para restaurar e eliminar permanentemente os utilizadores.

- Administrador global

- Parceiro de Suporte de Escalão 1

- Parceiro de Suporte de Escalão 2

- Administrador de utilizadores

## <a name="view-your-restorable-users"></a>Ver os seus utilizadores restaurável
Pode ver todos os utilizadores que foram eliminados há menos de 30 dias. Estes utilizadores podem ser restaurados.

### <a name="to-view-your-restorable-users"></a>Para ver os seus utilizadores restaurável
1. Inicie sessão para o [portal do Azure](https://portal.azure.com/) com uma conta de Administrador Global para a organização.

2. Selecione **do Azure Active Directory**, selecione **utilizadores**e, em seguida, selecione **utilizadores eliminados**.

    Reveja a lista de utilizadores que estão disponíveis para restaurar.

    ![Utilizadores - página de utilizadores eliminados, com os utilizadores que ainda podem ser restaurados](media/active-directory-users-restore/users-deleted-users-view-restorable.png)

## <a name="restore-a-recently-deleted-user"></a>Restaurar um utilizador eliminado recentemente

Quando uma conta de utilizador é eliminada da organização, a conta estiver num estado suspenso e todas as informações da organização relacionados são preservadas. Quando restaurar um utilizador, estas informações de organização também são restauradas.

> [!Note]
> Assim que um utilizador é restaurado, as licenças foram atribuídas ao utilizador no momento da eliminação são também restauradas, mesmo que não há nenhum postos de trabalho disponíveis para essas licenças. Se, em seguida, está a consumir mais licenças mais do que tiver adquirido, sua organização pode ser temporariamente fora de conformidade para a utilização de licenças.

### <a name="to-restore-a-user"></a>Para restaurar um utilizador
1. Sobre o **utilizadores - utilizadores eliminados** página, procure e selecione um dos utilizadores disponíveis. Por exemplo, _Mary Parker_.

2. Selecione **utilizador de restauro**.

    ![Utilizadores - página de utilizadores eliminados, com a opção de utilizador de restauro realçada](media/active-directory-users-restore/users-deleted-users-restore-user.png)

## <a name="permanently-delete-a-user"></a>Eliminar permanentemente um utilizador
Pode eliminar permanentemente um utilizador da sua organização sem esperar que os 30 dias para eliminação automática. Não é possível restaurar um utilizador permanentemente eliminado pelo administrador de outro, nem por suporte técnico da Microsoft.

>[!Note]
>Se eliminar permanentemente um utilizador por engano, terá de criar um novo utilizador e inserir manualmente todas as informações anteriores. Para obter mais informações sobre como criar um novo utilizador, consulte [adicionar ou eliminar utilizadores](add-users-azure-active-directory.md).

### <a name="to-permanently-delete-a-user"></a>Eliminar permanentemente um utilizador

1. Sobre o **utilizadores - utilizadores eliminados** página, procure e selecione um dos utilizadores disponíveis. Por exemplo, _Rae Huff_.

2. Selecione **eliminar permanentemente**.

    ![Utilizadores - página de utilizadores eliminados, com a opção de utilizador de restauro realçada](media/active-directory-users-restore/users-deleted-users-permanent-delete-user.png)

## <a name="next-steps"></a>Passos Seguintes
Depois de ter restaurado ou eliminado os seus utilizadores, pode efetuar os seguintes processos de basic:

- [Adicionar ou eliminar utilizadores](add-users-azure-active-directory.md)

- [Atribuir funções a utilizadores](active-directory-users-assign-role-azure-portal.md)

- [Adicionar ou alterar as informações de perfil](active-directory-users-profile-azure-portal.md)

- [Adicionar utilizadores convidados de outra organização](../b2b/what-is-b2b.md)

Para obter mais informações sobre outras tarefas de gestão de usuário disponíveis [documentação de gestão de utilizador do Azure AD](../users-groups-roles/index.yml).
