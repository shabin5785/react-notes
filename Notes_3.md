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
    
- to find out where state should live, For each piece of state in your application:
	1.Identify every component that renders something based on that state.
	2.Find a common owner component (a single component above all the components that need the state in the 	 hierarchy).
	3.Either the common owner or another component higher up in the hierarchy should own the state.
	4.If you can’t find a component where it makes sense to own the state, create a new component solely for holding the state and add it somewhere in the hierarchy above the common owner component.
    
 ### Code splitting and lazy loading
    
- Code-Splitting is a feature supported by bundlers like Webpack, Rollup and Browserify (via factor-bundle) which can create multiple bundles that can be dynamically loaded at runtime.Code-splitting your app can help you “lazy-load” just the things that are currently needed by the user, which can dramatically improve the performance of your app. While you haven’t reduced the overall amount of code in your app, you’ve avoided loading code that the user may never need, and reduced the amount of code needed during the initial load.
-The best way to introduce code-splitting into your app is through the dynamic import() syntax. When Webpack comes across this syntax, it automatically starts code-splitting your app

-The React.lazy function lets you render a dynamic import as a regular component.React.lazy and Suspense are not yet available for server-side rendering. If you want to do code-splitting in a server rendered app, we recommend Loadable Components. The lazy component should then be rendered inside a Suspense component, which allows us to show some fallback content (such as a loading indicator) while we’re waiting for the lazy component to load.


-If the other module fails to load (for example, due to network failure), it will trigger an error. You can handle these errors to show a nice user experience and manage recovery with **Error Boundaries**. Once you’ve created your Error Boundary, you can use it anywhere above your lazy components to display an error state when there’s a network error

- A good place for code splitting and lazy loading is with routes.

-React.lazy currently only supports default exports. If the module you want to import uses named exports, you can create an intermediate module that reexports it as the default. This ensures that tree shaking keeps working and that you don’t pull in unused components.

### Context
-  Context is designed to share data that can be considered “global” for a tree of React components, such as the current authenticated user, theme, or preferred language


### Error Boundary
- A JavaScript error in a part of the UI shouldn’t break the whole app. Error boundaries are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of the component tree that crashed. Error boundaries catch errors during rendering, in lifecycle methods, and in constructors of the whole tree below them.

- Error boundaries do not catch errors for:
	1.Event handlers (learn more)
	2.Asynchronous code (e.g. setTimeout or requestAnimationFrame callbacks)
	3.Server side rendering
	4.Errors thrown in the error boundary itself (rather than its children)
    

- A class component becomes an error boundary if it defines either (or both) of the lifecycle methods static getDerivedStateFromError() or componentDidCatch(). Use static getDerivedStateFromError() to render a fallback UI after an error has been thrown. Use componentDidCatch() to log error information.

- Error boundaries work like a JavaScript catch {} block, but for components. Only class components can be error boundaries. In practice, most of the time you’ll want to declare an error boundary component once and use it throughout your application

-As of React 16, errors that were not caught by any error boundary will result in unmounting of the whole React component tree.We debated this decision, but in our experience it is worse to leave corrupted UI in place than to completely remove it.

- React components are declarative and specify what should be rendered. try / catch is great but it only works for imperative code,Error boundaries preserve the declarative nature of React, and behave as you would expect.

- React doesn’t need error boundaries to recover from errors in event handlers. Unlike the render method and lifecycle methods, the event handlers don’t happen during rendering. So if they throw, React still knows what to display on the screen.If you need to catch an error inside event handler, use the regular JavaScript try / catch statement

### Higher Order Component
- a higher-order component is a function that takes a component and returns a new component. Whereas a component transforms props into UI, a higher-order component transforms a component into another component.

- Resist the temptation to modify a component’s prototype (or otherwise mutate it) inside a HOC. Instead of mutation, HOCs should use composition, by wrapping the input component in a container component

- HOCs should pass through props that are unrelated to its specific concern. 

- The container components created by HOCs show up in the React Developer Tools like any other component. To ease debugging, choose a display name that communicates that it’s the result of a HOC.

