---
title: 'Tutorial: Integração do Active Directory do Azure com AirWatch | Documentos da Microsoft'
description: Saiba como configurar o início de sessão único entre o Azure Active Directory e AirWatch.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 02/07/2019
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: e20a298c34a7b2723963396f8ccaafaa9472e19a
ms.sourcegitcommit: 2d0fb4f3fc8086d61e2d8e506d5c2b930ba525a7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/18/2019
ms.locfileid: "57888336"
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a>Tutorial: Integração do Active Directory do Azure com AirWatch

Neste tutorial, saiba como integrar AirWatch com o Azure Active Directory (Azure AD).
Integrar AirWatch no Azure AD fornece as seguintes vantagens:

* Pode controlar no Azure AD que tenha acesso ao AirWatch.
* Pode permitir que os utilizadores ser automaticamente sessão iniciada para AirWatch (Single Sign-On) com as suas contas do Azure AD.
* Pode gerir as suas contas num local central – portal do Azure.

Se quiser saber mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [o que é o acesso a aplicações e início de sessão único com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis).
Se não tiver uma subscrição do Azure, [crie uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com AirWatch, terá dos seguintes itens:

* Uma subscrição do Azure AD. Se não tiver um ambiente do Azure AD, pode obter a versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/)
* AirWatch logon único habilitado subscrição

## <a name="scenario-description"></a>Descrição do cenário

Neste tutorial, configure e teste do Azure AD início de sessão único num ambiente de teste.

* Suporta AirWatch **SP** iniciada SSO

## <a name="adding-airwatch-from-the-gallery"></a>Adicionando AirWatch da Galeria

Para configurar a integração da AirWatch com o Azure AD, terá de adicionar AirWatch a partir da Galeria à sua lista de aplicações de SaaS geridas.

**Para adicionar AirWatch a partir da galeria, execute os seguintes passos:**

1. Na **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo, clique em **Azure Active Directory** ícone.

    ![O botão do Azure Active Directory](common/select-azuread.png)

2. Navegue para **aplicações empresariais** e, em seguida, selecione a **todos os aplicativos** opção.

    ![O painel de aplicações empresariais](common/enterprise-applications.png)

3. Para adicionar nova aplicação, clique em **nova aplicação** botão na parte superior de caixa de diálogo.

    ![O novo botão de aplicativo](common/add-new-app.png)

