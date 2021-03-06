- React came out in 2013
- people starting building big sites with jquery. Now to manage these big sites tools like backbonejs came up to organize. now it slowly progressed to single page apps,where as the app is loaded only once. This led to angular and modularizing the app and split code to small components. Now more and more components needs to be handled and is being interacted with each other. Also data was flowing every where between components and difficult to debug as a result.So a f/w was built to organize components, design data flow and storage, leading to birth of react.

**React Concepts**
1. Dont touch DOM directly. React will do it for us. Changing dom direclty based on user input is Imperative approach. Problem with this approach is its difficult to see relationship between events and how components and events affect each other. React has a declarative approach. We tell react how our app looks like( a json object) and react will decide on how to update the DOM. So we give react the state of our app and react updates our app based on it. So we dont have to say do this and then do this and do this etc, but we tell react this is how my final app should look and react updates our app to reach that state.

2. Build website with small blocks. React is built around reusable components. So build small reusable components. So we can use components deveoped by others, and use component libraries with ready made components. Components can now be shared and reused. And easy to debug.These components are plain JS fns.

3. Uni directional data flow. react is built using state( data ) and components (jsx, js inside html).React uses this to create a VirtualDOM ( a  huge JS object, like tree). VDOM is a blueprint on how to update actual dom.So react reads the VDOM and update DOM. Now VDOM updates when state changes. So an interaction changes State, react will react to it, combines new state with components and update dom using VDOM. so data only flows one way. The data can never flow other way. Data can flow down the VDOM tree. 

4. React can work in any device/platform. To use react, we need a core react library and a platform specific react library that knows how to work with specific DOM

- Decide on what components that we need, where to keep state and what changes when state changes. This is a good design for a react app.

npx allows as to run a command 

- babel and webpack converts react code to vanilla JS that browser understands. Create react app spins up a project that has everything set up for us to start writing code now itself. react-scripts from create react app runs the babel and webpack to run and build the app. Building the react app takes files from src folder, runs webpack scripts and via that babel over it and builds it and puts in the public folder.

- Using class component gives as access to state.

- jsx has different names for some html parameters, like className for class. class is a differnt meaning in jsx. jsx has equivalent to most html fns and parameters.
- jsx has {}, which means a js expression to be executed. Which can be a variable ,expression a fn etc.
- we cannot modify state directly, only via set state. This is part of uni direction flow. Also this restriction allows react to monitor state changes and react to it.

- modern SPA works like, load html , js and css. then just request data or call api as needed, us js to process the data and display it using html and css

- naming an app jsx or js doesnt matter. both works. jsx is just a js file with html inside it. naming conventions might help us.

- state usually lives in one component and is passed down as props. One state is passed down as attributes, it becomes props. Now as state changes all components that receive it as props, will be notified and may be re rendered. So be careful where we store state. WE dont want components taht have no effect on state change to be notified. 

- setstate is a async call. So to see change in state at once we setit, use the callback fn of setstate. Else if we log state, it might not yet be set.

- functional components dont have access to state or lifecylce methods. They are just a components taht are used to render html, get some props render component and be with it.

- state changes can only one uni directional. It can only flow down and never flow up in heirarchy tree

- careful with this reference.WE can bind this context to a method.Arrow fns have this context references the declared scope.

- we dont call a fn in an event handler, cause it will executed during render. We assign a fn to event handler and then its invoked during the event trigger.

- as said earlier setState is async. And many parts of the app can change the state at same time. So when ever we use this.state or this.props to update state inside setState fn, we might not get the actual state. React cannot guarantee that. Instead we can use a fn instead of directly updating using this.state. That fn takes two arguments, which react passes to it automatically. First is prevState and other prevProps. Now instead of this.state, we can refer prevState, so that we always gets the current state, no matter where ever its updated. This is important in wherever we use this.state in setState method.

- its recommended to add props to constructor method and inside it props.

- state can be declared as a variable outisde constructor, as a class variable. It will work just as before.

- everything inside {} is evaluted as javascript.

- http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/

- order of execution: constructor -> render -> comp did mount

- update phase is when we have new props, or state changes or if we force update. Update doesnt remount component, only re render. So render is called during mount and update.

- shouldComponentUpdate method can be used to decide if we want a component to update or not. It returns a boolean. Now why we need this? As state changes, react will update all components that is dependent on that state. Inlcuding all children. Now there may be some component that we know was not affected by state change, even though its a child. Now we can use shouldComponentUpdate in that component class to decide if it should update or not, using prevState and prevProps. So we can stop unnecessarly re rendering that component.

