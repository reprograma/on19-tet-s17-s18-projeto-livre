# On19-S17-S18-Projeto-Livre
Projeto Livre

## Voltei mis amoressssss
Ela mesma, Agnes Melo;
Porém, pro projeto final, né? quem tá ansiosa respirah;<br><br>
![bjork gritah](https://64.media.tumblr.com/e4ac84e95284f4abc15bfdd63bb89a1c/tumblr_ml4r2etFcA1rok2afo1_500.gifv)
<br><br>
Vamos fazer desse processinho o mais indolor e tranquilo possível? Então se liga nas 3 coisas que são importantes da gente prestar atenção nessas duas semanas:
* Vamos checar como estão as ideias e os códigos dos projetos para entender de onde partir. Esse é também um momento de acolhimento e troca entre nós;
* Na apresentação para a banca, precisamos mostrar nossas rotas no postman para as juradas virarem a cadeira;
* Também é preciso gerar a documentação da nossa API através do swagger;
* E por último, precisamos deployar nossa API no render pra que ela esteja acessível, cronicamente online, igual a senhora que passa sete horas no twitter por dia;

Parece bastante coisa, mas a gente vai juntas e vai dar tudo certo! (ou assim espero né mias lindas)
<br><br>
## Documentação no swagger
Esse tuto eu roubei da May (a maior que temos), viu gurias? Bora que bora documentar esse babadoh:
* Abro meu projeto
<br>
* Abro o terminal na raiz do projeto
<br>
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
<br>
Note que foi criado um arquivo chamado swagger_output.json dentro da nossa pasta swagger.
<br>
Parabéns, vc ja tem sua documentação!!!!
<br>
Bora deixar nossa documentaçao mais visual?
<br>
* Vamos lá no nosso app.js e adicionaremos o seguinte código:
```
    const swaggerUi = require('swagger-ui-express');

    const swaggerFile = require('../swagger/swagger_output.json');

    app.use('/minha-rota-de-documentacao', swaggerUi.serve, swaggerUi.setup(swaggerFile));
```
<br>
* Em seguida, inicializaremos nosso projeto, é so digitar no terminal:
```
$ npm start
```
* Feito isso, acessaremos a nossa rota
```
localhost:3000/minha-rota-de-documentacao
```

PS: Estou usando a porta 3000, caso vc esteja usando alguma diferente, use ela, beleza?

