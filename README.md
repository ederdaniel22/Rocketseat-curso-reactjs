Iniciamos o projeto com: 
## yarn init -y

Instalamos o React com: 
## yarn add react

instalamos o react-dom com: 
## yarn add react-dom.

Criamos a pasta src com os arquivos index.jsx e App.jsx

instalamos o babel com: 
## yarn add @babel/core @babel/cli @babel/preset-env
usando o babel criamos o dist/bundle.js com o comando 
## yarn babel src/index.jsx --out-file dist/bundle.js
na raiz do projeto criamos e configuramos o babel.config.js 

Instalamos o webpack com: 
## yarn add webpack webpack-cli  
E na raiz criamos o arquivo webpack.config.js

criamos a pasta public e nela o arquivo index.html

## para rodar o projeto usamos yarn webpack

para o browser enxergar o javascrit do html:
instalamos webpack-plugin com: 
## yarn add html-webpack-pluggin -D

fizemos a importação da extensão no wepack.config.js com:
## const HtmlWebpackPlugin = require('html-webpack-plugin)
Atualizamos o webpack.config.js

Instalamos o weback server com: 
## yarn add webpack-dev-server -D
atualizamos as configurações no webpack config com a linha abaixo do resolve
## devServer: {
##    contentBase: path.resolve(__dirname, 'public')
##    },
essa configuração vai automatizar a reinicialização

Para rodar o projeto a partir dessa configuração usamos
## yarn webpack serve

Configurar o source-map no webpack.config.js para visualizar erros na aplicação
no module.exports abaixo do mode devlopment inserir:
## devtool: 'eval-source-map',

Criar a variável NODE_ENV com:
## NODE_ENV=production yarn webpack

Instalar o CrossEnv
## yarn add cross-env -D

criar no package json os scripts
## "scripts":{
##    "dev": "webpack serve",
##    "build": "cross-env NODE_ENV=production webpack"
##  },

A partir desse momento para rodar o projeto usamos 
## yarn dev

Criar pasta styles e dentro dela o arquivivo:
## global.css

criar no webpack.config.js mais um rules para que o projeto entenda css também
Retirar deste rules o babel loader, instalar as dependências 
## yarn add style-loader css-loader -D
depois inserir a linha:
## use: ['style-loader', 'css-loader', 'sass-loader']

Atualizamos a aplicação instalando o sass
## yarn add node-sass -D
## yarn add sass-loader D

Primeiro componente, criar na pasta src uma pasta chamada components, para armazenar nossos componentes individualmente
## raiz/src/components 
dentro dela criar o arquivo ou componente:
## NomeDoArquivo.jsx
criar a função e fazer a exportação com o nome do arquivo
dentro da função criada fazer o return com o conteúdo a ser utilizado no componente
## export function NomeDoArquivo(){
##  return(
##    <section className="NomeDoArquivo-list">
      
##    </section>
##  );
## }

Fazer a importação do componente dentro do return do App principal, para ser renderizado no browser
## import { RepositoryList } from './components/RepositoryList'
## import './styles/global.scss'
## export function App(){
##    return <RepositoryList />
## }

Criar um novo componente chamado RepositoryItem
## RepositoryItem.jsx
esse componente vai individualizar cada item da lista de repositorios e poderá ser importado no RepositoryList dentro
da <ul> como componente quantas vezes for nrcessário, dentro do RepositoryList podemos atualizar as propriedas do
componente agregando a ele propriedades diferentes do original, essas propriedades srão recebidas como props no 
componente pai ou seja no RepositoryItem

<!-- CRIAÇÃO
export function RepositoryItem(){
  return(
    <li>
          <strong>unform</strong>
          
          <p>Forms in React</p>

          <a href="">
            Acessar repositórios
          </a>
        </li>
  );
} -->

<!-- 
IMPORTAÇÃO
import { RepositoryItem } from "../RepositoryItem";

export function RepositoryList() {
  return (
  

    <section className="repository-list">

      <h1>Lista de repositórios</h1>
      
      UTILIZAÇÃO
      <ul>
        <RepositoryItem />        
        <RepositoryItem />        
        <RepositoryItem />        
        <RepositoryItem />        
        <RepositoryItem />        
      </ul>
    </section>
  );
} -->
Em cada componente desses podemos enviar novas propriedades ao componente pai
## <RepositoryItem repository="unform2">

E no componente pai recebemos as propriedades como argumento da função e renderizamos dentro da função como código JS
<!-- ## export function RepositoryItem(props){
  return <li>
          <strong>{props.repository}</strong>

          <p>Forms in React</p>

          <a href="">
            Acessar repositórios
          </a>
        </li>
} -->

Para testar se o componente estiver sem propriedades no componente pai digitamos 
## <strong>{props.repository ?? 'Default'}</strong>
Neste caso se o repositório tiver conteúdo vai renderizar o conteúdo, senão, vai renderizar o Default

Para incluirmos mais propriedade no componente filho digitamos
## <RepositoryItem repository="unform2" description="Forms in React" link="https://github.com/unform/unform"/>
Essas propridades serão recebidas no componente pai também como (props), porém como são várias propriedades, mas que serão usadas apenas
pelo componente pai, podemos criar uma contante com uma descrição e associarmos ao componente pai.
<!-- 
NOVO FORMATO
import { RepositoryItem } from "../RepositoryItem";

CRIAÇÃO DAS PROPRIEDADES
const repository = {
  name: 'unform',
  description: 'Forms in React',
  link: 'https://github.com/unform/unform'
}

export function RepositoryList() {
  return (
    <section className="repository-list">

      <h1>Lista de repositórios</h1>
      
      <ul>
        <RepositoryItem repository={repository}/>        
        <RepositoryItem repository={repository}/>        
        <RepositoryItem repository={repository}/>        
        <RepositoryItem repository={repository}/>        
        <RepositoryItem repository={repository}/>   
      </ul>
    </section>
  );
} 

REPOSITORY ITEM
export function RepositoryItem(props){
  return(
    <li>
          <strong>{props.repository.name ?? 'Default'}</strong>

          <p>{props.repository.description}</p>

          <a href={props.repository.link}>
            Acessar repositórios
          </a>
        </li>
  );
}
-->

Conceito de Estado.
Componente teste
Counter

import { usestate } from 'react;

export function Counter(){
  const [counter, setcounter] = useState(0);

  function increment(){
    setCounter(counter + 1);
  }
  return(
    <div>
      <h2{counter}></h2>
      <button type="button" onClick={increment}>
      Increment
      </button>
    </div>
  );
}

Para renderizar importá-lo no app
## import { Counter } from './components/Counter'
E integrá-lo na função
## <Counter />

Atualizado até aula de Estado de componente
Inicializando com:
## yarn dev

IMUTABILIDADE: CONCEITO => Uma variável nunca poderá ser mudada, ela poderá receber novos valores em uma outra variável, 
mas a principal não será alterada