- Don’t Use HOCs Inside the render Method. React’s diffing algorithm (called **reconciliation**) uses component identity to determine whether it should update the existing subtree or throw it away and mount a new one. If the component returned from render is identical (===) to the component from the previous render, React recursively updates the subtree by diffing it with the new one. If they’re not equal, the previous subtree is unmounted completely.Instead, apply HOCs outside the component definition so that the resulting component is created only once. Then, its identity will be consistent across renders. 

- Static Methods Must Be Copied Over. When you apply a HOC to a component, though, the original component is wrapped with a container component. That means the new component does not have any of the static methods of the original component

- There are similarities between HOCs and a pattern called container components. Container components are part of a strategy of separating responsibility between high-level and low-level concerns. Containers manage things like subscriptions and state, and pass props to components that handle things like rendering UI. HOCs use containers as part of their implementation. You can think of HOCs as parameterized container component definitions. To avoid manual work, You can use hoist-non-react-statics to automatically copy all non-React static methods. Another possible solution is to export the static method separately from the component itself

- While the convention for higher-order components is to pass through all props to the wrapped component, this does not work for refs. That’s because ref is not really a prop — like key, it’s handled specially by React. If you add a ref to an element whose component is the result of a HOC, the ref refers to an instance of the outermost container component, not the wrapped component.The solution for this problem is to use the React.forwardRef API 

### Notes

- React is unaware of changes made to the DOM outside of React. It determines updates based on its own internal representation, and if the same DOM nodes are manipulated by another library, React gets confused and has no way to recover. The easiest way to avoid conflicts is to prevent the React component from updating. You can do this by rendering elements that React has no reason to update, like an empty <div />.

- Fundamentally, JSX just provides syntactic sugar for the React.createElement(component, props, ...children) function.

- Since JSX compiles into calls to React.createElement, the React library must also always be in scope from your JSX code

- User-Defined Components Must Be Capitalized. When an element type starts with a lowercase letter, it refers to a built-in component like <div> or <span> and results in a string 'div' or 'span' passed to React.createElement. Types that start with a capital letter like <Foo /> compile to React.createElement(Foo) and correspond to a component defined or imported in your JavaScript file.We recommend naming components with a capital letter. If you do have a component that starts with a lowercase letter, assign it to a capitalized variable before using it in JSX.
  
- We cannot use a general expression as the React element type. If you do want to use a general expression to indicate the type of the element, just assign it to a capitalized variable first.
  
- You can pass any JavaScript expression as a prop, by surrounding it with {}. if statements and for loops are not expressions in JavaScript, so they can’t be used in JSX directly. Instead, you can put these in the surrounding code
  
- If you pass no value for a prop, it defaults to true. In general, we don’t recommend not passing a value for a prop, because it can be confused with the ES6 object shorthand
  
- In JSX expressions that contain both an opening tag and a closing tag, the content between those tags is passed as a special prop: props.children. You can provide more JSX elements as the children. You can pass any JavaScript expression as children, by enclosing it within {}.
  
- false, null, undefined, and true are valid children.
  
### Speed and Performance
  
- Use the Production Build
  
- If your application renders long lists of data (hundreds or thousands of rows), we recommended using a technique known as “windowing”. This technique only renders a small subset of your rows at any given time, and can dramatically reduce the time it takes to re-render the components as well as the number of DOM nodes created. react-window and react-virtualized are popular windowing libraries.
  
- If you know that in some situations your component doesn’t need to update, you can return false from shouldComponentUpdate instead, to skip the whole rendering process, including calling render() on this component and below.
  
- The Profiler measures how often a React application renders and what the “cost” of rendering is. Its purpose is to help identify parts of an application that are slow and may benefit from optimizations such as memoization
  
### Portals
 
 - Portals provide a first-class way to render children into a DOM node that exists outside the DOM hierarchy of the parent component.
  
 - Even though a portal can be anywhere in the DOM tree, it behaves like a normal React child in every other way. Features like context work exactly the same regardless of whether the child is a portal, as the portal still exists in the React tree regardless of position in the DOM tree. This includes event bubbling. An event fired from inside a portal will propagate to ancestors in the containing React tree, even if those elements are not ancestors in the DOM tree.
  
### Hooks
  
 - Hooks are a new addition in React 16.8. They let you use state and other React features without writing a class. Hooks allow you to reuse stateful logic without changing your component hierarchy. This makes it easy to share Hooks among many components or with the community
  
 
  
  
  
  
  

