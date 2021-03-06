---
title: 'Tutorial: Integração do Active Directory do Azure com Deskradar | Documentos da Microsoft'
description: Saiba como configurar o início de sessão único entre o Azure Active Directory e Deskradar.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.reviewer: barbkess
ms.assetid: 5ff3e014-b79f-4a6c-bb0b-38462bea5d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/04/2019
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: ea17794a5ca57ae0d38d9a90857706cf380cab36
ms.sourcegitcommit: 2d0fb4f3fc8086d61e2d8e506d5c2b930ba525a7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/18/2019
ms.locfileid: "57895673"
---
# <a name="tutorial-azure-active-directory-integration-with-deskradar"></a>Tutorial: Integração do Active Directory do Azure com Deskradar

Neste tutorial, saiba como integrar Deskradar com o Azure Active Directory (Azure AD).
Integrar Deskradar no Azure AD fornece as seguintes vantagens:

* Pode controlar no Azure AD que tenha acesso ao Deskradar.
* Pode permitir que os utilizadores ser automaticamente sessão iniciada para Deskradar (Single Sign-On) com as suas contas do Azure AD.
* Pode gerir as suas contas num local central – portal do Azure.

Se quiser saber mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [o que é o acesso a aplicações e início de sessão único com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis).
Se não tiver uma subscrição do Azure, [crie uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com Deskradar, terá dos seguintes itens:

* Uma subscrição do Azure AD. Se não tiver um ambiente do Azure AD, pode obter a versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/)
* Deskradar logon único habilitado subscrição

## <a name="scenario-description"></a>Descrição do cenário

Neste tutorial, configure e teste do Azure AD início de sessão único num ambiente de teste.

* Suporta Deskradar **SP e IDP** iniciada SSO

## <a name="add-deskradar-from-the-gallery"></a>Adicionar Deskradar a partir da Galeria

Para configurar a integração do Deskradar com o Azure AD, terá de adicionar Deskradar a partir da Galeria à sua lista de aplicações de SaaS geridas.

**Para adicionar Deskradar a partir da galeria, execute os seguintes passos:**

1. Na **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo, clique em **Azure Active Directory** ícone.

    ![O botão do Azure Active Directory](common/select-azuread.png)

2. Navegue para **aplicações empresariais** e, em seguida, selecione a **todos os aplicativos** opção.

    ![O painel de aplicações empresariais](common/enterprise-applications.png)

3. Para adicionar nova aplicação, clique em **nova aplicação** botão na parte superior de caixa de diálogo.

    ![O novo botão de aplicativo](common/add-new-app.png)