- we also has a componentWillUnmount method. Example is we conditionally hiding a component. So on hiding react will know component is no longer rendered, and will unmount and call lifecycle method before it.

- for every jsx html element returned by react, there is style attribute using which we can set css type styles on the component.

- react has no inbuilt routing. We have to use a separate library for that. react-router is a good choice.

- earlier in Single Page App (SPA), routing was not comptable with browser history. So back and forward buttons doesnt work that well. But now browsers provide a history api to deal with it and modern routing libraries like react-router make use of that to mimic actual browser history management. 

- pages in a react app for also components. But they are not typically reused. Components within this page components are usually reused. Like a login component added to multiple pages. Pages are linked together by router.

- main parts of Router is exact, path and component. path is the url part to match and exact can be true or false. If true path needs to match exactly, else even if part of path matches component is loaded. This can cause multiple components having same base url to load. 

Router also has a Switch component, that whenever it matches a route, will stop matching any more routes.

- every router loaded component is passed  params.(url ,path , history and match). Url will be the url matched, and if multiple urls are matched for a page, the url passed will be the url till the match was found. Eg 
url="/" c="home" and url="/abcd" Now / page will be matched when we go to both address if exact is false. But home component will be passed url "/" as its was caused the component to load.
path is the path value expression used in router.
Match has a parameter isexact, which is true when url and path is same. In above example of "/abcd" it will be false when address is "/abcd" as url and path is  not exact match.
match also has Params, which is the url parameters ( or route parameters)

- react is a SPA and selectively loads components to provide routing. Now if we use normal a links, then entire app needs to be re rendered. So react router has a Link component ,that on clicking will be load only the component needed and not entire app.

- it also has a history parameter. We can push a component to the history ( say on button click or load) and the page will be routed there ( component loaded ). This is another way compared to Link to navigate

- history has a location parameter. That gives current page url. Now with no exact match and we load a url "/as/asd/asd", this might load home at "/", but history location param will be current complete url. This along with exact match can tell us the matching done and routing evaluation.

- match property can be used for dynamic routing. Its value can be used to get the url that we actually need even though the page was loaded using some differnt url. We can then use match url to route as desired.

- Route only passes all above route params to its first child.. and not to other childs in the heirarchy

- one solution for this to pass around history props via the hierarchy. But this is a bad practice knows as props drilling or props tunneling. Cause children in tree who doesnt need this property needs to pass it around as well. 

- higher order component is a fn that takes a component a input, modifies and  returns another component as the output.

- react dom router has a higher order component named withRouter. We can use this to wrap any child component that we need and enhance it to have router props and features.

-The ReactComponent import name is special and tells Create React App that you want a React component that renders an SVG, rather than its filename


### Redux

- if we keep state at components, then we have to decide where to keep state, what components render when state changes, pass state between components etc. This becomes messy. Redux solves this by providing a single state management solution, so that we can decouple state from components.
- Redux can be used outside react, its independant. Its pretty good at managing very large state.
- Redux manages state based on three principles: A single source of truth, State is read only, and changes using pure function. State is never modfied ,we create a new state for a change and we can go back to old state if required. Also pure fns means that the output is predictable. If we give it the same input always, we get the same output. 

- redux terms: Action is a user interaction. It goes through a reducer and creates an output. The output is state( or store) and creates new state. React then reacts to new state and updates DOM

- Redux is based on the arch pattern called Flux Pattern. Its much better than the erstwhile MVC

- Redux allows the state to be more scalable.

- We can have redux and state within components together. 

- If we pass an object as state to react ,react will check if object is new or chagned. Now if we change properties in an object and pass the object to react, react might not see it as a changed object and hence not update dom. So in reducers, instead of modifying current state, we create a new state object with modified values and pass to react.

- there can be middleware that receives action before reducer and can update/modify it. Like a logger for actions.

- reducers might need an initial state set so that they can work when loaded the first time.

- every single reducer gets the action even if it has nothing to do with it. So we check action type before proceeding. So important to have default case to just return the state as itself.

- connect, a higher order fn takes two args. First a fn( usually named mapStateToProps), is used to map state to props in a component. Second is used when a component doestn need state, but needs to send value as props to another component .This is also a fn, usually named mapDispatchToProps.

