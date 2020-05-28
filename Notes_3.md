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
- A JavaScript error in a part of the UI shouldn’t break the whole app.


