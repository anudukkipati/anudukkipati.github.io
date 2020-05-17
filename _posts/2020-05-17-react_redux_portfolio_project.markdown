---
layout: post
title:      "React Redux Portfolio Project"
date:       2020-05-17 18:52:06 +0000
permalink:  react_redux_portfolio_project
---


For the final project, we were required to build project which includes a Rails backend API and a single page React frontend app. I decided to build a notes app which will have information on different topics in web development. My Dev.Notes app is a simple app which provides information that can be useful to web development students. 

**Step 1: Setting up Rails backend**

To create a Rails API, I used -

```
rails new devNotes-backend --api
```


This will do three main things:

•	Configure your application to start with a more limited set of middleware than normal. Specifically, it will not include any middleware primarily useful for browser applications (like cookies support) by default.

•	Make ApplicationController inherit from ActionController::API instead of ActionController::Base. As with middleware, this will leave out any Action Controller modules that provide functionalities primarily used by browser applications.

•	Configure the generators to skip generating views, helpers, and assets when you generate a new resource

Then I created my **model** "Note" –

```
 rails g scaffold note title topic url content:text
```


 A **scaffold in Rails** is a full set of model, database migration for that model, controller to manipulate it, views to view and manipulate the data, and a test suite for each of the above. But since I used - - api to create the app, views are not created.

Added **validations** to the model –

```
validates :title, :topic, :url, :content, presence:true
```

Created some “notes” in seed.rb so that the database is populated with some data that can be used and ran migrations.

```
db: migrate
db:seed

```

Installed “gem **rack-cors**” which will provide  support for Cross-Origin Resource Sharing (CORS) for Rack compatible web applications and made changes to config/initializers/cors.rb  to allow GET, POST or OPTIONS requests from any origin on any resource.

Started the server using rails s.

**Step 2 : Create React Frontend App**

 I used `npx create-react-app dev-notes-frontend` which will provide the environment required to build a single page application.

It created a directory called dev-notes-frontend inside the current folder. Inside that directory, it generated the initial project structure and installed the transitive dependencies:


```
dev-notes-frontend
├── README.md
├── node_modules
├── package.json
├── .gitignore
├── public
│   ├── favicon.ico
│   ├── index.html
│   └── manifest.json
└── src
    ├── App.css
    ├── App.js
    ├── App.test.js
    ├── index.css
    ├── index.js
    ├── logo.svg
    └── serviceWorker.js
    └── setupTests.js
```


Started the server using `npm start` which will open a web browser to show the app.

**Step 3 : React-Redux**

Installed redux and react-redux so that state can be managed using redux. React Redux is the official Redux UI binding library for React. The React Redux library gives access to a component called the **Provider**. The `<Provider /> ` makes the Redux store available to any nested components that have been wrapped in the connect() function. Since any React component in a React Redux app can be connected, most applications will render a <Provider> at the top level, with the entire app’s component tree inside of it. It wraps around the App component. Using the <Provider> component provided by the React Redux library, components have the ability to be connected to the store.

```
import React from 'react';
import ReactDOM from 'react-dom';
import 'bootstrap/dist/css/bootstrap.min.css';
import './index.css';
import App from './App';
import { BrowserRouter as Router } from 'react-router-dom'
import { createStore, applyMiddleware, compose, combineReducers } from 'redux';
import { Provider } from 'react-redux'
import thunk from 'redux-thunk'
import notesReducer from './reducers/notesReducer'

import * as serviceWorker from './serviceWorker';

const rootReducer = combineReducers (
  {
    notes: notesReducer
   
  }
)

const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;

const store = createStore(rootReducer,composeEnhancers(
  applyMiddleware(thunk)
 ));

ReactDOM.render(
  <React.StrictMode>
      <Provider store={store}>
      <Router>
        <App />
      </Router>
    </Provider>
    
  </React.StrictMode>,
  document.getElementById('root')
);

serviceWorker.unregister();

```


**Redux Thunk**

When retrieving data from APIs, we run into a problem where the action creator returns an action before the data is retrieved.  To resolve this, a middleware called Thunk can be used. Thunk allows us to return a function inside of our action creator instead of a plain JavaScript object. That returned function receives the store's dispatch function, and with that we can dispatch multiple actions: one to place the state in a loading state, and another to update our store with the returned data.

```
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import rootReducer from './reducers';
 
const store = createStore(rootReducer, applyMiddleware(thunk));
 
ReactDOM.render(
  <Provider store={store} >
    <App />
  </Provider>, document.getElementById('root')
)

```

**React Router**: a routing library for React that allows us to link to specific URLs then show or hide various components depending on which URL is displayed. React Router conditionally renders certain components to display depending on the route being used in the URL (/ for the home page, /notes for the notes page, etc.). To use it, I installed ` npm install react-router-dom` and imported `import {BrowserRouter as Router, Route, Switch} from react-router-dom`. As everything that needs to be rendered has to go inside ‘BrowserRouter’, I wrapped App element inside Router.

```
ReactDOM.render(
  <React.StrictMode>
      <Provider store={store}>
      <Router>
        <App />
      </Router>
    </Provider>
    
  </React.StrictMode>,
  document.getElementById('root')
);

```

I added the **switch** and **route** elements in App.js. Switch and Route are route matching components. When a <Switch> is rendered, it searches through its children <Route> elements to find one whose path matches the current URL. When it finds one, it renders that <Route> and ignores all others. If no <Route> matches, the <Switch> renders nothing(null). As <Route path> matches the beginning of the URL, and not the whole thing, I used <Route exact path> which matches the entire URL.

```
function App() {
  return (
    <Container>

    
     <div className="App">
       <NavBar  />
       <Header title={"Dev.Notes"} />

       <br></br>
       <Switch>
         <Route exact path="/" component={Home} />
         <Route exact path="/notes" component={NotesContainer} />
         <Route exact path="/notes/new" component={NewNoteForm}/>
            <Route exact path="/notes/:id" component={NoteShow} />
          </Switch>
          
        </div>
      </Container>
  );
}

export default App;

```

As I built my app, I added components(stateless) and containers (with state) as needed.

**Resources**:

 https://guides.rubyonrails.org/api_app.html#creating-a-new-application 
 
 https://learn.co/tracks/online-software-engineering-structured/redux/async-redux/redux-thunk 
 
 https://reacttraining.com/react-router/web/guides/primary-components

