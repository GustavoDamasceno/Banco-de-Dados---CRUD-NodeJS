# Banco de Dados - CRUD NodeJS

## Sumário

1. Ferramentas
2. Vamos começar a criar o sistema
3. Express
4. Operação Read
5. Parte visual do nosso projeto
6. Operação Create
7. MongoDB
8. Salvando nossos dados no banco
9. Mostrando o conteúdo do nosso Banco de dados
10. Operação Update - atualizando dados
11. Deletando dados

CRUD em NodeJS, vamos inserir os dados no nosso BD, mostrar em uma tabela para o usuário, editar os dados e deletar dados. Utilizando nodeJS, express e mongodb.

Antes de construir nosso sistema vamos ver uma breve definição das ferramentas que iremos utilizar.

![Alt Text](https://media.giphy.com/media/IPbS5R4fSUl5S/giphy.gif)

## 1.Ferramentas

* nodeJS
* express
* mongodb

### nodeJS

Pode ser definido como um ambiente de execução **Javascript server-side**. O que significa que com o **nodeJS** é possível criar aplicações Javascript para rodar como uma aplicação standalone em uma máquina, não dependendo de um browser para a execução. Seu objetivo é ajudar programadores na criação de aplicações de alta escabilidade, com códigos capazes de manipular dezenas de milhares de conexões simultâneas, numa única máquina física. O **nodeJS** é baseado ni interpretador V8 Javascript Engine (interpretador de Javascript open source implementado pelo Google em C++ e utilizado pelo Chrome). Foi criado em 2009, e seu desenvolvimento é mantido pela fundação **Node.JS** em parceria com a **Linux Foundation**.

### express

É um framework para construção de aplicações web para **nodeJS**. Ele simplifica o processo de criação do servidor que já está disponível no Node.

### mongodb

MongoDB é um dos mais populares de banco de dados. E disparado o mais famoso NoSQL no mercado. O mesmo é open-source e escrito em C ++. É um banco de dados orientado a documentos que armazena dados em documentos JSON com esquema dinâmico. Isso significa que você pode armazenar seus registros sem se preocupar com a estrutura de dados, como o número de campos ou tipos de campos para armazenar valores. Os documentos do MongoDB são semelhantes aos objetos JSON.

MongoDB é um **banco de dados multi-plataforma NoSQL**, que pode ser executado em Windows, Linux e Mac etc. Ele suporta linguagens de programação mais populares, como C #, Java, PHP, Javascript, NodeJs, Python e muito mais! 

## 2.Vamos começar a criar o sistema

Para poder criar nosso sistema, precisamos instalar o nodeJS. Basta clicar [aqui](https://www.hostinger.com.br/tutoriais/instalar-node-js-ubuntu/) para aprender a instalar o **nodeJS**.

Agora que já temos o **nodeJS**, vamos começar!

![Alt Text](https://media.giphy.com/media/p4NLw3I4U0idi/giphy.gif)

Bem, vamos lá. Crie uma pasta para o seu projeto e entre nela, depois abra a pasta do seu projeto na sua IDE, no meu caso é o **visual studio code**.

```
$ mkdir projeto
$ cd projeto
$ code .
```
Agora, dentro do nosso diretório vamos rodar o comando **npm init -y** o qual irá criar o **package.json**, arquivo que irá ajudar a gerenciar as dependências que instalaremos daqui a pouco.

```
$ npm init -y
```
Você vai perceber que na sua pasta surgiu um arquivo chamado **package.json**.
Bem, agora vamos criar nosso arquivo principal o **server.js** e dentro dele escreva o seguinte código:

```
console.log('Hello world');
```
Agora volte para o terminal e digite

```
$ node server.js
```
Você verá a mensagem **Hello world** no seu terminal, agora precisamos utilizar o express.

## 3.Express

Vamos começar fazendo a instalação do express:

```
$ npm install express --save
```
Feito isso você perceberá que o npm salvou o **express** como uma dependência no package.json
Você vai perceber que surgiu está linha dentro das dependências no arquivo package.json

```
"express": "^4.17.1" 
```
Agora precisamos colocar o express no nosso arquivo server.js. Para isso, a gente apaga aquele console.log() que tinhamos colocado para testar e coloca o código abaixo:

```
const express = require('express')
const app = express()
```
Precisamos fazer com que nosso servidor e o navegador possam se comunicar. Fazemos isso com a ajuda do metódo **listen** fornecido pelo Express:

```
app.listen(3000, function() {
    console.log('server running on port 3000')
})
```
Rodando no terminal o comando **node server.js**, vamos acessar o caminho localhost:3000 em nosso navegador.
O nome da aba será Error, e vai aparecer uma mensagem:

```
Cannot Get/
```
Isso significa que agora podemos nos comunicar com nosso servidor express através do navegador, agora vamos usar a operação Read.

## 4.Operação Read

Está operação é executada pelos navegadores sempre que você visita uma página da web. Ao ser iniciado os navegadores enviam uma solicitação **GET** ao servidor para executar uma operação de Leitura. A razão pela qual vemos o erro "cannot get/" é porque ainda temos que enviar algumas informações de volta para o navegador, que esteja vindo do nosso servidor.
Utilizando o **express**, essa solicitação é feita com o metódos **GET** e é adicionada da seguinte maneira: Vamos no nosso arquivo server.js e adicionar

```
app.get('/', (req, res) => {
    res.send('testando esse caralho');
});
```
Observe que estamos passando o caminho no qual o navegador está acessando que em nosso caso é o **localhost:3000/**, e para isso o primeiro argumento é "/". O segundo argumento é uma função callback que informa ao servidor o que fazer quando o caminho é correspondido. Esse callback leva dois argumentos, um objeto de solicitação (**req**) e outro de resposta (**res**). Bem, para gente testar estamos enviando uma frase 'testando esse caralho' com o método send para nos tazer o objeto de resposta.
Agora basta reiniciar o servidor e em seguida, acessar localhost:3000 no seu navegador.
Com isso, você deverá ver a mensagem 'testando esse caralho' no seu navegador.

## 5. Parte visual do nosso projeto

Vamos iniciar a parte visual do projeto, para isso iremos utilizar im template engine chamado **EJS** (Embedded Javascript), ele é bem simples de usa principalmente para quem já tem familiaridade com o html e javascript. Para instalar o ejs, basta digitar no seu terminal:

```
npm install ejs --save
```
Necessitamos configurar nossa view engine no Express, basta incluir o código abaixo no nosso arquivo server.js

```
app.set('view engine', 'ejs')
```
Pronto, agora vamos gerar o código HTML que será renderizado em nosso navegador. Vamos então criar nosso arquivo **index.ejs** dentro de uma pasta chamada 'views', Não vou esplicar essa parte html apenas vou disponibilizar o arquivo (até porque é bem simples). A estrutura da sua pasta projeto estará bem parecida com essa abaixo:

![](https://miro.medium.com/max/172/1*A7vhvRujAMfP9oH8ZrBOeg.png)

O conteúdo do arquivo ejs, será esse abaixo:

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>My CRUD in NodeJS</title>

        <style type="text/css">
          @import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";

          body{
              margin: 0;
              padding: 0;
              font-family: sans-serif;
              background: url(https://static1.squarespace.com/static/54f47ba4e4b0d786dd0fe615/571e0c7c2b8ddefbf16cce7a/5ab8c180352f53ed871f7e74/1523881085036/people_standing_fullscreen.jpg?format=2500w) no-repeat;
              background-size: cover;
          }

          .login-box{
              width: 280px;
              position: absolute;
              top: 50%;
              left: 50%;
              transform: translate(-50%, -50%);
              color: white;
          }

          .login-box h1{
              float: left;
              font-size: 40px;
              border-bottom: 6px solid #4caf50;
              margin-bottom: 50px;
              padding: 13px 0;
          }

          .textbox{
              width: 100%;
              overflow: hidden;
              font-size: 20px;
              padding: 8px 0;
              margin: 8px 0;
              border-bottom: 1px solid #4caf50;
          }

          .textbox i{
              width: 26px;
              float: left;
              text-align: center;
          }

          .textbox input{
              border: none;
              outline: none;
              background: none;
              color: white;
              font-size: 18px;
              width: 80%;
              float: left;
              margin: 0 10px;
          }

          .btn{
              width: 100%;
              background: none;
              border: 2px solid #4caf50;
              color: white;
              padding: 5px;
              font-size: 18px;
              cursor: pointer;
              margin: 12px 0;
          }

          .btn-2{
              width: 100%;
              background: none;
              border: 2px solid #4caf50;
              color: white;
              padding: 5px;
              font-size: 18px;
              cursor: pointer;
          }
        
        </style>
    </head>
    <body>

        <form class="login-box" action="/show" method="POST">
            <h1>Login</h1>
            
            <div class="textbox">
                <i class="fa fa-user" aria-hidden="true"></i>
                <input type="text" id="user" placeholder="Username" name="name" value=""><br>
            </div>
            <div class="textbox">
                <i class="fa fa-lock" aria-hidden="true"></i>
                <input type="password" id="senha" placeholder="Password" name="password" value=""><br>
            </div>
            
            <input id="btn-2" class="btn-2" type="submit" value="Register">
        </form>
        
    </body>
</html>

```
Você deve ter percebido que inseri o CSS  na tag style, não consegui inserir ele externamete usando o código:

```
< link rel="stylesheet" href="/app.css"> 
```
realmente, ele não reconhece... Aí, coloquei direto no mei arquivo.ejs. Mas, se você conseguir o código ficará um pouco mais bonito!

Bem, agora a gente precisa setar nosso arquivo para que ele seja enviado para o servidor, e ser renderizado no navegador. Para isso precisamos fazer uma alteração no trecho de códgip app.get(). Ficará dessa forma:

```
app.set('view engine', 'ejs');

app.get('/', (req, res) => {
    res.render('index.ejs');
});

```

Agora basta a gente reiniciar o nosso servidor. Quando você abrir a página no seu navegador (**localhost:3000**) você verá o resultado, como o de baixo:

![](https://i.stack.imgur.com/HPGsH.png)


## 6. Operação Create

A operação Create é executada apenas pelo navegador se uma solicitação **Post** for enviada ao servidor. Essa solicitação pode ser acionada com Javascript ou por meio de um elemento <form>.

Bem, precisamos ter três coisa neste elemento de formulário:
Um atributo **action**, um atributo **method** e um atributo **name** para todo elemento <input> do formulário.

Já está implementado, basta olhar o arquivo **index.ejs** que coloquei aí em cima.

O atributo **action** informa ao navegador para onde redirecionar nosso app Express. Nesse caso estamos sendo direcionados para /show. O atributro **method** informa ao navegador qual solicitação enviar, nesse caso é uma solicitação do tipo **POST**.

No nosso servidor, podemos processar essa solicitação Post com um método post fornecido pelo Express que leva os mesmos argumentos GET:

```
app.post('/show', (req, res) => {
    console.log('Testando essa porra aqui')
    })
```
Após isso, salve as alterações. reinicie o servidor... Você poderá ver em seu terminal a seguinte mensagem: "Testando essa porra aqui".
Bem, agora sabemos que o Express está lidando direito com o formulário. Mas,acontece que o express não lida com a leitura de dados do elemento <form> por conta própria. Temos que adicionar outro pacote chamado **body-parser** para conseguir essa funcionalidade, pare o servidor e digite em seu terminal o seguinte comando:

```
npm install body-parser --save 
```
O express nos permite adicionar middleware como body-parser ao nosso aplicativo com o método **use**. Vamos então incluir o body-parser em seu arquivo.js, ficará assim:

```
const express = require('express');
const bodyParser = require('body-parser');
const app = express();

app.use(bodyParser.urlencoded({ extended: true})); 

```
O método **urlencoded** dentro de body-parser diz ao body-parser para extrair dados do elemento <form> e adicioná-los à propriedade body no objeto request. Vamos testar, dê um console.log() e preencha o formulário, você deverá ver tudo no campo de formulário dentro do objeto:

```
app.post('/show', (req, res) => {
    console.log(req.body)
    }) 
```
Então, reinicie o servidor e você verá em seu trminal algo parecido com isto:

```
server running on port 3000
{ name: 'gustavo', password: 'gd1527'} 
```

## 7. MongoDB

Para usarmos o **MongoDB** como banco de dados, nós precisamos instalá-lo e podemos fazer isso através do npm, com o comando abaixo:

```
npm install mongodb --save 
```
Depois de instalado, podemos nos conectar ao MongoDB através do método de conexão do **Mongo.Client**, conforme mostrado no código abaixo:

```
const MongoClient = require('mongodb').MongoClient 
const uri = "<!-- insira aqui o caminho para seu BD -->"
MongoClient.connect(uri, (err, client) => {
  // ... start the server
})

```
Relaxa, o código acima a gente vai implementar mais adiante. Neste projeto utilizei o mlab (atualmente ele está direcionando para o atlas... Mas, é só seguir os passos do site), crie uma conta no [site](https://mlab.com/) deles, é fácil e gratuito. Após verificar sua conta, você pode criar um usuário.. **Vai seguinto o tutorial do site!** Quando terminar, entre na aba Users e crie um usuário e uma senha paa o banco de dados, você vai usar esses dados para conectar ao banco que vocçe acabou de criar.

Depois, pegue o url do MongoDB e adicione-o ao seu método MongoClient.connect. Certifique-se de usar seu usuário e senha do banco de dados. Em seguida, queremos iniciar nosso servidor apenas quando o banco de dados estiver conectado. Por isso, vamos mover o **app.listen** para o método connect. Lembra daquele código de conexão? que eu até disse Realaxa? Vamos implementá-lo agora.

```
const MongoClient = require('mongodb').MongoClient;

const uri = "mongodb+srv://dazzle:palmeiras@cluster0-str4z.mongodb.net/test?retryWrites=true&w=majority";

MongoClient.connect(uri, (err, client) => {
    if(err) return console.log(err)
    db = client.db('basedata'); //nome do meu data base

    app.listen(3000, () => {
        console.log('Server running on port 3000');
    });
});

```
Bem, acabamos de onfigurar o MongoDB. Agora, vamos criar uma coleçao (lá no site) para armazenar os dados do nosso projeto. Uma coleção é um local nomeado para armazenar ojetos, você pode criar quantas coleções quiser. Podemos armazena ojetos como "nomes", "password", ou qualquer outra nomenclatura que quiser. Agora vamos inicar as operações do CRUD.


## 8. Salvando nossos dados no banco

Iremos criar a coleção “data”, que irá armazenar nossos dados, apenas colocando-a entre aspas ao chamar o método db.collection() do MongoDB. Ao criar a coleção, também podemos salvar nossa primeira entrada no MongoDB com o método save simultaneamente.

Quando terminarmos de salvar, precisamos redirecionar o usuário para algum lugar (senão o usuário ficará esperando para sempre até que nosso servidor seja alterado). Nesse caso, vamos redirecioná-los de volta para /, o que faz com que os navegadores sejam recarregados.

```
app.post('/show', (req, res) => {
    db.collection('data').save(req.body, (err, result) => {
        if(err) return console.log(err)

        console.log('salvo no banco de dados');
        res.redirect('/');
    });
});

```

Agora, se você inserir algo no elemento <form>, poderá ver uma entrada na sua coleção do MongoDB e a confirmação através do seu terminal.

TOP D++ né?

![Alt Text](https://media.giphy.com/media/8mgQWF7hk5m3XDj3pM/giphy.gif)

já temos algum conteúdo no banco de dados, por que não tentar mostrar ao usuário quando eles chegarem à nossa página?

## 9. Mostrando o conteúdo do nosso Banco de dados

Temos que fazer algumas coisas para mostrar o conteúdo armazenado em nosso banco de dados para o nosso usuário. Precisamos: Pegar o conteúdo no banco de dados e usar nossa template engine para exibir esse conteúdo.

Podemos obter o conteúdo do nosso Banco de Dados usando o método **find** disponível no método collectio.

```
app.get('/', (req, res) => {
    var cursor = db.collection('data').find()
})
```
O método de localização retorna um cursor(um objeto do Mongo), este objeto contém todas as citações de nosso banco de dados. Ele também contém várias outras propriedades e métodos que nos permitem trabalhar com dados facilmente. Um desses métodos é o método **toArray**.

O método **toArray** recebe uma função callback que nos permite fazer algumas coisas com os objetos que recuperamos do mLab. Vamos tentar fazer um **console.log()** nesses resultados e ver o que conseguimos!

```
app.post('/show', (req, res) => {
    db.collection('data').save(req.body, (err, result) => {
        if(err) return console.log(err)

        console.log('salvo no banco de dados');
        res.redirect('/');
        db.collection('data').find().toArray((err, results) => {
            console.log(results);
        })
    });
});

```
Após incluir o trecho acima, vá até seu navegador e preencha o <form> e clique em register . Você verá o resultado em seu terminal.

```
server running on port 3000
salvo no banco de dados
[ { _id:5b174d4443634722ac83c48b,
    name: 'Gustavo',
    password: '151098' } ]

```
Ótimo! Você está vendo o conteúdo preenchido (o mesmo que foi salvo no banco de dados). Concluímos a primeira parte, que é obter dados do MongoLab. A próxima parte será renderizar esse conteúdo usando nossa **template engine**. Bom, para isso crie um novo arquivo dentro da pasta ‘views’, vou chamar de **show.ejs**.

Agora abra-o e crie uma tabela que mostre o conteúdo que enviamos pelo formulário.

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>My CRUD in NodeJS</title>
</head>
<body>

<h2>Registros<h2>
    <table border="1">
        <thead>
            <tr>
                <td>Nome</td>
                <td>Password</td>
            </tr>
        </thead>
        <tbody>
        <% data.forEach(function(details) { %>
            <tr>
                <td><%= details.name %></td>
                <td><%= details.password %></td>
            </tr>
            <% }) %>
        </tbody>
        <button><a href="/">Voltar</a></button>
</body>
</html>

```

nós estamos mostrando nossa variável data combinada com o método .forEach() onde irá percorrer o conteúdo da collection em nosso banco de dados, e criamos então a function(details) que nas linhas 20 e 21, irá mostrar o conteúdo que estamos chamando com **<%= details.name%>** e **<%= details.surname%>** respectivamente.

Em seguida faça uma pequena alteração no server.js. Deixe conforme abaixo:

```
const express = require('express');
const bodyParser = require('body-parser');
const app = express();

const MongoClient = require('mongodb').MongoClient;

const uri = "mongodb+srv://dazzle:palmeiras@cluster0-str4z.mongodb.net/test?retryWrites=true&w=majority";

MongoClient.connect(uri, (err, client) => {
    if(err) return console.log(err)
    db = client.db('basedata'); //nome do meu data base

    app.listen(3000, () => {
        console.log('Server running on port 3000');
    });
});

app.use(bodyParser.urlencoded({ extended: true}));

app.set('view engine', 'ejs');

app.get('/', (req, res) => {
    res.render('index.ejs');
});

app.get('/', (req, res) => {
    var cursor = db.collection('data').find()
})

app.get('/show', (req, res) => {
    db.collection('data').find().toArray((err, results) => {
        if (err) return console.log(err)
        res.render('show.ejs', { data: results })

    })
})

app.post('/show', (req, res) => {
    db.collection('data').save(req.body, (err, result) => {
        if(err) return console.log(err)

        console.log('salvo no banco de dados');
        res.redirect('/show');
        
    });
});

```
Volte ao navegador e preencha o formulário, você será redirecionado para a página **localhost:3000/show** , e verá o conteúdo.

## 10. Operação Update - atualizando dados

A operação UPDATE é usada quando você quer alterar algum conteúdo no banco de dados.

Note que incluí os buttons no arquivo show.ejs onde irá direcionar para a página de edit, e incluí também o de delete, o qual será nossa próxima etapa do CRUD. Usei também um CSS na tabela, caso você ainda não saiba como funciona uma tabela, acesse esse site [aqui](http://www.devfuria.com.br/html-css/tabelas/), gostei bastante das informações.

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>My CRUD in NodeJS</title>
  <style>
     body{
        margin: 0;
        padding: 0;
        font-family: sans-serif;
        background: url(https://www.wallpaperup.com/uploads/wallpapers/2012/09/22/15991/1bc49bcd7b4d4d6ee6d405f46c8087de.jpg) repeat;
        background-size: cover;
      }

     button.css3button {
        background: #009879;
        background-image: -webkit-linear-gradient(top, #009879, #009879);
        background-image: -moz-linear-gradient(top, #009879, #009879);
        background-image: -ms-linear-gradient(top, #009879, #009879);
        background-image: -o-linear-gradient(top, #009879, #009879);
        background-image: linear-gradient(to bottom, #009879, #009879);
        -webkit-border-radius: 28;
        -moz-border-radius: 28;
        border-radius: 28px;
        font-family: Arial;
        color: #FFFF;
        font-size: 20px;
        padding: 10px 20px 10px 20px;
        text-decoration: none;
        }
    
     button.css3button:hover {
        background: #009879;
        background-image: -webkit-linear-gradient(top, #009879, #009879);
        background-image: -moz-linear-gradient(top, #009879, #009879);
        background-image: -ms-linear-gradient(top, #009879, #009879);
        background-image: -o-linear-gradient(top, #009879, #009879);
        background-image: linear-gradient(to bottom, #009879, #009879);
        text-decoration: none;
      }

      h1{
        font-weight: bold;
        text-align: center;
        color: #009879;
      }
      .content-table{
          width: 880px;
          position: absolute;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%);
          color: white;
          border-collapse: collapse;
          margin: 25px 0;
          font-size: 0.9cm;
          min-width: 400px;
          border-radius: 5px 5px 0 0;
          overflow: hidden;
          box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
      }

      .content-table thead tr{
          background-color: #009879;
          color: #ffffff;
          text-align: left;
          font-weight: bold;  
      }

      .content-table th,
      .content-table td {
          padding: 12px 15px;
      }

      .content-table tbody tr{
          border-bottom: 1px solid #dddddd;
      }

      .content-table tbody tr:nth-of-type(even){
          background-color: #f3f3f3;
      }

      .content-table tbody tr:last-of-type{
          border-bottom: 2px solid #009879;
      }

      .content-table tbody tr.active-row{
          font-weight: bold;
          color: #009879;
      }

  </style>

</head>
<body>

<h1>Banco de Dados<h1>
    <table class="content-table">
        <thead>
            <tr>
                <td>Nome</td>
                <td>Password</td>
                <td>Ação</td>
            </tr>
        </thead>
        <tbody>
        <% data.forEach(function(details) { %>
            <tr class="active-row">
                <td><%= details.name %></td>
                <td><%= details.password %></td>
                <td><a href="/edit/<%= details._id %>">Editar</a> - <a href="/delete/<%= details._id %>">Deletar</a></td>
            </tr>
            <% }) %>
        </tbody>
        <button type="button" name="" value="" class="css3button"><a href="/"> Voltar </a></button>
</body>
</html>

```

Então antes de avançar vamos ver como está ficando o nosso projeto! Quando você abrir o navegador em localhost:3000 irá visualizar o seguinte:

![](https://pbs.twimg.com/media/EA3ELiWXsAAh7sE?format=jpg&name=large)

Depois de preencher os dados e apertar no botão register, as informações irão para o banco de dados:

![](https://pbs.twimg.com/media/EA3ELiWX4AA2tce?format=jpg&name=large)

Depois esses dados serão pegos e mostrado na nossa tabela, além disso terá um botão voltar a tela de registro dos dados:

![](https://pbs.twimg.com/media/EA3ELiWXYAIz5aq?format=jpg&name=large)

Vamos retomar o desenvolvimento do nosso projeto. Vamos fazer um **Post** na rota **/edit/:id** e irei tratar essa atualização conforme abaixo. Note que fiz algumas alterações na estrutura do projeto, aproveitando um recurso de rotas que o **Express()** nos oferece.

Veja abaixo que, com o recurso de rotas fornecido, podemos apenas indicar qual a rota iremos observar e dentro dessa rota, teremos os métodos abaixo.

No método **.get**, estou armazenando em **var id**, o id que iremos passar no **params** vindo da **view** (faremos primeiro nossos métodos no servidor, e depois a view), estou usando essa variável para encontrar o objeto que iremos alterar, isso está sendo feito na função **.find(Object(id))** que irá percorrer o array em nosso banco, e quando encontrar o nosso objeto, irá renderizar a nossa **view edit.ejs** e também passando o resultado desse objeto para ser usado com os valores dentro do <form> em nossa view.

abra seu arquivo server.js e adicione:

```
app.route('/edit/:id')
.get((req, res) => {
    var id = req.params.id
    var ObjectId = require('mongodb').ObjectId;

    db.collection('data').find(ObjectId(id)).toArray((err, result) => {
        if(err) return res.send(err)
        res.render('edit.ejs', {data: result})
    })
})

.post ((req, res) => {
    var id = req.params.id
    var name = req.body.name
    var password = req.body.password
    var ObjectId = require('mongodb').ObjectId;

    db.collection('data').updateOne({_id: ObjectId(id)}, {
        $set: {
            name: name,
            password: password
        }
    }, (err, result) => {
        if(err) return res.send(err)
        res.redirect('/show')
        console.log('Atualizando no Banco de Dados')
    })
})
```
Criei um novo arquivo dentro da pasta views, com o nome edit.ejs. Nele há um formulário parecido com o que temos no index.ejs, porém, ao invés de incluir um novo “nome” e “password”, iremos alterar o valor já existente. Note que incluí um botão para voltar aos registros salvos, e outro que fará o post para editar nosso objeto, veja que já estou importando os dados que está sendo renderizado conforme imagem acima. Note também que estou passando o id do objeto no params, e já estou usando os valores da nossa base de dados dentro do input para melhor visualização do dado que estamos editando.

arquivo edit,ejs. logo abaixo:

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>My CRUD in NodeJS</title>

        <style type="text/css">
          @import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";

          body{
              margin: 0;
              padding: 0;
              font-family: sans-serif;
              background: url(https://static1.squarespace.com/static/54f47ba4e4b0d786dd0fe615/571e0c7c2b8ddefbf16cce7a/5ab8c180352f53ed871f7e74/1523881085036/people_standing_fullscreen.jpg?format=2500w) no-repeat;
              background-size: cover;
          }

          .login-box{
              width: 280px;
              position: absolute;
              top: 50%;
              left: 50%;
              transform: translate(-50%, -50%);
              color: white;
          }

          .login-box h1{
              float: left;
              font-size: 40px;
              border-bottom: 6px solid #4caf50;
              margin-bottom: 50px;
              padding: 13px 0;
          }

          .textbox{
              width: 100%;
              overflow: hidden;
              font-size: 20px;
              padding: 8px 0;
              margin: 8px 0;
              border-bottom: 1px solid #4caf50;
          }

          .textbox i{
              width: 26px;
              float: left;
              text-align: center;
          }

          .textbox input{
              border: none;
              outline: none;
              background: none;
              color: white;
              font-size: 18px;
              width: 80%;
              float: left;
              margin: 0 10px;
          }

          .btn{
              width: 100%;
              background: none;
              border: 2px solid #4caf50;
              color: white;
              padding: 5px;
              font-size: 18px;
              cursor: pointer;
              margin: 12px 0;
          }

          .btn-2{
              width: 100%;
              background: none;
              border: 2px solid #4caf50;
              color: white;
              padding: 5px;
              font-size: 18px;
              cursor: pointer;
          }
        
        </style>
    </head>
    <body>
          <% data.forEach(function(details) { %>
            <form class="login-box" action="/show" method="POST">
                <h1>Editar</h1>
                
                <div class="textbox">
                    <i class="fa fa-user" aria-hidden="true"></i>
                    <input type="text" id="user" placeholder="Username" name="name" value="<%= details.name %>"><br>
                </div>
                <div class="textbox">
                    <i class="fa fa-lock" aria-hidden="true"></i>
                    <input type="password" id="senha" placeholder="Password" name="password" value="<%= details.password %>"><br>
                </div>
                
                <input id="btn" class="btn" href='/show' value="Todos">
                <input id="btn-2" class="btn-2" type="submit" value="Editar">
            </form>
           <% }) %>
        
    </body>
</html>
 
```

Voltando ao nosso código de update pouco mais acima, note que quando fazemos um .post o nosso server irá armazenar as variáveis que iremos usar para dar update em nosso objeto, updateOne() recebe o nosso objeto que estamos alterando, e $set recebe os dados do form que queremos atualizar, se tudo estiver correto, seremos redirecionado para a tela onde mostra todos nossos registros, e estamos printando em nosso console a informação de “Atualizado no banco de dados”.

## 11. Deletando dados

A operação DELETE é a última operação desse nosso projeto, após ter feito corretamente o UPDATE, e tendo adquirido esse conhecimento, você verá que o método .delete é bem simples. Lembra que fizemos o botão de “Deletar” em nossa página **/show**? Pois é, já estamos enviando o id que iremos apagar do nosso BD, então será simples fazer esse tratamento.

```
app.route('/delete/:id')
.get((req, res) => {
  var id = req.params.id

  db.collection('data').deleteOne({_id: ObjectId(id)}, (err, result) => {
    if (err) return res.send(500, err)
    console.log('Deletado do Banco de Dados!')
    res.redirect('/show')
  })
})
```

Note que quando clicar no botão de deletar, seremos direcionados para /delete/:id e então, com o método .get iremos pegar e armazenar o id enviado, e da mesma forma que o updateOne, estamos passsando o id a ser buscado em nosso BD e então deletá-lo, printamos em nosso console a informação de deletado e seremos redirecionados para a tela de registros.

Feito isso, encerramos nosso projeto de CRUD Simples em NodeJS.

![Alt Text](https://media.giphy.com/media/3oxHQqbAXz5W6GpHSE/giphy.gif)

