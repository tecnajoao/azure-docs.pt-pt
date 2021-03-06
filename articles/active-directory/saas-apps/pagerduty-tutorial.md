---
title: 'Tutorial: Integração do Active Directory do Azure com PagerDuty | Documentos da Microsoft'
description: Saiba como configurar o início de sessão único entre o Azure Active Directory e o PagerDuty.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 03/14/2019
ms.author: jeedes
ms.openlocfilehash: ded5854c5e669ab1982641169f13a9cb400d5d6d
ms.sourcegitcommit: 62d3a040280e83946d1a9548f352da83ef852085
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59270120"
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a>Tutorial: Integração do Active Directory do Azure com PagerDuty

Neste tutorial, saiba como integrar o PagerDuty no Azure Active Directory (Azure AD).
Integrar o PagerDuty no Azure AD fornece as seguintes vantagens:

* Pode controlar no Azure AD que tenha acesso ao PagerDuty.
* Pode permitir que os utilizadores ser automaticamente sessão iniciada para PagerDuty (Single Sign-On) com as suas contas do Azure AD.
* Pode gerir as suas contas num local central – portal do Azure.

Se quiser saber mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [o que é o acesso a aplicações e início de sessão único com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis).
Se não tiver uma subscrição do Azure, [crie uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com PagerDuty, terá dos seguintes itens:

* Uma subscrição do Azure AD. Se não tiver um ambiente do Azure AD, pode obter a versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/)
* PagerDuty logon único habilitado subscrição

## <a name="scenario-description"></a>Descrição do cenário

Neste tutorial, configure e teste do Azure AD início de sessão único num ambiente de teste.

* Suporta o PagerDuty **SP** iniciada SSO

## <a name="adding-pagerduty-from-the-gallery"></a>Adicionar PagerDuty a partir da Galeria

Para configurar a integração do PagerDuty no Azure AD, terá de adicionar PagerDuty a partir da Galeria à sua lista de aplicações de SaaS geridas.

**Para adicionar PagerDuty a partir da galeria, execute os seguintes passos:**

1. Na **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo, clique em **Azure Active Directory** ícone.

    ![O botão do Azure Active Directory](common/select-azuread.png)

2. Navegue para **aplicações empresariais** e, em seguida, selecione a **todos os aplicativos** opção.

    ![O painel de aplicações empresariais](common/enterprise-applications.png)

3. Para adicionar nova aplicação, clique em **nova aplicação** botão na parte superior de caixa de diálogo.

    ![O novo botão de aplicativo](common/add-new-app.png)

