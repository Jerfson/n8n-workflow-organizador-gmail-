# 🔑 Guia: Configuração do OAuth2 do Gmail no n8n

Para que o n8n consiga ler, marcar e mover e-mails na sua conta do Gmail, é necessário criar credenciais OAuth 2.0 no **Google Cloud Console**. Siga o passo a passo abaixo:

---

## 1. Criar um Projeto no Google Cloud Console

1. Acesse o [Google Cloud Console](https://console.cloud.google.com/).
2. Faça login com a conta Google que deseja integrar.
3. No topo da página, clique no seletor de projetos e em **Novo Projeto** (*New Project*).
4. Dê um nome ao projeto (ex.: `n8n-gmail-automation`) e clique em **Criar** (*Create*).

---

## 2. Ativar a Gmail API

1. No menu lateral, acesse **APIs e Serviços** > **Biblioteca** (*Library*).
2. Pesquise por **Gmail API**.
3. Clique em **Gmail API** e depois no botão **Ativar** (*Enable*).

---

## 3. Configurar a Tela de Consentimento OAuth (*OAuth consent screen*)

1. No menu lateral, vá para **APIs e Serviços** > **Tela de consentimento OAuth**.
2. Selecione **Externo** (*External*) e clique em **Criar**.
3. Preencha os campos obrigatórios:
   - **Nome do app:** `n8n Automator` (ou o nome que preferir)
   - **E-mail de suporte do usuário:** seu e-mail
   - **Dados de contato do desenvolvedor:** seu e-mail
4. Clique em **Salvar e continuar**.
5. Na etapa **Escopos** (*Scopes*), adicione os escopos necessários:
   - `https://www.googleapis.com/auth/gmail.modify` (ler, compor, enviar e modificar e-mails/etiquetas)
   - `https://www.googleapis.com/auth/gmail.send` (para envio de alertas)
6. Clique em **Salvar e continuar**.
7. Na etapa **Usuários de teste** (*Test users*), adicione o seu próprio e-mail do Gmail.
8. Clique em **Salvar e continuar** e volte ao Painel.

---

## 4. Criar as Credenciais OAuth 2.0

1. No menu lateral, vá para **APIs e Serviços** > **Credenciais** (*Credentials*).
2. Clique em **+ Criar credenciais** > **ID do cliente OAuth** (*OAuth client ID*).
3. Em **Tipo de aplicativo**, selecione **Aplicativo da Web** (*Web application*).
4. Em **URIs de redirecionamento autorizados** (*Authorized redirect URIs*), adicione o URI fornecido pelo n8n ao criar a credencial:
   - Geralmente é: `https://<seu-n8n>/rest/oauth2-credential/callback`
   - Se estiver usando o n8n localmente: `http://localhost:5678/rest/oauth2-credential/callback` (ou via túnel)
5. Clique em **Criar**.
6. Copie o **ID do cliente** (*Client ID*) e a **Chave secreta do cliente** (*Client Secret*).

---

## 5. Vincular a Credencial no n8n

1. No n8n, acesse o menu **Credentials** > **Add Credential**.
2. Busque por **Gmail OAuth2 API**.
3. Cole o **Client ID** e o **Client Secret** obtidos no passo anterior.
4. Clique em **Connect my account** / **Sign in with Google**.
5. Autorize o acesso na janela pop-up do Google.
6. Salve a credencial com um nome fácil de identificar (ex.: `Gmail account`).

---

## 6. Selecionar a Credencial no Fluxo

No fluxo importado, abra cada nó do Gmail (Gatilho, Nós de Etiqueta e Envio de E-mail) e selecione a credencial criada no campo **Credential for Gmail OAuth2**.
