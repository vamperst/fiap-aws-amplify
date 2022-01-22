## Criar aplicação e adicionar autenticação

1. Certifique-se de que esta na raiz do seu IDE executando o comando `cd ~/environment` no terminal.
2. Agora vamos baixar o template de react que iremos utilizar durante as demos de amplify. Para tal execute o comando `npx create-react-app postagram`
3. Entre na pasta criada para o projeto com o comando `cd postagram/`
4. Instale as dependencias node necessárias para o projeto com o comando: `npm install aws-amplify @emotion/css uuid react-router-dom@5 @aws-amplify/ui-react`
   ![img/dependencies-install.png](img/dependencies-install.png)
5. Agora você vai configurar o usuario a ser utilizado pelo amplify na sua maquina. Para iniciar o processo execute o comando `amplify configure`
6. Precione enter para confirmar que esta como administrador. Então selecione `us-east-1` no seletor de região. E no ultima parte desse passo ele pergunta o nome do usuario a ser criado para o amplify. De o nome de `amplify-fiap`. Ele irá mostrar uma URL, clique nela para ir a outra página do console AWS onde irá criar o usuario. NÃO CLIQUE ENTER ATÉ QUE TENHA EXECUTADO ATÉ O PASSO 10.
![img/configure-1.png](img/configure-1.png)
7. Avance na página inicial do IAM
   ![img/iam-1.png](img/iam-1.png)
8. Avance na página de permissões se estiver como na imagem:
![img/iam-2.png](img/iam-2.png)
9. Avance para a pagina de revisão e crie o usuario.
    ![img/iam-3.png](img/iam-3.png)
10. COPIE o id de chave de acesso e chave de acesso secreta em um lugar onde não irá perder pois essas credencias serão necessarias algumas vezes ao longo do curso.
    ![img/iam-4.png](img/iam-4.png)
11. De volta ao terminal do Cloud9, pressione enter para continuar.
12. Cole a accessKey e secretKey copiadas no passo 10 e pressione enter.
    ![](img/configure-2.png)
13. De o nome de `amplify-fiap` ao perfil das credenciais localmente.
    ![](img/configure-3.png)
14. Agora você vai iniciar o amplify no projeto. Para garantir que esta na pasta certa execute o comando `cd ~/environment/postagram` e então execute o comando `amplify init`
15. Deixa as opções como na imagem abaixo:
    ![](img/init-1.png)
16. Selecione `AWS access keys` como meio de acesso e novamente cole as credenciais do passo 10 e selecione a região `us-east-1`.
    ![](img/init-2.png)
17. Após esse processo o amplify vai criar a base do projeto na sua conta AWS utilizando cloudformation. É possivel ver o status do projeto com o comando `amplify status`
    ![](img/status-1.png)
18. Agora vamos criar o [cognito](https://docs.aws.amazon.com/pt_br/cognito/latest/developerguide/what-is-amazon-cognito.html) a ser utilizado no nosso projeto para cuidar da parte de autenticação e autorização. Para tal, execute o comando `amplify add auth` e deixa as opções como abaixo:
    ![](img/auth-1.png)
19. As alterações feitas ainda não foram aplicadas na sua conta AWS. Para tal execute o comando `amplify push -y`:
    ![](img/auth-2.png)
    ![](img/auth-3.png)
20. Agora que o recurso de autenticação já foi criado na sua conta é hora de adicionar o código que irá cuidar disso no código do projeto. Para abrir o script principal utilize o comando `c9 open src/App.js`. Isso vai abrir o arquivo no IDE como na imagem abaixo para que você possa editar o arquivo.
![](img/auth-4.png)
21. Deixe o arquivo como na imagem abaixo, note que a function app esta contraida e não alterada para caber todo o código do passo em apenas um print.
    ![](img/auth-5.png)
22. Para salvar utilize CTRL + S. 
23. Agora vamos liberar a porta 8080 da maquina onde estamos desenvolvendo para que possa acessar o server que vai subir ao testar o código localmente. Para isso irá precisar abrir um console da aws em outra aba e ir para o serviço EC2 como nas imagens abaixo:
    1.  No canto direito superior clique na letra e então clique em `Manage ec2 instance`
    ![](img/manage-ec2-1.png)
    2. Selecione a instancia EC2 e vá para a aba `Segurança` e clique no nome do grupo de segurança.
    ![](img/manage-ec2-2.png)
    3. No lado direito inferior clique em `editar regras de entrada`
    ![](img/manage-ec2-3.png)
    4. Adicione uma regra TCP personalizada como na imagem abaixo e salve.
    ![](img/manage-ec2-4.png)
24. De volta para o terminal do Cloud9, execute o comando `npm start` para iniciar o server de frontend local na sua maquina do Cloud9.
    ![](img/auth-6.png)
25. Abra novamente a pagina da ec2 utilizada pelo cloud9 e na aba Detalehe e copie somente o ip publico.
    ![](img/auth-7.png)
26. Em uma nova aba cole o ip publico copiado com e adicione a porta 8080, ippublico:8080, para acessar o software recém criado.
    ![](img/use-1.png)
27. Crie uma conta com um email valido em `Create account` e acesse o software.
    ![](img/use-2.png)
    ![](img/use-3.png)
    ![](img/use-4.png)
28. Agora vamos adicionar um botão de `Logout` na ferramenta, para isso pare o server no terminal do cloud 9 com o comando `CTRL + C`.
29. Abra novamente o arquivo App.js com o comando `c9 open src/App.js` caso tenha fechado.
30. Deixe a function App como na imagem abaixo. As linhas alteradas são as 14 e 31 da imagem.
    ![](img/out-1.png)
31. Salve o arquivo com CTRL + S.
32. Execute novamente o comando `npm start` e acesse novamente o ip publico na porta 8080. Verá que agora tem um botão para fazer o Sign out da aplicação na parte inferior da página e retorna direto para a tela de login.
    