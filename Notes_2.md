
- just declaring state is enough in a class component. babel will auto add constructor over it.

- when we bind a fn to an event in render method of a component, we dont put ending () .cause putting this will lead to the fn being executed when render method is laoded. We want the fn to be called in a later point when the event occurs.

- controlled component in react is one where react is the source of truth for the component value. and not the HTML.

- **this** is evaluated from where the method is called from and not by the method itself. If we want it to be based on fn itself, make it an arrow fn. Two ways for this: in event change method, use a arrow call back fn to invoke our normal fn, or in event change method invoke arrow fn.

- we cannot pass props upwards from child to parent. Only downwards. To solve this, we can pass a fn from parent to child and child will invoke it when needed, sending props to parent.

- React ref gives us access to DOM elements. Rather than refering them using DOM selectors.

- we need to put only the data that changes inside state.

- Redux flow: Action creator -> action -> dispatcher -> reducer -> state

- actions must be a plain js object. So we cannot put async await in action creator. Use middleware for async code there.

- reducers should never return value undefined

- every time a reducer is called, its invoked with a state value equal to previous call returned state value. So for first time its undefined. With teh way reducer in redux is coded, it detects a change by comparing prevstate with newstate .Its an object comparision .So to make haschanged true need to return a new state object. So if we mutate prevstate and return it as new object, the haschanged comparison becomes false as prev and curretn state are same. So always create a new object as new state and copy prev state to it and return.

- trying to memoize an async fn in action creator is complicated. Use the pattern for that. So instead of memoizing action creator fn or dispatch fn, call a memoized fn from action creator.

- react-router-dom is the package for routing. react-router is the core pacakge and dom one is to be used for web. similary we have react-router-native 

- we can have duplicate routes in react router, It will match both and will show both components.

- react router checks the value from url ( extracted path) contains the router match path. So without exact multiple react router paths will be contained in url , like "/" and "/abc", and "/abc/5" for the url me.com/abc/5. exact will check for an exact match.

- if we link react components wiht <a> tag, then react will make a request for new page for every link, causing exist html page to be dumped, new page requested( same as dumped page) and react scripts run. So avoid using it and link using react components Link.

- React router has : browser router( look at url), hashrouter( look after hash automaticaly put by react after url) and memory router ( no url used for navigation. react router keeps url in memory and wont chagne url)
  
  
  - if we ask react router for a route taht doesnt exist, it will check in public folder for a file named like that. if it cannot find it it will return the index page. This is what we get when we normally get an error for unkown route in traditioanl apps. But react serves index html
  
 - key interpolation: generate the  key in an object dynamically when code runs
  
 
  - redux form makes away with boiler plate code for wiring a form to redux and the actions. it handles it automatically in the backend. the key for redux-form in reducer needs to be form.
  
  - in redux-form, the validate and fields are linked by an error obejct with keys same as field names.
  
  - browserrouter listens to changes in history object. When history object updates, router react to that change and cahgnes route. Now getting reference to history object is easy in a component, but quite difficult outside that, part of which is due to the reason that history object is created by browserrouter. To overcome this, we can create history object ourselves and nt allow browserrouter to create and control it.
  
 - its better for each component to own its own data generation and fetching.
  
  - usually react components are heirachially arranged. One below another in a tree structure. Using a portal we can render a component as a child of some other component , like a child of root. So we haev multipe childs for root instead of usual one. Commonly used for popup or modals.
  
  - we create portal using ReactDOM similar to creating root component. Now rendering portal against body as root causes the entire body to be replaced. So we usually create a placeholer in index.html and render portal under that.
  
  - in nested elements, if an event occurs and is not handled by js, it bubbles up in heirarchy until its handled. We can call stop propagation on the event to prevent it bubble up.
  
  - We cannot return jsx elements without surrounding div or parent element. Its not valid and throws error. WE can use React.Fragment to overcome this.
  
  - Using react context, we can communicate with any prarent-child, by passing nested layers in between them. Wihtout that we need to pass props through all nested layers to reach lower level. Context object can be though of as a stream connecting source and provider. We can push data to it and get from it. 
  
  - we use contextType static field in class to link context object.
  
  - each provider in context creates its own stream or storage. 
  
  - we can get value from context using this.context or by using a consumer. consumers are used when we need to get value from multiple contexts. this.context is used when there is only one context
  
  - context is not a replacement for redux
  
  - hooks brings component state and life cycle fns to functional components. Hooks allows to better share code between components and code reuse between them. Its better in this case than a class based component.
  
  - useEffect can take care of both componentDidmount and componentDidupdate
  
  - by default useEffect is called everytime a component is loaded or updated. We can pass a variable to the useEffect array to monitor, so taht fn is invoked only when the variabel changes.
  
  - if we pass an empty array to useEffect, its caled only once ( componentDidMount), cause value in array never cahnges. 
  
  - also useEffect compares object equality. If we return an object in useEffect array, the object is different each time so comparision causes useEffect to be invoked .