- if state is a new object but all its properties are same with same value as old state, react will re render, cause its a new object. But if state is same object with different properties or values, react will not rerender.

- reselect is a library that allows us to check state values and decide if new and old state have same value, then it can decide not to pass on new state by creating new object with same old values , but send old state so that component is no re rendered .This is called as memoization.

- reselect "selects" part of state that we need and memoize it so that we can save on re renders

- createStucturedSelector from reselect can automatically pass top level state to selectors.

- if in connect method, if we dont pass mapDipatch fn as second arg, connect by default passes dispatch method to props. We can use this to create any action call, instead of using mapDispatchToProps.

- if our state is readonly, we dont need any actions. Just reducer to pull required state will do

- if a component is direclty linked by Route, then it gets the Route variables. If not directly linked we need to use withRoute to get Route params to that component.

- mapStateToProps has two arguments .First is state and second is own props of the component.

### CSS in JS

- Traditioanl css has a global name space. We declare a class, and the moment its use, its imported to css namespace. So an one usnig the same classname later will get that styles. If we dont want this, we have to name the classes in a way to avoid. 

- CSS in JS aims to solve this, but using JS to apply styles to components.  One such component is styledComponents

### Observable and Promise
- with observable pattern, we can get notified when ever an event occurs and respond to it. With promise pattern, we can still get the data, but we need to trigger a request and get the data. Push vs Pull. Both are async.

- async data fetch i fine to be done in a component if that is the only component that needs the data. If anohter component also needs the data and those two components are loaded independantly, then we might be in a situation where, data fetching component is not loaded and other one is loaded, with no data. So we can move the fetch to a reducer fn so that we can make data fetch independant of component. 

- redux thunk intercepts only fns as actions and dispatches it. Normal actions are passed through. Thunk takes the fn and invokes the fn, causing the dispatch action inside fns to be fired as a result. Thunk passes these dispatch to reducer.

- double bang (!!) on any truthy or falsy value returns true or false. so !!null is false. !!8 is true.

- redux saga is built using generator functions. generator fn is pause and execute fn. It has yield keywork, upon which fn execution is stopped and curretn value is evaluted and returned out of fn. we have to call next() to continue execution.

**Redux Sagas**
- take gives an option to get payload from an action. takeEvery doesnt provide this option.
- we cannot restart sagas. so takeEvery and take runs only once. Takeevery has a fn as second arg, and it just regenerates that fn for every action captured. take doenst has such a fn, so it executes only once( when first run) and is not loaded again until entire app restarts. takevery so creates a never ending loop for listening to action and invoking second generator fn. So takevery is take inside a while loop. 

- so take the generator fn complets and is not invoked again. in takevery the fn call to second generator fn prevents it from completing.

- now if in a while loop in a take, if we put a delay call from saga, take cannto trigger next call to to fn inside while loop ( same as fn in takevery), until delay is completed .Its blocked till then.

- now if taklatest will take the latest action and cancel all before that.

- put in saga ,put the data back into normal redux flow. Like proceed from saga method.

- saga methods get the whole action passed to the action its listening to

**React Hooks**

- hooks is a way to write functional components, that give them more features. It can be used only with fn components and not in class components.

- one hooks component is useState that allows fn component to access state. useState gives as a variable and a setter for that variable inside state, while taking an initial value. So one useState call per state variable we need. It can be called and instantiated any number of times

- another hook is useEffect. its helps to mimic life cylce components. it allows us to fire sideeffects from fn components. useEffect takes a fn that is invkoed when ever the component renders. So changing state , like using useState cause render and hence useEffect to invoked. We can control useEffect invocation and rerender by setting the properties for which it needs to invocked. Else it wil be called for every state change, even if its not intended for that. By passing an empty set properties to be invokced, we can make useEffect fire only when loaded, cause weare now saying fire it for property change, but gave it no properties to monitor.

- useEffect with no props to watch, might cause infite reloading. useEffect fire on comp load, we does some operation, updates state, which cause rerender, which invokes useEffect again, we again does the operation and the cycle continues. So always use the props for which we listen for changes to fire useEffect to control this. 

- we cannot call useEffect inside a conditional. Add conditioanl expression inside useEffect instead.

- check how componets re renders , with parent component rendering etc. espeically with useEffect.

- we can return a fn from useEffect, whcih is a cleanup  method called when component unmount. So similar to componentDidUnmount