4. Na caixa de pesquisa, escreva **PagerDuty**, selecione **PagerDuty** no painel de resultados, em seguida, clique em **Add** botão para adicionar a aplicação.

     ![PagerDuty na lista de resultados](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD início de sessão único

Nesta secção, configure e teste do Azure AD início de sessão único com PagerDuty com base num utilizador de teste **Eduarda Almeida**.
Para o início de sessão único funcionar, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionado no PagerDuty deve ser estabelecido.

Para configurar e testar o Azure AD início de sessão único com PagerDuty, tem de concluir os seguintes blocos de construção:

1. **[Configurar o Azure AD início de sessão único](#configure-azure-ad-single-sign-on)**  - para permitir que os utilizadores utilizar esta funcionalidade.
2. **[Configurar o PagerDuty Single Sign-On](#configure-pagerduty-single-sign-on)**  - para configurar as definições de início de sessão único no lado do aplicativo.
3. **[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  - para testar o Azure AD início de sessão único com Eduarda Almeida.
4. **[Atribua o utilizador de teste do Azure AD](#assign-the-azure-ad-test-user)**  - para ativar a Eduarda Almeida utilizar o Azure AD início de sessão único.
5. **[Criar utilizador de teste do PagerDuty](#create-pagerduty-test-user)**  - para ter um equivalente da Eduarda Almeida no PagerDuty que está ligado à representação de utilizador do Azure AD.
6. **[Testar início de sessão único](#test-single-sign-on)**  - para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o Azure AD início de sessão único

Nesta secção, vai ativar o Azure AD início de sessão único no portal do Azure.

Para configurar o Azure AD início de sessão único com PagerDuty, execute os seguintes passos:

1. Na [portal do Azure](https://portal.azure.com/), na **PagerDuty** página de integração de aplicações, selecione **início de sessão único**.

    ![Configurar a ligação de início de sessão única](common/select-sso.png)

2. Sobre o **selecionar um método de início de sessão único** caixa de diálogo, selecione **SAML/WS-Fed** modo para ativar o início de sessão único.

    ![Único início de sessão em modo de seleção](common/select-saml-option.png)

3. Sobre o **definir a segurança de início de sessão único com o SAML** página, clique em **editar** ícone para abrir **configuração básica de SAML** caixa de diálogo.

    ![Editar a configuração SAML do básico](common/edit-urls.png)

4. Sobre o **configuração básica de SAML** secção, execute os seguintes passos:

    ![PagerDuty domínio e URLs únicas início de sessão em informações](common/sp-identifier.png)

    a. Na **iniciar sessão no URL** caixa de texto, escreva um URL com o seguinte padrão: `https://<tenant-name>.pagerduty.com`

    b. Na **identificador (ID de entidade)** caixa de texto, escreva um URL com o seguinte padrão: `https://<tenant-name>.pagerduty.com`

    > [!NOTE]
    > Estes valores não são reais. Atualize estes valores com o início de sessão real URL e o identificador. Contacte [equipa de suporte de cliente do PagerDuty](https://www.pagerduty.com/support/) obter esses valores. Também pode consultar os padrões mostrados a **configuração básica de SAML** secção no portal do Azure.

5. No **definido no início de sessão único com o SAML** página, além do **certificado de assinatura SAML** secção, clique em **transferir** para transferir o **certificado (Base64)** entre as opções de determinado de acordo com seus requisitos e guarde-o no seu computador.

    ![O link de download de certificado](common/certificatebase64.png)

6. Sobre o **configurar PagerDuty** secção, copie os URLs apropriados de acordo com seus requisitos.

    ![URLs de configuração de cópia](common/copy-configuration-urls.png)

    a. URL de início de sessão

    b. Identificador do Azure AD

    c. URL de fim de sessão

### <a name="configure-pagerduty-single-sign-on"></a>Configurar o PagerDuty Single Sign-On

1. Numa janela do browser web diferente, inicie sessão no site da sua empresa Pagerduty como um administrador.

2. No menu na parte superior, clique em **definições de conta**.

    ![Definições da conta](./media/pagerduty-tutorial/ic778535.png "definições da conta")

3. Clique em **início de sessão único**.

    ![Início de sessão único](./media/pagerduty-tutorial/ic778536.png "início de sessão único")

4. Sobre o **ativar o início de sessão único (SSO)** página, execute os seguintes passos:

    ![Ativar o início de sessão único](./media/pagerduty-tutorial/ic778537.png "ativar início de sessão único")

    a. Abra o seu certificado codificado de base 64 transferido a partir do portal do Azure no bloco de notas, copie o conteúdo do mesmo para a área de transferência e, em seguida, cole-os para o **certificado X.509** caixa de texto
  
    b. Na **URL de início de sessão** caixa de texto, colar **URL de início de sessão** que copiou do portal do Azure.
  
    c. Na **URL de fim de sessão** caixa de texto, colar **URL de fim de sessão** que copiou do portal do Azure.

    d. Selecione **início de sessão de nome de utilizador/palavra-passe de permitir**.

    e. Selecione **comparação de contexto de autenticação exigir EXATA** caixa de verificação.

    f. Clique em **guardar alterações**.

### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD 

O objetivo desta secção é criar um utilizador de teste no portal do Azure chamado Eduarda Almeida.

1. No portal do Azure, no painel esquerdo, selecione **do Azure Active Directory**, selecione **utilizadores**e, em seguida, selecione **todos os utilizadores**.

    !["Os utilizadores e grupos" e os links de "Todos os utilizadores"](common/users.png)

2. Selecione **novo utilizador** na parte superior do ecrã.

    ![Novo utilizador botão](common/new-user.png)

3. Nas propriedades do utilizador, execute os seguintes passos.

    ![A caixa de diálogo de utilizador](common/user-properties.png)

    a. Na **Name** campo introduza **BrittaSimon**.
  
    b. Na **nome de utilizador** tipo de campo **brittasimon@yourcompanydomain.extension**  
    Por exemplo, BrittaSimon@contoso.com

    c. Selecione **palavra-passe de Show** caixa de verificação e, em seguida, anote o valor que é apresentado na caixa de palavra-passe.

    d. Clique em **Criar**.

### <a name="assign-the-azure-ad-test-user"></a>Atribua o utilizador de teste do Azure AD

Nesta secção, vai ativar Eduarda Almeida utilizar do Azure-início de sessão único, concedendo acesso para o PagerDuty.

1. No portal do Azure, selecione **aplicações empresariais**, selecione **todos os aplicativos**, em seguida, selecione **PagerDuty**.

    ![Painel de aplicações empresariais](common/enterprise-applications.png)

2. Na lista de aplicações, selecione **PagerDuty**.

    ![A ligação do PagerDuty na lista de aplicações](common/all-applications.png)

3. No menu à esquerda, selecione **utilizadores e grupos**.

    ![A ligação "Utilizadores e grupos"](common/users-groups-blade.png)

4. Clique nas **adicionar utilizador** botão, em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar atribuição](common/add-assign-user.png)

5. Na **utilizadores e grupos** caixa de diálogo select **Eduarda Almeida** na lista de utilizadores, em seguida, clique o **selecionar** na parte inferior do ecrã.

6. Se está esperando a qualquer valor de função a asserção de SAML, em seguida, no **selecionar função** caixa de diálogo selecione a função adequada para o utilizador na lista, em seguida, clique o **selecione** na parte inferior do ecrã.

7. Na **adicionar atribuição** clique da caixa de diálogo a **atribuir** botão.

### <a name="create-pagerduty-test-user"></a>Criar utilizador de teste do PagerDuty

Para ativar a utilizadores do Azure AD iniciar sessão no PagerDuty, tem de ser aprovisionados no PagerDuty.  
No caso do PagerDuty, aprovisionamento é uma tarefa manual.

>[!NOTE]
>Pode utilizar quaisquer outras Pagerduty utilizador conta criação ferramentas ou APIs fornecidas pelo Pagerduty para aprovisionar o Azure Active Directory contas de utilizador.

**Para Aprovisionar uma conta de utilizador, execute os seguintes passos:**

1. Inicie sessão no seu **Pagerduty** inquilino.

2. No menu na parte superior, clique em **utilizadores**.

3. Clique em **adicionar utilizadores**.
   
    ![Adicionar utilizadores](./media/pagerduty-tutorial/ic778539.png "adicionar utilizadores")

4.  Sobre o **convidar sua equipe** caixa de diálogo, execute os seguintes passos:
   
    ![Convidar sua equipe](./media/pagerduty-tutorial/ic778540.png "convidar sua equipe")

    a. Tipo de **primeiro e último nome** do utilizador, como **Eduarda Almeida**. 
   
    b. Introduza **E-Mail** como o endereço do utilizador **brittasimon\@contoso.com**.
   
    c. Clique em **Add**e, em seguida, clique em **enviar convites**.
   
    >[!NOTE]
    >Todos os utilizadores adicionados irão receber um convite para criar uma conta do PagerDuty.

### <a name="test-single-sign-on"></a>Testar início de sessão único 

Nesta secção, vai testar a configuração do Azure AD única início de sessão com o painel de acesso.

Quando clica no mosaico do PagerDuty no painel de acesso, deve ser automaticamente sessão iniciada no PagerDuty para o qual configura o SSO. Para obter mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).

## <a name="additional-resources"></a>Recursos Adicionais

- [Lista de tutoriais sobre como integrar aplicações SaaS com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [O que é o acesso a aplicações e início de sessão único com o Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [O que é o acesso condicional no Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

