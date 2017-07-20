##### 不用 Redux 如何实现组件间通信呢？

可以用来概括的是:
`通过子组件，修改父组件的 state ，然后把父组件的 state 作为所有子组件的 props 值传入各个子组件`

这样就实现了各个兄弟组件间通信。

### 子组件修改父组件的 state

下面有个小例子仅供大家参考下

```js
import React, { Component } from 'react';


class Child extends Component {

  handleClick = () => {
    this.props.changeColor('green')
  }

  render() {
    return (
      <div style={{ 'border' : '3px solid red' }}>
        <button onClick={this.handleClick}>Child button</button>
      </div>
    );
  }
}

class App extends Component {
  state = {
    bgColor: 'yellow'
  }

  changeBackground = (color) => {
    this.setState({
      bgColor: color
    })
  }

  render() {
    return (
      <div style={{ 'border' : '3px solid green',
                    'padding' : '20px',
                    'backgroundColor' : this.state.bgColor
      }}>
        <Child changeColor={this.changeBackground} />
      </div>
    );
  }
}

export default App

```