- we can write custom hooks. Its just a common function that generalizes the useEffect and useState method taht we write for similar components. The generic hooks accepts paramerts like normal fns, and use it to change the way effect or state is used. We then use this generic hook in our other components instead of repeating the same code.

- useREducer hook brings the reducer state to component, in cases where we need complex state management. useReducer takes an reducer fn( which is like an usual redux fn that has a switch statement) and an initial state. It returns the state and dispatch. We then create fns that create actions and use dispatch to dispatch those fns .Reducer then accepts the actions, uses the reducer fn to update the state. State update causes a re render , thereby updating the application.

**GraphQL**

- REST is very verbose. Like to find comments of a post of a user, we usually make three rest requests. A user fetch req, a user posts fetch request based on userid and a comment fetch request for a post of a user. Also during this process we end up receiving a bunch of data taht we dont care about and have to discard

- Graphql is a unified interface for getting data. It exposes a single end point, against which we can make a query or a mutation .The request is specified in JSON object

- so graphql need only one query to fetch all comments. Also we tell graphql what fields to return. Like a db query for rest end points.So we can fetch comments of a post in a single query. The relationship is built in graphql, like a relational db.

- apollo cache results from graphql

- apollo and graphql can replace redux. We dont need to store state in redux to store state

- graphql can store local state as well, not just fetch remote data. We can use local cache to store, front end persistant store. Only thing is we need to use same query and mutation to interact with local cache. So apollo+graphql can replace redux.

- apollo has a resolver function, that either uses local cache and returns data or gets external data via graphql query and update local cache adn then provide data.

**React Performance**

- react lazy alllows us to load components when needed only. Its used with Route which helps to load components when that Route is loaded. We use lazy to import components using promise. When these components are loaded to Router, it will load it when required only.

- now lazy is async load. So there might be an issue when we request the page, it  might not be loaded at once, leading to an error or empty page or no component.

- to overcome this we wrap lazy loaded route in a Suspense component. Suspence loads an async component and take a fallback argument. Fallback is any valid html component taht is displayed until lazy loaded componet is ready.

- we could wrap individual componetns other than inside Routes in lazy as well. Depends on how big a component is that to need this.

**Error Handling**
- we write a class component that has a static method getDerivedStateFromError. We then wrap this componetn around the components that we need to error handle. When an error occurs in its children, the static method is invoked. We can then process error and setState. Also from that components render method, we can return a certain component in case of error. we can have many error handling components, with differnt error views and wrap then around differnt routes/components as we need. 

- Also another life cylce method componentDidCatch allows us to get error and info about any component thrwing this error. 

- A component with these two life cycle methods is allowed to be an error bounday or error handling component.


- React.memo can be used to memoize a component so that it doenst re render itself when its props doest change, but the state of teh class its part of changes. Same as using shouldComponentUpdate to decide whether to update or not. Same for a class component is React.PureComponent.

- but initial load of a memoized componet is slower than normal load. So there is a tradeoff.

- React memo uses shallow comparision. So if we create new object every render, and even if value is same, react memo cannot find the difference as obejcts are different. So careful with inline array and inline functions

- using reselct the components are already memoized as reselect checks the props to decide if it needs updating. 

- inline functions can be re generated for every render. To avoid this use useCallback hook to wrap the fns. This callback returns the same function is the argument of fn doesnt change so we can avoid creating new fns unnecessarly

- useMemo hook memoizes the fn and the return value as well. It caches the return value of a fn. So when we call same fn the same args, it returns the cached value. useCallback only returns the fn defintion so that we need to invoke the fn every time, even though its the same fn. 

- use compression( like gzip) to reduce js size. 

- React has a inbuilt profiler component that we can wrap components and get profiled info about that component.

### Progressive Web Apps

- https is mandatory for PWA

- it needs an app manifest. THis helps with making the PWA similar to native apps, such as add to home screen option, icons of different sizes, splash screen etc.

- service workers run in background to do tasks we need, like background sync, push notificaiotns, offline capabilities etc. Need to check if browser supports service workers and if yes, register it to use it. Service workers intercept requests to network and check if need to forward request to netwrk or local cache api and serve the request. And do other actions with network actions.

### Gatsby
- its a f/w writtern in react

- in creat react app, the browser builds and render the components. Nextjs is a react f/w that does this using server side rendering. 

- both above are dynamically generating pages. But gatsby is static site generator. SO build and push it to a server and serve frm there. Though we can achieve serverside rendering with gatsby.

- netlify provides a free optin to deploy sites and is linked to github