4. Na caixa de pesquisa, escreva **Deskradar**, selecione **Deskradar** no painel de resultados, em seguida, clique em **Add** botão para adicionar a aplicação.

     ![Deskradar na lista de resultados](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD início de sessão único

Nesta secção, configurar e testar o Azure AD início de sessão único com [nome da aplicação] com base num utilizador de teste **Eduarda Almeida**.
Para o início de sessão único funcionar, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionado em [nome da aplicação] deve ser estabelecido.

Para configurar e testar o Azure AD início de sessão único com [nome da aplicação], tem de concluir os seguintes blocos de construção:

1. **[Configurar o Azure AD início de sessão único](#configure-azure-ad-single-sign-on)**  - para permitir que os utilizadores utilizar esta funcionalidade.
2. **[Configurar Deskradar Single Sign-On](#configure-deskradar-single-sign-on)**  - para configurar as definições de início de sessão único no lado do aplicativo.
3. **[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  - para testar o Azure AD início de sessão único com Eduarda Almeida.
4. **[Atribua o utilizador de teste do Azure AD](#assign-the-azure-ad-test-user)**  - para ativar a Eduarda Almeida utilizar o Azure AD início de sessão único.
5. **[Criar utilizador de teste Deskradar](#create-deskradar-test-user)**  - para ter um equivalente da Eduarda Almeida na Deskradar que está ligado à representação de utilizador do Azure AD.
6. **[Testar início de sessão único](#test-single-sign-on)**  - para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o Azure AD início de sessão único

Nesta secção, vai ativar o Azure AD início de sessão único no portal do Azure.

Para configurar o Azure AD início de sessão único com [nome da aplicação], execute os seguintes passos:

1. Na [portal do Azure](https://portal.azure.com/), na **Deskradar** página de integração de aplicações, selecione **início de sessão único**.

    ![Configurar a ligação de início de sessão única](common/select-sso.png)

2. Sobre o **selecionar um método de início de sessão único** caixa de diálogo, selecione **SAML/WS-Fed** modo para ativar o início de sessão único.

    ![Único início de sessão em modo de seleção](common/select-saml-option.png)

3. Sobre o **definir a segurança de início de sessão único com o SAML** página, clique em **editar** ícone para abrir **configuração básica de SAML** caixa de diálogo.

    ![Editar a configuração SAML do básico](common/edit-urls.png)

4. Sobre o **configuração básica de SAML** secção, se desejar configurar a aplicação no **IDP** iniciada pelo modo, execute os seguintes passos:

    ![Deskradar domínio e URLs únicas início de sessão em informações](common/idp-intiated.png)

    a. Na **identificador** caixa de texto, escreva um URL com o seguinte padrão: `https://YOURDOMAIN.deskradar.cloud`

    b. Na **URL de resposta** caixa de texto, escreva um URL com o seguinte padrão: `https://YOURDOMAIN.deskradar.cloud/auth/sso/saml/consume`

5. Clique em **definir URLs adicionais** e executar o passo seguinte, se desejar configurar a aplicação na **SP** iniciada pelo modo:

    Na **URL de início de sessão** caixa de texto, escreva um URL com o seguinte padrão:  `https://YOURDOMAIN.deskradar.cloud/auth/sso/saml/login`

    ![Deskradar domínio e URLs únicas início de sessão em informações](common/metadata-upload-additional-signon.png)

    > [!NOTE]
    > Estes valores não são reais. Atualize estes valores com o URL de identificador, o URL de resposta e início de sessão real. Substitua **OSEUDOMÍNIO** com o domínio de instância Deskradar. Contacte [equipa de suporte de cliente Deskradar](mailto:support@deskradar.com) obter esses valores. Também pode consultar os padrões mostrados a **configuração básica de SAML** secção no portal do Azure.

6. Aplicação de Deskradar espera que as asserções SAML num formato específico. Configure as seguintes declarações para esta aplicação. Pode gerir os valores destes atributos do **atributos de utilizador** secção na página de integração de aplicações. Sobre o **definido no início de sessão único com o SAML** página, clique em **editar** botão para abrir **atributos de utilizador** caixa de diálogo.

    ![image](common/edit-attribute.png)

7. No **afirmações de utilizador** secção sobre o **atributos de utilizador** caixa de diálogo, configurar o atributo de token de SAML conforme mostrado na imagem acima e execute os seguintes passos:

    | Name | Atributo de origem|
    | ---------------| --------- |
    | FirstName | user.givenname |
    | LastName | user.surname |
    | Email | user.userprincipalname |
    | | |

    a. Clique em **Adicionar nova afirmação** para abrir o **afirmações de utilizador de gerir** caixa de diálogo.

    ![image](common/new-save-attribute.png)

    ![image](common/new-attribute-details.png)

    b. Na **nome** caixa de texto, escreva o nome de atributo apresentado para essa linha.

    c. Deixe o **espaço de nomes** em branco.

    d. Selecione a origem de dado **atributo**.

    e. Partir do **atributo de origem** lista, digite o valor de atributo apresentado para essa linha.

    f. Clique em **OK**.

    g. Clique em **Guardar**.

8. No **definido no início de sessão único com o SAML** página, além do **certificado de assinatura SAML** secção, clique em **transferir** para transferir o **certificado (Base64)** entre as opções de determinado de acordo com seus requisitos e guarde-o no seu computador.

    ![O link de download de certificado](common/certificatebase64.png)

9. Sobre o **configurar Deskradar** secção, copie os URLs apropriados de acordo com seus requisitos.

    ![URLs de configuração de cópia](common/copy-configuration-urls.png)

    a. URL de início de sessão

    b. Azure Ad Identifier

    c. URL de fim de sessão

### <a name="configure-deskradar-single-sign-on"></a>Configurar Deskradar Single Sign-On

1. Inicie sessão sua instância de Deskradar com a conta de administrador através de e-mail e palavra-passe que definiu quando se inscreveu com uma ligação de convite.

2. Open **equipe** painel ao clicar no ícone na barra lateral.

3. Mude para o **autenticação** separador.

4. Sobre o **SAML 2.0** separador, execute os seguintes passos:

    ![Configuração de Deskradar](./media/deskradar-tutorial/14-paste-urls.jpg)

    a. Ativar **SAML** método de autenticação.

    b. Na **URL de SSO SAML** caixa de texto, introduza o **URL de início de sessão** valor, que copiou do portal do Azure.

    c. Na **emissor do fornecedor de identidade** caixa de texto, introduza o **do Azure AD identificador** valor, que copiou do portal do Azure.

5. Abra o transferido **certificado (Base64)** ficheiro com um editor de texto e copie e cole-os em **certificado público** na Deskradar.

    ![Configuração de Deskradar](./media/deskradar-tutorial/15-paste-certificate.jpg)

### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD

O objetivo desta secção é criar um utilizador de teste no portal do Azure chamado Eduarda Almeida.

1. No portal do Azure, no painel esquerdo, selecione **do Azure Active Directory**, selecione **utilizadores**e, em seguida, selecione **todos os utilizadores**.

    !["Os utilizadores e grupos" e os links de "Todos os utilizadores"](common/users.png)

2. Selecione **novo utilizador** na parte superior do ecrã.

    ![Novo utilizador botão](common/new-user.png)

3. Nas propriedades do utilizador, execute os seguintes passos.

    ![A caixa de diálogo de utilizador](common/user-properties.png)

    a. Na **Name** , insira **BrittaSimon**.
  
    b. Na **nome de utilizador** tipo de campo **brittasimon\@yourcompanydomain.extension**  
    Por exemplo, BrittaSimon@contoso.com

    c. Selecione **palavra-passe de Show** caixa de verificação e, em seguida, anote o valor que é apresentado na caixa de palavra-passe.

    d. Clique em **Criar**.

### <a name="assign-the-azure-ad-test-user"></a>Atribua o utilizador de teste do Azure AD

Nesta secção, vai ativar Eduarda Almeida utilizar o Azure início de sessão único ao conceder acesso para Deskradar.

1. No portal do Azure, selecione **aplicações empresariais**, selecione **todos os aplicativos**, em seguida, selecione **Deskradar**.

    ![Painel de aplicações empresariais](common/enterprise-applications.png)

2. Na lista de aplicações, selecione **Deskradar**.

    ![A ligação de Deskradar na lista de aplicações](common/all-applications.png)

3. No menu à esquerda, selecione **utilizadores e grupos**.

    ![A ligação "Utilizadores e grupos"](common/users-groups-blade.png)

4. Clique nas **adicionar utilizador** botão, em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar atribuição](common/add-assign-user.png)

5. Na **utilizadores e grupos** caixa de diálogo select **Eduarda Almeida** na lista de utilizadores, em seguida, clique o **selecionar** na parte inferior do ecrã.

6. Se está esperando a qualquer valor de função a asserção de SAML, em seguida, no **selecionar função** caixa de diálogo selecione a função adequada para o utilizador na lista, em seguida, clique o **selecione** na parte inferior do ecrã.

7. Na **adicionar atribuição** caixa de diálogo, clique nas **atribuir** botão.

### <a name="create-deskradar-test-user"></a>Criar utilizador de teste Deskradar

Nesta secção, vai criar um usuário chamado Eduarda Almeida no Deskradar. Trabalhar com [equipa de suporte de cliente Deskradar](mailto:support@deskradar.com) para adicionar os utilizadores na plataforma Deskradar. Os utilizadores tem de ser criados e ativados antes de utilizar o início de sessão único.

### <a name="test-single-sign-on"></a>Testar o início de sessão único

Nesta secção, vai testar a configuração do Azure AD única início de sessão com o painel de acesso.

**Para utilizar a aplicação no SP iniciada pelo modo siga os passos abaixo:**

1. Inicie a sua instância de Deskradar ao abrir o URL no seu browser: `https://YOURDOMAIN.deskradar.cloud` (substitua `YOURDOMAIN` com o domínio de instância Deskradar). 
1. Selecione **Enterprise Single Sign-On.**

    ![Deskradar](./media/deskradar-tutorial/16-sso-button.jpg)

- Irá entrar para Deskradar diretamente, se já tem sessão iniciada no Active Directory.
- Será redirecionado para o Active Directory formulário de sessão, se não estiver inscrito ainda. Pode introduzir as credenciais de conta empresarial lá para iniciar sessão.
- Será direcionado novamente para Deskradar e a sessão iniciada no Deskradar após o início de sessão com êxito com as suas credenciais de conta empresarial.

**Para utilizar a aplicação no IDP iniciada a seguir de modo a abaixo passo:**

Quando clica no mosaico Deskradar no painel de acesso, deve ser automaticamente sessão iniciada no Deskradar para o qual configura o SSO. Para obter mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).

## <a name="additional-resources"></a>Recursos Adicionais

- [Lista de tutoriais sobre como integrar aplicações SaaS com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [What is application access and single sign-on with Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis) (O que é o acesso a aplicações e o início de sessão único com o Azure Active Directory?)

- [O que é o acesso condicional no Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
