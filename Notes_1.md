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
