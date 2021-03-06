---
title: 'Tutorial: Integração do Active Directory do Azure com TimeOffManager | Documentos da Microsoft'
description: Saiba como configurar o início de sessão único entre o Azure Active Directory e TimeOffManager.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 03/27/2019
ms.author: jeedes
ms.openlocfilehash: a297c9db22d81ee3c32be4732198ba25b8f5a8f8
ms.sourcegitcommit: 62d3a040280e83946d1a9548f352da83ef852085
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59280201"
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a>Tutorial: Integração do Active Directory do Azure com TimeOffManager

Neste tutorial, saiba como integrar TimeOffManager com o Azure Active Directory (Azure AD).
Integrar TimeOffManager no Azure AD fornece as seguintes vantagens:

* Pode controlar no Azure AD que tenha acesso ao TimeOffManager.
* Pode permitir que os utilizadores ser automaticamente sessão iniciada para TimeOffManager (Single Sign-On) com as suas contas do Azure AD.
* Pode gerir as suas contas num local central – portal do Azure.

Se quiser saber mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [o que é o acesso a aplicações e início de sessão único com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis).
Se não tiver uma subscrição do Azure, [crie uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com TimeOffManager, terá dos seguintes itens:

* Uma subscrição do Azure AD. Se não tiver um ambiente do Azure AD, pode obter a versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/)
* TimeOffManager logon único habilitado subscrição

## <a name="scenario-description"></a>Descrição do cenário

Neste tutorial, configure e teste do Azure AD início de sessão único num ambiente de teste.

* Suporta TimeOffManager **IDP** iniciada SSO

* Suporta TimeOffManager **Just In Time** aprovisionamento de utilizadores

## <a name="adding-timeoffmanager-from-the-gallery"></a>Adicionando TimeOffManager da Galeria

Para configurar a integração do TimeOffManager com o Azure AD, terá de adicionar TimeOffManager a partir da Galeria à sua lista de aplicações de SaaS geridas.

**Para adicionar TimeOffManager a partir da galeria, execute os seguintes passos:**

1. Na **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo, clique em **Azure Active Directory** ícone.

    ![O botão do Azure Active Directory](common/select-azuread.png)

2. Navegue para **aplicações empresariais** e, em seguida, selecione a **todos os aplicativos** opção.

    ![O painel de aplicações empresariais](common/enterprise-applications.png)

3. Para adicionar nova aplicação, clique em **nova aplicação** botão na parte superior de caixa de diálogo.

    ![O novo botão de aplicativo](common/add-new-app.png)

