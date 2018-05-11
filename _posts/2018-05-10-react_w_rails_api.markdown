---
layout: post
title:      "React w/ Rails API"
date:       2018-05-10 21:57:49 -0400
permalink:  react_w_rails_api
---

## Using Router v4
Getting started with v4 is easy.
In the terminal you type
```
npm install --save react-router-dom
```
and in App.js you add
```
import { BrowserRouter as Router, Route } from 'react-router-dom';
```

Wrap your app with Router like so:
```
class App extends Component {
  render() {
    return (
      <Router>
        <div className="App"></div>
      </Router>  
    );
  }
}
```
We're now ready to add routes.

The following code works!

```
import React, { Component } from 'react';
import { BrowserRouter as Router, Route, Link } from 'react-router-dom';
import logo from './logo.svg';
import './App.css';

class TwoDeep extends Component {
  render() {
    return (
      <div>
        <h3>Two</h3>
      </div>
    )
  }
}

class OneDeep extends Component {
  render() {
    return (
      <div>
        <h2>One</h2>
        <Link to='/one/two'>two</Link>
        <Route path='/one/two' component={TwoDeep} />
      </div>
    )
  }
}


class App extends Component {
  render() {
    return (
      <Router>
        <div className="App">
          <h1>App</h1>
          <Link to='/one'>one</Link>
          <Route path='/one' component={OneDeep} />
        </div>
      </Router>
    );
  }
}

export default App;

```

As you can see, we are nesting OneDeep within App and TwoDeep within OneDeep.
I like to think of the routes as conditional components, the condition being whatever route is being fed to the browser.

One gotcha, that got me many times is this (same code except I added one word 'exact' in the App component)-

```
import React, { Component } from 'react';
import { BrowserRouter as Router, Route, Link } from 'react-router-dom';
import logo from './logo.svg';
import './App.css';

class TwoDeep extends Component {
  render() {
    return (
      <div>
        <h3>Two</h3>
      </div>
    )
  }
}

class OneDeep extends Component {
  render() {
    return (
      <div>
        <h2>One</h2>
        <Link to='/one/two'>two</Link>
        <Route path='/one/two' component={TwoDeep} />
      </div>
    )
  }
}


class App extends Component {
  render() {
    return (
      <Router>
        <div className="App">
          <h1>App</h1>
          <Link to='/one'>one</Link>
          <Route exact path='/one' component={OneDeep} />
        </div>
      </Router>
    );
  }
}

export default App;

```

Now, when I click on the 'two' link, not only does it not render and display TwoDeep, but the OneDeep component disappears as well!
This is because by clicking on the 'two' link, I changed the route from '/one' to '/one/two', and component OneDeep only displays when the EXACT route of '/one' appears.
So OneDeep is not rendered and disappears from the screen.
Unfortunately TwoDeep is nested within OneDeep so its route is rendered irrelevant (pun not intended).

This is a simple concept that reveals the beauty of Router v4, Routes are actually just components.
