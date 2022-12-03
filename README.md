# On19-S17-S18-Projeto-Livre

## Voltei mis amoressssss
Ela mesma, Agnes Melo;
Porém, pro projeto final, né? quem tá ansiosa respirah;<br><br>
![bjork gritah](https://64.media.tumblr.com/e4ac84e95284f4abc15bfdd63bb89a1c/tumblr_ml4r2etFcA1rok2afo1_500.gifv)
<br><br>
Vamos fazer desse processinho o mais indolor e tranquilo possível? Então se liga nas 4 coisas que são importantes da gente prestar atenção nessas duas semanas:
* Vamos checar como estão as ideias e os códigos dos projetos para entender de onde partir. Esse é também um momento de acolhimento e troca entre nós;
* Na apresentação para a banca, precisamos mostrar nossas rotas no postman para as juradas virarem a cadeira;
* Também é preciso gerar a documentação da nossa API através do swagger;
* E por último, precisamos deployar nossa API no render pra que ela esteja acessível, cronicamente online, igual a senhora que passa sete horas no twitter por dia;

Parece bastante coisa, mas a gente vai juntas e vai dar tudo certo! (ou assim espero né mias lindas)
<br><br>
## Documentação no swagger
Esse tuto eu roubei da May (a maior que temos), viu gurias? Bora que bora documentar esse babadoh:
* Abro meu projeto
* Abro o terminal na raiz do projeto
* Executo os seguintes comandos:
```
     $ npm i swagger-autogen swagger-ui-express (isso fará a instalacao do swagger autogen no nosso projeto)
     $ touch swagger.js (isso fará com que um arquivo swagger seja criado no nosso projeto)
     $ mkdir swagger/  (isso fará com que uma pasta swagger seja criada no nosso projeto)
 ```
* Depois da criação da pasta, vamos no arquivo swagger.js e adicionamos esse pedaço de código:
```
     const swaggerAutogen = require('swagger-autogen')();
     const outputFile = './swagger/swagger_output.json';
     const endpointsFiles = ['./src/app.js'];
     swaggerAutogen(outputFile, endpointsFiles);
```
* Iremos lá no nosso package.json e faremos a seguinte alteraçao:
```
  "script”: {
   "start": "nodemon server.js",
   "swagger-autogen": "node swagger.js",
 }
 ```
* Em seguida digitaremos o seguinte comando la no terminal:
```
npm run swagger-autogen
```
Note que foi criado um arquivo chamado swagger_output.json dentro da nossa pasta swagger.
Parabéns, vc ja tem sua documentação!!!!
Bora deixar nossa documentaçao mais visual?
* Vamos lá no nosso app.js e adicionaremos o seguinte código:
```
    const swaggerUi = require('swagger-ui-express');

    const swaggerFile = require('../swagger/swagger_output.json');

    app.use('/minha-rota-de-documentacao', swaggerUi.serve, swaggerUi.setup(swaggerFile));
```
* Em seguida, inicializaremos nosso projeto, é so digitar no terminal:
```
$ npm start
```
* Feito isso, acessaremos a nossa rota
```
localhost:3000/minha-rota-de-documentacao
```

PS: Estou usando a porta 3000, caso vc esteja usando alguma diferente, use ela, beleza?

## Deploy no render

* Na [página principal do Render](https://render.com/), clique no botão "Get started for free";
* Em seguida, clique no botão "GitHub" dentro das opções de registro e será redirecionada para o login do mesmo; preencha com suas credenciais do GitHub e ele te enviará um código por email (segurança é tudo né garoutas?), preencha o código corretamente;
* Na página seguinte, clique no botão "Authorize render";
* Logo depois, clique em "Complete sign up"; O render te mandará um email de confirmação de registro, abra o email na sua caixa de mensagens e clique no link para ativar sua conta;
* Com a conta ativada, já podemos começar o deploy! Na dashboard do render, clique em "New web service";
* Depois, no lado direito superior da tela, clique no link "Connect account" logo abaixo de "GitHub";
* O site mostrará as contas do github disponíveis para serem conectadas; selecione a conta onde sua API está e, logo depois, selecione "All repositories" e clique em "Install";
* Em seguida, selecione o seu projeto na lista de repositórios e clique em "Connect";
* Preencha o formulário com o nome do seu repositório; Em "Build Command", escreva "npm install"; Em "Start Command", escreva "npm start";
* No final da página, clique em "Create web service";
<br>A partir daí, o render já vai querer deployar nossa API (mt apressado o bicho), mas o deploy vai falhar; pra que ele funcione, precisamos adicionar nossas variáveis de ambiente:
* No menu esquerdo, clique em "Environment";
* Nessa página, clique em "Add environment variable" para adicionar todas as variáveis de ambiente necessárias (aquelas que estão no seu arquivo .env do projeto), MENOS a variável referente à porta; o render define essa variável automaticamente;
* Depois de adicionar tudo certinho e clicar em "Save changes", o render já tentará deployar seu projeto novamente de forma automática;
* Se der tudo certo, você só precisa esperar alguns minutinhos e pronto, seu projeto já está deployado!