4. Na caixa de pesquisa, escreva **TimeOffManager**, selecione **TimeOffManager** no painel de resultados, em seguida, clique em **Add** botão para adicionar a aplicação.

     ![TimeOffManager na lista de resultados](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD início de sessão único

Nesta secção, configure e teste do Azure AD início de sessão único com TimeOffManager com base num utilizador de teste **Eduarda Almeida**.
Para o início de sessão único funcionar, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionado no TimeOffManager deve ser estabelecido.

Para configurar e testar o Azure AD início de sessão único com TimeOffManager, tem de concluir os seguintes blocos de construção:

1. **[Configurar o Azure AD início de sessão único](#configure-azure-ad-single-sign-on)**  - para permitir que os utilizadores utilizar esta funcionalidade.
2. **[Configurar TimeOffManager Single Sign-On](#configure-timeoffmanager-single-sign-on)**  - para configurar as definições de início de sessão único no lado do aplicativo.
3. **[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  - para testar o Azure AD início de sessão único com Eduarda Almeida.
4. **[Atribua o utilizador de teste do Azure AD](#assign-the-azure-ad-test-user)**  - para ativar a Eduarda Almeida utilizar o Azure AD início de sessão único.
5. **[Criar utilizador de teste TimeOffManager](#create-timeoffmanager-test-user)**  - para ter um equivalente da Eduarda Almeida na TimeOffManager que está ligado à representação de utilizador do Azure AD.
6. **[Testar início de sessão único](#test-single-sign-on)**  - para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o Azure AD início de sessão único

Nesta secção, vai ativar o Azure AD início de sessão único no portal do Azure.

Para configurar o Azure AD início de sessão único com TimeOffManager, execute os seguintes passos:

1. Na [portal do Azure](https://portal.azure.com/), na **TimeOffManager** página de integração de aplicações, selecione **início de sessão único**.

    ![Configurar a ligação de início de sessão única](common/select-sso.png)

2. Sobre o **selecionar um método de início de sessão único** caixa de diálogo, selecione **SAML/WS-Fed** modo para ativar o início de sessão único.

    ![Único início de sessão em modo de seleção](common/select-saml-option.png)

3. Sobre o **definir a segurança de início de sessão único com o SAML** página, clique em **editar** ícone para abrir **configuração básica de SAML** caixa de diálogo.

    ![Editar a configuração SAML do básico](common/edit-urls.png)

4. Sobre o **configuração básica de SAML** secção, execute os seguintes passos:

    ![TimeOffManager domínio e URLs únicas início de sessão em informações](common/idp-reply.png)

    Na **URL de resposta** caixa de texto, escreva um URL com o seguinte padrão:  `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`

    > [!NOTE]
    > Este valor não é real. Atualize este valor com o URL de resposta real. Pode obter este valor a partir **início de sessão único na página de definições** qual será explicado mais tarde no tutorial ou contacte [equipa de suporte de TimeOffManager](https://www.purelyhr.com/contact-us). Também pode consultar os padrões mostrados a **configuração básica de SAML** secção no portal do Azure.

5. Aplicação de TimeOffManager espera que as asserções SAML num formato específico, o que requer a adição de mapeamentos de atributos personalizado à sua configuração de atributos de token SAML. Captura de ecrã seguinte mostra a lista de atributos predefinidos. Clique em **edite** ícone para abrir **atributos do utilizador** caixa de diálogo.

    ![image](common/edit-attribute.png)

6. Além dos acima, o aplicativo TimeOffManager espera mais alguns atributos a serem passados na resposta SAML. No **afirmações de utilizador** secção sobre o **atributos de utilizador** caixa de diálogo, execute os seguintes passos para adicionar o atributo de token de SAML conforme mostrado na tabela a seguir: 

    | Name | Atributo de origem|
    | --- | --- |
    | FirstName |User.givenname |
    | Apelido |User.surname |
    | Email |User.mail |

    a. Clique em **Adicionar nova afirmação** para abrir o **afirmações de utilizador de gerir** caixa de diálogo.

    ![image](common/new-save-attribute.png)

    ![image](common/new-attribute-details.png)

    b. Na **nome** caixa de texto, escreva o nome de atributo apresentado para essa linha.

    c. Deixe o **espaço de nomes** em branco.

    d. Selecione a origem de dado **atributo**.

    e. Partir do **atributo de origem** lista, digite o valor de atributo apresentado para essa linha.

    f. Clique em **Ok**

    g. Clique em **Guardar**.

7. No **definido no início de sessão único com o SAML** página, além do **certificado de assinatura SAML** secção, clique em **transferir** para transferir o **certificado (Base64)** entre as opções de determinado de acordo com seus requisitos e guarde-o no seu computador.

    ![O link de download de certificado](common/certificatebase64.png)

8. Sobre o **configurar TimeOffManager** secção, copie os URLs apropriados de acordo com seus requisitos.

    ![URLs de configuração de cópia](common/copy-configuration-urls.png)

    a. URL de início de sessão

    b. Identificador do Azure AD

    c. URL de fim de sessão

### <a name="configure-timeoffmanager-single-sign-on"></a>Configurar TimeOffManager Single Sign-On

1. Numa janela do browser web diferente, inicie sessão no site da sua empresa TimeOffManager como administrador.

2. Aceda a **conta \> opções de conta \> único configurações de logon**.
   
    ![Único configurações de logon](./media/timeoffmanager-tutorial/ic795917.png "único configurações de logon")

3. Na **definições de início de sessão único** secção, execute os seguintes passos:
   
    ![Único configurações de logon](./media/timeoffmanager-tutorial/ic795918.png "único configurações de logon")
   
    a. Abra o certificado com codificação base 64 no bloco de notas, copie o conteúdo do mesmo para a área de transferência e, em seguida, cole o certificado completo para **certificado X.509** caixa de texto.
   
    b. Na **Idp emissor** caixa de texto, cole o valor de **do Azure AD identificador** que copiou do portal do Azure.
   
    c. Na **URL de ponto final de IdP** caixa de texto, cole o valor de **URL de início de sessão** que copiou do portal do Azure.
   
    d. Como **impor SAML**, selecione **não**.
   
    e. Como **Auto-criar usuários**, selecione **Sim**.
   
    f. Na **URL de fim de sessão** caixa de texto, cole o valor de **URL de fim de sessão** que copiou do portal do Azure.
   
    g. Clique em **guardar alterações**.

4. Na **definições de início de sessão único** página, copie o valor da **URL do serviço de consumidor de asserção** e cole-a no **URL de resposta** caixa de texto em **SAML básico Configuração** secção no portal do Azure. 

      ![Único configurações de logon](./media/timeoffmanager-tutorial/ic795915.png "único configurações de logon")

### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD 

O objetivo desta secção é criar um utilizador de teste no portal do Azure chamado Eduarda Almeida.

1. No portal do Azure, no painel esquerdo, selecione **do Azure Active Directory**, selecione **utilizadores**e, em seguida, selecione **todos os utilizadores**.

    !["Os utilizadores e grupos" e os links de "Todos os utilizadores"](common/users.png)

2. Selecione **novo utilizador** na parte superior do ecrã.

    ![Novo utilizador botão](common/new-user.png)

3. Nas propriedades do utilizador, execute os seguintes passos.

    ![A caixa de diálogo de utilizador](common/user-properties.png)

    a. Na **Name** campo introduza **BrittaSimon**.
  
    b. Na **nome de utilizador** tipo de campo brittasimon@yourcompanydomain.extension. Por exemplo, BrittaSimon@contoso.com

    c. Selecione **palavra-passe de Show** caixa de verificação e, em seguida, anote o valor que é apresentado na caixa de palavra-passe.

    d. Clique em **Criar**.

### <a name="assign-the-azure-ad-test-user"></a>Atribua o utilizador de teste do Azure AD

Nesta secção, vai ativar Eduarda Almeida utilizar o Azure início de sessão único ao conceder acesso para TimeOffManager.

1. No portal do Azure, selecione **aplicações empresariais**, selecione **todos os aplicativos**, em seguida, selecione **TimeOffManager**.

    ![Painel de aplicações empresariais](common/enterprise-applications.png)

2. Na lista de aplicações, selecione **TimeOffManager**.

    ![A ligação de TimeOffManager na lista de aplicações](common/all-applications.png)

3. No menu à esquerda, selecione **utilizadores e grupos**.

    ![A ligação "Utilizadores e grupos"](common/users-groups-blade.png)

4. Clique nas **adicionar utilizador** botão, em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar atribuição](common/add-assign-user.png)

5. Na **utilizadores e grupos** caixa de diálogo select **Eduarda Almeida** na lista de utilizadores, em seguida, clique o **selecionar** na parte inferior do ecrã.

6. Se está esperando a qualquer valor de função a asserção de SAML, em seguida, no **selecionar função** caixa de diálogo selecione a função adequada para o utilizador na lista, em seguida, clique o **selecione** na parte inferior do ecrã.

7. Na **adicionar atribuição** clique da caixa de diálogo a **atribuir** botão.

### <a name="create-timeoffmanager-test-user"></a>Criar utilizador de teste TimeOffManager

Nesta secção, um usuário chamado Eduarda Almeida é criado na TimeOffManager. TimeOffManager suporta o aprovisionamento de utilizadores de just-in-time, que está ativado por predefinição. Não existe nenhum item de ação para nesta secção. Se um utilizador já não existir no TimeOffManager, é criado um novo após a autenticação.

>[!NOTE]
>Pode utilizar quaisquer outras TimeOffManager utilizador conta criação ferramentas ou APIs fornecidas pelo TimeOffManager para aprovisionar contas de utilizador do Azure AD.
> 

### <a name="test-single-sign-on"></a>Testar o início de sessão único 

Nesta secção, vai testar a configuração do Azure AD única início de sessão com o painel de acesso.

Quando clica no mosaico TimeOffManager no painel de acesso, deve ser automaticamente sessão iniciada no TimeOffManager para o qual configura o SSO. Para obter mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).

## <a name="additional-resources"></a>Recursos Adicionais

- [Lista de tutoriais sobre como integrar aplicações SaaS com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [O que é o acesso a aplicações e início de sessão único com o Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [O que é o acesso condicional no Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

