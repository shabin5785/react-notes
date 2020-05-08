
- just declaring state is enough in a class component. babel will auto add constructor over it.

- when we bind a fn to an event in render method of a component, we dont put ending () .cause putting this will lead to the fn being executed when render method is laoded. We want the fn to be called in a later point when the event occurs.

- controlled component in react is one where react is the source of truth for the component value. and not the HTML.

- **this** is evaluated from where the method is called from and not by the method itself. If we want it to be based on fn itself, make it an arrow fn. Two ways for this: in event change method, use a arrow call back fn to invoke our normal fn, or in event change method invoke arrow fn.

- we cannot pass props upwards from child to parent. Only downwards. To solve this, we can pass a fn from parent to child and child will invoke it when needed, sending props to parent. 