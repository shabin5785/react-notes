
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

- if we link react components wiht <a> tag, then react will make a request for new page for every link, causing exist html page to be dumped, new page requested( same as dumped page) and react scripts run. So avoid using it and link using react components. 
