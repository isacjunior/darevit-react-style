<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSuaawjDg0AH5TQlE6ToM4VmCJMkL0P44sFHjtPNhi2rXgWH0HFFw" width="127px" height="127px" align="left"/>

# Darevit React Style Guide
Este guia de estilo é baseado principalmente nos padrões que prevalecem atualmente em React/Airbnb.

<br>

## React and Javascript Style Guide

Este guia contém algumas práticas considero ser adequada a se usar em um projeto React. Esse estilo é baseado no [Airbnb's](https://github.com/airbnb/javascript) com algumas modificações.

## Objetivo

Qual o propósito de utilizarmos um Style Guide?
O principal objectivo é mantermos uma única forma de escrita, porém também ganhamos:

  - Melhor Legibilidade de código
  - Melhor manutenção do código
  - Ganho de tempo em code reviews
  - Entre outros grandes benefícios

## Rules
### Extensão de componentes React
- Ao criar um arquivo, em que ele ir utilizar a sintaxe jsx, é indicado que se use a extensão `.jsx`

```
Button/
├── index.jsx
```
### Criação de componentes com folha de stilo
- Quando necessário criar um componete que terá estilos, sempre optar por styled-components, e com a seguinte estrutura:

```
Button/
├── index.jsx
└── styled.js
```

### Importando Component
- Sempre que for extender uma classe com Component ou PureComponent, faça a destruturação na importação.
```Javascript
// Bad
import React from 'react'
class Classe extends React.Component

// Good
import React, { Component } from 'react'
class Classe extends Component
```

### Criação de Classes
```Javascript
// Very Bad
import React from 'react'
const Classe = React.createClass({
  render() {
    ....
  }
})

// Bad
import React from 'react'
class Classe extends React.Component {
  render() {
    ....
  }
}

// Good
import React, { Component } from 'react'
class Classe extends Component {
  render() {
    ....
  }
}
```

### Stateless Component 
- Prefira utilizar a sintaxe funcional para componentes sem estado e em components.
```Javascript
const Title = (props) => (
  <h1>{props.title}</h1>
)
```

### Stateful Component 
- Prefira utilizar a sintaxe de classes para componentes que possuem conhecimento do estado, em container e componentes que utilizem lifecycles.
```Javascript
class Title extends Component {
  render () {
    return (
      ....
    )
  }
}
```

### State 
- Caso seja necessário criar um estado local na sua classe, prefira:
```Javascript
// Bad
class ThemeProvider extends Component {
  componentWillMount() {
    this.state = {
      color: '#FFFFFF',
    }
  }
}

// God
class ThemeProvider extends Component {
  constructor() {
    super()
    this.state = {
      color: '#FFFFFF',
    }
  }
}

// Best
class ThemeProvider extends Component {
  state = {
    color: '#FFFFFF',
  }
}
```

### Falta de vírgula no último elmento do objeto
- Na utilização de objetos, sempre adicione vírgula no último element, isso ir auxiliar na visualização do git diff, caso haja adição de um novo elemento na última posição.
```Javascript
// Bad
export {
  Provider,
  Consumer
}

// Good 
export {
  Provider,
  Consumer,
}
```

### Arrow function
- Sempre prefira escrever funções com arrow function, principamente se o retorno couber apenas em uma linha, e quando houver callbacks com funções anônimas.
```Javascript
// Very Bad
function double(array) {
  return array.map(function(item) {
    return item * 2
  })
}

// Good
function double(array) {
  return array.map(item => item * 2)
}

// Best
const double = array => array.map(item => item * 2)
```

### Setando uma variável
- Sempre que possível, utilize const na inicialização de qualquer variável.
```Javascript
// Bad
var a = 1

// Good
const a = 1
```

### Template Strings
- Dê preferência ao uso de template strings na concatenação de strings.
```Javascript
// Bad
const person = {
  name: 'Isac'
}
const myName = "My name is "+ person.name+"."

// God
const person = {
  name: 'Isac'
}
const myName = `My name is ${person.name}.` 
```

### Ponto e vírgula
```Javascript
// Bad
import React from 'react';

// Good
import React from 'react'
```

### Console.log
- Nunca deixe console.log() em seu código
```Javascript
// Bad
const sum = (a, b) => {
  const result = a + b
  console.log(result)
}
```

### Comentários
- Nunca deixa comentários em seu código
```Javascript
// Bad
// Função que soma dois elementos
const sum = (a, b) => a + b

// Good
const sum = (a, b) => a + b
```

### Retorno de elementos com JSX
- Caso seja possível, prefira omitir `return` 
```Javascript
// Bad
const Bonus = () => {
  return (
    <div>
      <h1>Darevit Style Guide</h1>
    </div>
  )
}

// Good
const Bonus = () => (
  <div>
    <h1>Darevit Style Guide</h1>
  </div>
)
```

### Destruturação de objetos
- Sempre que possível, utilize destruturação de objetos
```Javascript
// Bad
const Title = (props) => (
  <h1>{props.title}</h1>
)

// Good
const Title = ({ title }) => (
  <h1>{title}</h1>
)
```

### Exportação default
- Caso o seu arquivo contenha somente um elemento a ser exportado, prefira `export default`
```Javascript
class ClasseNameA extends Component {
  render() {
    ....
  }
}

export default ClasseNameA
```

### Englobar elementos em JSX
- Sempre que retornamos um elemento JSX, é de nosso conhecimento, que é necessário envolver em um elemento pai. Caso esteja utilizando versão superior a React 16.2, prefira `Fragment`, ou sintaxe curta de Fragment.
```Javascript
// Bad
import React from 'react'

const NameA = () => (
  <div>
    ....
  </div>
)

// Good
import React, { Fragment } from 'react'

const NameA = () => (
  <Fragment>
    ....
  </Fragment>
)

// Best
import React, { Fragment } from 'react'

const NameA = () => (
  <>
    ....
  </>
)
```

### Repassando props
- Caso haja a necessidade de repassar props para outros componentes, prefira nomear as props. Isso irá facilitar o entendimento do fluxo, e quais props esto sendo utilizadas. Evitando a passagem desnecessárias de outras props.
```Javascript
// Bad
const Button = props => (
  <StyledButton {...props}>
    {props.children}
  </StyledButton>
)

// Good
const Button = ({ primary, children }) => (
  <StyledButton color={primary}>
    {children}
  </StyledButton>
)
```

### Bind em métodos
- Caso esteja sendo necessário criar bind para o contexto this, prefira utilizar métodos com arrow function.
```Javascript
// Bad
class MyComponent extends Component {
  constructor() {
    super()
    this.methodA = this.methodA.bind(this)
  }

  methodA() { ... }
}

// Good
class MyComponent extends Component {
  methodA = () => { ... }
}
```

### Inicializando State
- React > 16.3: Não utilize componentWillMount para iniciar o seu state
```Javascript
// Bad
class MyComponent extends Component {
  componentWillMount() {
    this.setState({
      currentColor: this.props.defaultColor,
      palette: 'rgb'
    })
  }
}

// Good
class MyComponent extends Component {
  state = {
    currentColor: this.props.defaultColor,
    palette: 'rgb'
  }
}
```

### ComponentWillMount
- React > 16.3: Sempre prefira o uso do `componetDidMount` ao invez do `componentWillMount`, o mesmo será descontinuado na versão 17.
```Javascript
// Bad
class MyComponent extends Component {
  componentWillMount() {
    ...
  }
}
// Good 
class MyComponent extends Component {
  componentDidMount() {
    ...
  }
}
```

### ComponentWillReceiveProps
- React > 16.3: Este é um exemplo de verificação de props para atualização do estado. Sempre que se deparar com tal situação, utilize `getDerivedStateFromProps` para realizar tal operação. `ComponentWillReceiveProps` será descontinuado na versão 17.
```Javascript
// Bad
class ExampleComponent extends Component {
  state = {
    isScrollingDown: false
  };

  componentWillReceiveProps(nextProps) {
    if (this.props.currentRow !== nextProps.currentRow) {
      this.setState({
        isScrollingDown:
          nextProps.currentRow > this.props.currentRow
      })
    }
  }
}

// Good
class ExampleComponent extends Component {
  state = {
    isScrollingDown: false,
    lastRow: null
  }

  getDerivedStateFromProps(nextProps, prevState) {
    if (nextProps.currentRow !== prevState.lastRow) {
      return {
        isScrollingDown:
          nextProps.currentRow > prevState.lastRow,
        lastRow: nextProps.currentRow
      }
    }
    return null
  }
}

```

### ComponentWillUpdate
- React > 16.3: Caso queira executar alguma ação após o componente receber alguma chamada externa, prefira o uso de `componentDidUpdate`, pois `componentWillUpdate` será descontinuado na versão 17.
```Javascript
// Bad 
class ExampleComponent extends Component {
  componentWillUpdate(nextProps, nextState) {
    if (this.state.someStatefulValue !== nextState.someStatefulValue) {
      nextProps.onChange(nextState.someStatefulValue);
    }
  }
}

// Good 
class ExampleComponent extends Component {
  componentDidUpdate(prevProps, prevState) {
    if (this.state.someStatefulValue !== prevState.someStatefulValue) {
      this.props.onChange(this.state.someStatefulValue)
    }
  }
}
```

### Component ou PureComponent
- `PureComponent` é similar ao Component. A diferença está em no `shouldComponentUpdate()`. Em PureComponent isto é feito de forma superficial no estado e props. Utilize PureComponent somente em casos em que você saiba exatamente a estrutura das propriedades que irão ser recebidas pelo component. Em alguns casos, onde o seu componente sempre irá renderizar uma mesma estrutura, você poderá utilizá-lo para ganhar performance.
Mais informações você poderá encontrar na documentação do React.

### Valores padrões em parâmetros
- Sempre que possível, crie valores padrões nos parâmetros da sua função

```Javascript
// Bad
const getPrice = (amount, scale, currency) => {
  return priceNormalize(parseFloat(inScale(amount, scale), 10), currency)
}

// Good
const getPrice = (amount = 0, scale = 2, currency = 'BRL') => {
  return priceNormalize(parseFloat(inScale(amount, scale), 10), currency)
}
```