4. Na caixa de pesquisa, escreva **AirWatch**, selecione **AirWatch** no painel de resultados, em seguida, clique em **Add** botão para adicionar a aplicação.

     ![AirWatch na lista de resultados](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar o Azure AD início de sessão único

Nesta secção, configure e teste do Azure AD início de sessão único com AirWatch com base num utilizador de teste **Eduarda Almeida**.
Para o início de sessão único funcionar, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionado no AirWatch deve ser estabelecido.

Para configurar e testar o Azure AD início de sessão único com AirWatch, tem de concluir os seguintes blocos de construção:

1. **[Configurar o Azure AD início de sessão único](#configure-azure-ad-single-sign-on)**  - para permitir que os utilizadores utilizar esta funcionalidade.
2. **[Configurar AirWatch Single Sign-On](#configure-airwatch-single-sign-on)**  - para configurar as definições de início de sessão único no lado do aplicativo.
3. **[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  - para testar o Azure AD início de sessão único com Eduarda Almeida.
4. **[Criar utilizador de teste da AirWatch](#create-airwatch-test-user)**  - para ter um equivalente da Eduarda Almeida na AirWatch que está ligado à representação de utilizador do Azure AD.
5. **[Atribua o utilizador de teste do Azure AD](#assign-the-azure-ad-test-user)**  - para ativar a Eduarda Almeida utilizar o Azure AD início de sessão único.
6. **[Testar início de sessão único](#test-single-sign-on)**  - para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o Azure AD início de sessão único

Nesta secção, vai ativar o Azure AD início de sessão único no portal do Azure.

Para configurar o Azure AD início de sessão único com AirWatch, execute os seguintes passos:

1. Na [portal do Azure](https://portal.azure.com/), na **AirWatch** página de integração de aplicações, selecione **início de sessão único**.

    ![Configurar a ligação de início de sessão única](common/select-sso.png)

2. Sobre o **selecionar um método de início de sessão único** caixa de diálogo, selecione **SAML/WS-Fed** modo para ativar o início de sessão único.

    ![Único início de sessão em modo de seleção](common/select-saml-option.png)

3. Sobre o **definir a segurança de início de sessão único com o SAML** página, clique em **editar** ícone para abrir **configuração básica de SAML** caixa de diálogo.

    ![Editar a configuração SAML do básico](common/edit-urls.png)

4. Sobre o **configuração básica de SAML** secção, execute os seguintes passos:

    ![AirWatch domínio e URLs únicas início de sessão em informações](common/sp-identifier.png)

    a. Na **iniciar sessão no URL** caixa de texto, escreva um URL com o seguinte padrão: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`

    b. Na **identificador (ID de entidade)** texto, escreva o valor como: `AirWatch`

    > [!NOTE]
    > Este valor não é a verdadeira. Atualize este valor com o URL de início de sessão real. Contacte [equipa de suporte de cliente da AirWatch](https://www.air-watch.com/company/contact-us/) para obter este valor. Também pode consultar os padrões mostrados a **configuração básica de SAML** secção no portal do Azure.

5. Aplicação da AirWatch espera que as asserções SAML num formato específico. Configure as seguintes declarações para esta aplicação. Pode gerir os valores destes atributos do **atributos de utilizador** secção na página de integração de aplicações. Sobre o **definido no início de sessão único com o SAML** página, clique em **editar** botão para abrir **atributos de utilizador** caixa de diálogo.

    ![image](common/edit-attribute.png)

6. No **afirmações de utilizador** secção sobre o **atributos de utilizador** caixa de diálogo, editar as afirmações utilizando **ícone de edição** ou adicionar as afirmações utilizando **Adicionar nova afirmação**para configurar o atributo de token SAML conforme mostrado na imagem acima e execute os seguintes passos:

    | Name |  Atributo de origem|
    |---------------|----------------|
    | UID | user.userprincipalname |
    | | |

    a. Clique em **Adicionar nova afirmação** para abrir o **afirmações de utilizador de gerir** caixa de diálogo.

    ![image](common/new-save-attribute.png)

    ![image](common/new-attribute-details.png)

    b. Na **nome** caixa de texto, escreva o nome de atributo apresentado para essa linha.

    c. Deixe o **espaço de nomes** em branco.

    d. Selecione a origem de dado **atributo**.

    e. Partir do **atributo de origem** lista, digite o valor de atributo apresentado para essa linha.

    f. Clique em **Ok**

    g. Clique em **Guardar**.

7. No **definido no início de sessão único com o SAML** página, além do **certificado de assinatura SAML** secção, clique em **transferir** para transferir o **XML de metadados de Federação**  entre as opções de determinado de acordo com seus requisitos e guarde-o no seu computador.

    ![O link de download de certificado](common/metadataxml.png)

8. Sobre o **configurar AirWatch** secção, copie os URLs apropriados de acordo com seus requisitos.

    ![URLs de configuração de cópia](common/copy-configuration-urls.png)

    a. URL de início de sessão

    b. Azure Ad Identifier

    c. URL de fim de sessão

### <a name="configure-airwatch-single-sign-on"></a>Configurar AirWatch Single Sign-On

1. Numa janela do browser web diferente, inicie sessão no site da sua empresa AirWatch como administrador.

2. No painel de navegação esquerdo, clique em **contas**e, em seguida, clique em **administradores**.

   ![Os administradores](./media/airwatch-tutorial/ic791920.png "administradores")

3. Expanda a **definições** e, em seguida, clique **dos serviços de diretório**.

   ![As definições](./media/airwatch-tutorial/ic791921.png "definições")

4. Clique nas **usuário** separador a **Base DN** caixa de texto, escreva o seu nome de domínio e, em seguida, clique em **guardar**.

   ![Usuário](./media/airwatch-tutorial/ic791922.png "utilizador")

5. Clique nas **servidor** separador.

   ![Server](./media/airwatch-tutorial/ic791923.png "Server")

6. Execute os seguintes passos:

    ![Carregue](./media/airwatch-tutorial/ic791924.png "carregar")   

    a. Como **tipo de diretório**, selecione **nenhum**.

    b. Selecione **utilizar SAML para autenticação**.

    c. Para carregar o certificado transferido, clique em **carregar**.

7. Na **pedir** secção, execute os seguintes passos:

    ![Pedir](./media/airwatch-tutorial/ic791925.png "do pedido")  

    a. Como **solicitar tipo de enlace**, selecione **POST**.

    b. No portal do Azure, no **configurar o início de sessão único em Airwatch** página de diálogo, copie a **URL de início de sessão** valor e, em seguida, cole-o no **fornecedor único início de sessão no URL de identidade** caixa de texto.

    c. Como **formato NameID**, selecione **endereço de E-Mail**.

    d. Clique em **Guardar**.

8. Clique nas **utilizador** separador novamente.

    ![Usuário](./media/airwatch-tutorial/ic791926.png "utilizador")

9. Na **atributo** secção, execute os seguintes passos:

    ![Atributo](./media/airwatch-tutorial/ic791927.png "atributo")

    a. Na **identificador de objeto** caixa de texto, tipo `http://schemas.microsoft.com/identity/claims/objectidentifier`.

    b. Na **nome de utilizador** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.

    c. Na **nome a apresentar** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.

    d. Na **nome próprio** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.

    e. Na **sobrenome** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.

    f. Na **E-Mail** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.

    g. Clique em **Guardar**.

### <a name="create-an-azure-ad-test-user"></a>Criar um utilizador de teste do Azure AD 

O objetivo desta secção é criar um utilizador de teste no portal do Azure chamado Eduarda Almeida.

1. No portal do Azure, no painel esquerdo, selecione **do Azure Active Directory**, selecione **utilizadores**e, em seguida, selecione **todos os utilizadores**.

    !["Os utilizadores e grupos" e os links de "Todos os utilizadores"](common/users.png)

2. Selecione **novo utilizador** na parte superior do ecrã.

    ![Novo utilizador botão](common/new-user.png)

3. Nas propriedades do utilizador, execute os seguintes passos.

    ![A caixa de diálogo de utilizador](common/user-properties.png)

    a. Na **Name** campo introduza **BrittaSimon**.
  
    b. Na **nome de utilizador** tipo de campo **brittasimon\@yourcompanydomain.extension**  
    Por exemplo, BrittaSimon@contoso.com

    c. Selecione **palavra-passe de Show** caixa de verificação e, em seguida, anote o valor que é apresentado na caixa de palavra-passe.

    d. Clique em **Criar**.

### <a name="assign-the-azure-ad-test-user"></a>Atribua o utilizador de teste do Azure AD

Nesta secção, vai ativar Eduarda Almeida utilizar o Azure início de sessão único ao conceder acesso para AirWatch.

1. No portal do Azure, selecione **aplicações empresariais**, selecione **todos os aplicativos**, em seguida, selecione **AirWatch**.

    ![Painel de aplicações empresariais](common/enterprise-applications.png)

2. Na lista de aplicações, selecione **AirWatch**.

    ![A ligação da AirWatch na lista de aplicações](common/all-applications.png)

3. No menu à esquerda, selecione **utilizadores e grupos**.

    ![A ligação "Utilizadores e grupos"](common/users-groups-blade.png)

4. Clique nas **adicionar utilizador** botão, em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar atribuição](common/add-assign-user.png)

5. Na **utilizadores e grupos** caixa de diálogo select **Eduarda Almeida** na lista de utilizadores, em seguida, clique o **selecionar** na parte inferior do ecrã.

6. Se está esperando a qualquer valor de função a asserção de SAML, em seguida, no **selecionar função** caixa de diálogo selecione a função adequada para o utilizador na lista, em seguida, clique o **selecione** na parte inferior do ecrã.

7. Na **adicionar atribuição** clique da caixa de diálogo a **atribuir** botão.

### <a name="create-airwatch-test-user"></a>Criar utilizador de teste da AirWatch

Para ativar a utilizadores do Azure AD iniciar sessão no AirWatch, eles têm de ser aprovisionados para AirWatch. No caso da AirWatch, aprovisionamento é uma tarefa manual.

**Para configurar o aprovisionamento de utilizadores, execute os seguintes passos:**

1. Inicie sessão no seu **AirWatch** site da empresa como administrador.

2. No painel de navegação no lado esquerdo, clique em **contas**e, em seguida, clique em **utilizadores**.
  
   ![Os utilizadores](./media/airwatch-tutorial/ic791929.png "utilizadores")

3. Na **usuários** menu, clique em **vista de lista**e, em seguida, clique em **Add \> adicionar utilizador**.
  
   ![Adicionar utilizador](./media/airwatch-tutorial/ic791930.png "adicionar utilizador")

4. Sobre o **Adicionar / Editar utilizador** caixa de diálogo, execute os seguintes passos:

   ![Adicionar utilizador](./media/airwatch-tutorial/ic791931.png "adicionar utilizador")

   a. Tipo de **nome de utilizador**, **palavra-passe**, **Confirmar palavra-passe**, **nome próprio**, **Apelido**,  **Endereço de e-mail** de uma conta válida do Azure Active Directory que pretende aprovisionar em caixas de texto relacionadas.

   b. Clique em **Guardar**.

> [!NOTE]
> Pode utilizar quaisquer outras AirWatch utilizador conta criação ferramentas ou APIs fornecidas pelo AirWatch para aprovisionar contas de utilizador do AAD.

### <a name="test-single-sign-on"></a>Testar o início de sessão único

Nesta secção, vai testar a configuração do Azure AD única início de sessão com o painel de acesso.

Quando clica no mosaico da AirWatch no painel de acesso, deve ser automaticamente sessão iniciada no AirWatch para o qual configura o SSO. Para obter mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).

## <a name="additional-resources"></a>Recursos Adicionais

- [Lista de tutoriais sobre como integrar aplicações SaaS com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [What is application access and single sign-on with Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis) (O que é o acesso a aplicações e o início de sessão único com o Azure Active Directory?)

- [O que é o acesso condicional no Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
