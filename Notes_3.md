- React elements are immutable. Once you create an element, you can’t change its children or attributes. An element is like a single frame in a movie: it represents the UI at a certain point in time. With our knowledge so far, the only way to update the UI is to create a new element, and pass it to ReactDOM.render().

-React DOM compares the element and its children to the previous one, and only applies the DOM updates necessary to bring the DOM to the desired state.

- Always start component names with a capital letter.React treats components starting with lowercase letters as DOM tags. For example, <div /> represents an HTML div tag, but <Welcome /> represents a component and requires Welcome to be in scope.

- Whether you declare a component as a function or a class, it must never modify its own props. All React components must act like pure functions with respect to their props.

-State is similar to props, but it is private and fully controlled by the component.

- Do Not Modify State Directly, use setState. 
- State Updates May Be Asynchronous.React may batch multiple setState() calls into a single update for performance. Because this.props and this.state may be updated asynchronously, you should not rely on their values for calculating the next state. To fix it, use a second form of setState() that accepts a function rather than an object. That function will receive the previous state as the first argument, and the props at the time the update is applied as the second argument:
-State Updates are Merged. When you call setState(), React merges the object you provide into the current state.

-Neither parent nor child components can know if a certain component is stateful or stateless, and they shouldn’t care whether it is defined as a function or a class. This is why state is often called local or encapsulated. It is not accessible to any component other than the one that owns and sets it.

- in react event handler, you cannot return false to prevent default behavior in React. You must call preventDefault explicitly

- The problem with arrow fn for this binding is that a different callback is created each time the component renders. In most cases, this is fine. However, if this callback is passed as a prop to lower components, those components might do an extra re-rendering. We generally recommend binding in the constructor or using the class fields syntax, to avoid this sort of performance problem.

- In rare cases you might want a component to hide itself even though it was rendered by another component. To do this return null instead of its render output.

- We can combine the two by making the React state be the “single source of truth”. Then the React component that renders a form also controls what happens in that form on subsequent user input. An input form element whose value is controlled by React in this way is called a “controlled component”.

- Starting with ECMAScript 2015, the object initializer syntax also supports computed property names. That allows you to put an expression in brackets [], that will be computed and used as the property name. Value in [] will be computed to find variabe name and then initialize

- In React, sharing state is accomplished by moving it up to the closest common ancestor of the components that need it. This is called “lifting state up”.

- no inheritance in react

-Ask three questions about each piece of data:
	1.Is it passed in from a parent via props? If so, it probably isn’t state.
	2.Does it remain unchanged over time? If so, it probably isn’t state.
	3.Can you compute it based on any other state or props in your component? If so, it isn’t state