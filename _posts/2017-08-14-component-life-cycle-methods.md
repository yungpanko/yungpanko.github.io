---
layout: post
title:  "Component Lifecycle Methods: Render Methods"
date:   2017-08-14
author: Jared Johnson
---

I've been building [React](https://facebook.github.io/react/) projects for the last few weeks and I keep finding myself returning to the chart below (pulled from a lesson in the [Learn.co](https://learn.co/) curriculum). It summarizes the inputs and use cases for the four Component Lifecycle Methods related to rendering.

|            Method           | nextProps | nextState | Can call `this.setState` |
|:---------------------------:|:---------:|:---------:|:------------------------:|
| `componentWillReceiveProps` |    yes    |     no    |            yes           |
|   `shouldComponentUpdate`   |    yes    |    yes    |            no            |
|    `componentWillUpdate`    |    yes    |    yes    |            no            |
|     `componentDidUpdate`    |    yes*   |    yes*   |            yes           |

|            Method           |              Called when?              |                  Used for                 |
|:---------------------------:|:--------------------------------------:|:-----------------------------------------:|
| `componentWillReceiveProps` |   component is going to get new props  |           applying state changes          |
|   `shouldComponentUpdate`   |   when a re-render has been triggered  |       deciding whether to re-render       |
|    `componentWillUpdate`    | new state and props are being received | dispatching actions based on state change |
|     `componentDidUpdate`    |          just after re-render          |       DOM updates following a render      |

\* `componentDidUpdate` will actually receive `prevProps` and `prevState` as arguments, as the newly applied state and props can be accessed through `this.props` and `this.state`.

And below is the order in which these methods are called, courtesy of [Osmel Mora](https://medium.com/react-ecosystem/react-components-lifecycle-ce09239010df).
![render methods order](/assets/images/lifecycle1.png)

This detail, alone, is worth a bookmark but in order to fully convince you, I shall elaborate. Let's break down each of these methods. First up, we have `componentWillReceiveProps`.

## componentWillReceiveProps

An important point to make here is that each of these methods is called **after** a component has been mounted and thus **after** the initial render. Our first render method is called before a component receives new props. This guy won't save you if you forget to write a default state or send initial props to your component. `componentWillReceiveProps` is a method that React gives you to deal with new props without triggering a state change (leading to an infinite loop). One of my code instructors argues that `componentWillReceiveProps` is the single most underutilized lifecycle method and I would agree given my own history of underutilizing it.

code example:
````javascript
componentWillReceiveProps(nextProps){
  this.setState({
    itemToBeUpdated: nextProps.newInfoToUse
  })
}
````

In the code example above, I am using my new props to update the state of my component. This will take place before the re-render has completed and should any display elements be controlled by what has changed in state, theses changes will be displayed to the user.

## shouldComponentUpdate

Next up is the odd one of the bunch, `shouldComponentUpdate`. This function is different from the others in the component lifecycle in that it expects to return a boolean (and defaults to true). `shouldComponentUpdate` is used to tell React whether or not a re-render that has been triggered should be completed. This is useful when the developer is concerned with gating unnecessary rendering.

code example:
````javascript
shouldComponentUpdate(nextProps, nextState) {
  return this.state.text !== nextState.text
}
````

The code example above is taken from one of my projects. I wanted to update a controlled searchable dropdown list ONLY if the text that I was storing my state changed. Any other actions that trigger a re-render in this component will be blocked by my `shouldComponentUpdate` function.

## componentWillUpdate

Our next function, `componentWillUpdate` is the last method called before a render takes place. This is our last opportunity to dispatch actions, so long as they do not attempt to push changes to our component state.

## componentDidUpdate

The last render method, `componentDidUpdate` is called as soon as a re-render has completed. The primary use cases for this method are interacting with third-party libraries and resources.

## Additional resources:

1. [React.Component Official Documentation](https://facebook.github.io/react/docs/react-component.html)
2. [React Ecosystem](https://medium.com/react-ecosystem/react-components-lifecycle-ce09239010df)
