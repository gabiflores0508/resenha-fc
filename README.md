# Resenha FC

Página única (`index.html`) que roda de graça no Render, na Vercel ou na Netlify. Os dados ficam no Firebase (Firestore) e a galera entra com a conta Google. Nos planos grátis do Firebase e da hospedagem sobra espaço pra uma pelada.

Os nomes dos menus do Firebase podem variar um pouco, mas o caminho é este.

## 1. Criar o projeto no Firebase

1. Entre em https://console.firebase.google.com e clique em **Criar um projeto**.
2. Dê um nome (por exemplo, `resenha-fc`). O Google Analytics pode ficar desligado.

## 2. Ligar o login com Google

1. No menu da esquerda, vá em **Criação > Authentication** e clique em **Vamos começar**.
2. Na aba **Método de login**, escolha **Google**, ative, selecione um e-mail de suporte e salve.

## 3. Criar o banco de dados

1. Vá em **Criação > Firestore Database** e clique em **Criar banco de dados**.
2. Escolha o local `southamerica-east1 (São Paulo)`.
3. Escolha **modo de produção**.

## 4. Colar as regras de segurança

1. No Firestore, abra a aba **Regras**.
2. Apague o que tiver lá e cole o conteúdo do arquivo `firestore.rules`.
3. Troque `SEU_EMAIL@gmail.com` pelo seu e-mail do Google e clique em **Publicar**.

As regras garantem que cada um só mexe no próprio perfil e na própria foto. Quadra, sorteio, pagamento e placar só podem ser alterados por adm. Dia fixo e lista de adm, só pelo dono.

## 5. Colocar a configuração no index.html

1. No Firebase, clique na engrenagem e vá em **Configurações do projeto**.
2. Em **Seus apps**, clique no ícone **</>** (Web), dê um apelido e registre. Não precisa marcar o Firebase Hosting.
3. Copie os valores do `firebaseConfig` que aparecem na tela.
4. Abra o `index.html`, procure `PELADA_CONFIG` perto do fim do arquivo e cole cada valor no lugar certo.
5. No mesmo bloco, troque `ownerEmail` pelo seu e-mail do Google (o mesmo das regras).

Esses valores não são segredo, podem ir pro GitHub. O que protege os dados são as regras do passo 4.

## 6. Publicar

### No Render (grátis)

1. Crie uma conta em https://github.com (se ainda não tiver) e um repositório novo chamado `resenha-fc`.
2. No repositório, clique em **Add file > Upload files**, arraste os quatro arquivos desta pasta (`index.html`, `firestore.rules`, `render.yaml` e `README.md`) e clique em **Commit changes**.
3. Abra este link, trocando `SEU_USUARIO` pelo seu usuário do GitHub:
   `https://dashboard.render.com/blueprint/new?repo=https://github.com/SEU_USUARIO/resenha-fc`
4. Entre no Render com a conta do GitHub, autorize o acesso ao repositório e clique em **Apply**.
5. Em um ou dois minutos o site fica no ar num endereço como `https://resenha-fc.onrender.com`.

Pra atualizar depois, é só editar o `index.html` no GitHub: o Render publica de novo sozinho.

### Na Vercel

1. Suba os arquivos num repositório do GitHub, como no Render.
2. Em https://vercel.com/new, importe o repositório.
3. Em **Framework Preset**, escolha **Other** e clique em **Deploy**.

Pelo terminal também dá: `cd resenha-fc`, depois `npx vercel` e `npx vercel --prod`.

### Na Netlify (sem GitHub)

Abra https://app.netlify.com/drop e arraste a pasta `resenha-fc` pra página.

## 7. Autorizar o endereço do site no Firebase

Sem isso, o login com Google dá erro.

1. No Firebase, vá em **Authentication > Configurações > Domínios autorizados**.
2. Clique em **Adicionar domínio** e coloque o endereço do site sem `https://`, por exemplo `resenha-fc.onrender.com` (Render) ou `resenha-fc.vercel.app` (Vercel).
3. Se usar um domínio próprio, adicione ele também.

## 8. Testar

1. Abra o site e entre com o mesmo e-mail que você colocou como dono. A aba **Admin** tem que aparecer.
2. Coloque seu apelido, confirme a quadra da próxima quinta e peça pra um amigo entrar pelo celular.
3. Depois que a galera entrar, marque os outros adm em **Admin > Quem é adm**.

## Bom saber

- **Trocar o nome do grupo:** mude `appName` no bloco `PELADA_CONFIG` do `index.html`.

- **Quem pode entrar:** qualquer pessoa com conta Google que tiver o link. Apelidos, fotos, lista e chave Pix ficam visíveis pra quem entrar.
- **Erro `unauthorized-domain` no login:** faltou o passo 7.
- **Aba Admin não aparece pra você:** o e-mail no `index.html` e nas regras tem que ser exatamente o da sua conta Google.
- **Trocar o dono:** mude o e-mail nos dois lugares (`index.html` e regras) e publique as regras de novo.
- **Atualizar a página:** edite o `index.html` e suba de novo. Pelo GitHub, o Render e a Vercel publicam sozinhos a cada envio.
