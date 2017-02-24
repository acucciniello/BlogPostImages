# Using React Router for Client Side Redirecting

## Introduction

If you are using React in your front end of your Node.js web application and you would like to use React Router in order to handle routing, then you have come to the right place.  Today, we will learn how to have your client side redirect to another page after you have completed some processing.  Let's get started!

## Installs

First we will need to make sure we have a couple of things installed.  The first thing here is to make sure you have [Node and NPM][nodeInstall] installed. In order to make this as simple as possible we are going to use *create-react-app* to get React full working in our application.  You install this by doing:

`$ npm install -g create-react-app`

Now create a directory for this example and enter it, here we will call it client-redirect. 

```
$ mkdir client-redirect
$ cd client-redirect
```

Once in that directory, initialize  create-react-app
in the repo.

`$ create-react-app client`


Once it is done, test that it is working by running:

`$ npm start`

You should see something like this:

![Create_React_App_Works_Image](https://github.com/acucciniello/BlogPostImages/blob/master/Using-React-Router-for-Client-Side-Redirecting/createReactAppWorks.png)

The last thing you must install is *react-router*:

`$ npm install --save react-router`

Now that you are all set up let's start with some code.

## Code

First we will need to edit the main JavaScript file, in this case is located at **client-redirect/client/src/App.js**.

### App.js

App.js is where we handle all of the routes for our application and acts as the main.js file.  Here is what the code looks like for App.js:

```
import React, { Component } from 'react'
import { Router, Route, browserHistory } from 'react-router'
import './App.css'
import Result from './modules/result'
import Calculate from './modules/calculate'

class App extends Component {
  render () {
    return (
      <Router history={browserHistory}>
        <Route path='/' component={Calculate} />
        <Route path='/result' component={Result} />
      </Router>
    )
  }
}

export default App
```

If you are familiar  with React, you should not be too confused as to what is going on.  At the top, we are importing all of the files and modules we need.  We are importing React, react-router, our App.css file for styles, and result.js and calculate.js files (do not worry we will show the implementation for these shortly).

The next part is where we do something different.  We are using react-router to set up our routes.

We chose to use a history of type *browserHistory*.  History in react-router listens to the browser's address bar  for anything changing and parses the URL from the browser and stores it in a location object so the router can match the specified route and render the  different components for that path. 

We then use `<Route>` tags in order to specify what path we would like a component to be rendered on. In this case, we are using `'/'` path for the components in calculate.js and `'/result'` path for the components in result.js.

Let's define what those pages will look like and see how the client can redirect using browserHistory.

### calculate.js

This page is a basic page with two text boxes and a button. Each text box should receive a number and when the button is clicked, we are going to calculate the sum of the two numbers given.  Here is what that looks like:

```
import React, { Component } from 'react'
import { browserHistory } from 'react-router'

export default class Calculate extends Component {
  render () {
    return (
      <div className={'Calculate-page'} >
        <InputBox type='text' name='first number' id='firstNum' />
        <InputBox type='text' name='second number' id='secondNum' />
        <CalculateButton type='button' value='Calculate' name='Calculate' onClick='result()' />
      </div>

    )
  }
}

var InputBox = React.createClass({
  render: function () {
    return <div className={'input-field'}>
      <input type={this.props.type} value={this.props.value} name={this.props.name} id={this.props.id} />
    </div>
  }
})

var CalculateButton = React.createClass({
  result: function () {
    var firstNum = document.getElementById('firstNum').value
    var secondNum = document.getElementById('secondNum').value
    var sum = Number(firstNum) + Number(secondNum)
    if (sum !== undefined) {
      const path = '/result'
      browserHistory.push(path)
    }
    window.sessionStorage.setItem('sum', sum)
    return console.log(sum)
  },
  render: function () {
    return <div className={'calculate-button'}>
      <button type={this.props.type} value={this.props.value} name={this.props.name} onClick={this.result} >
              Calculate
      </button>
    </div>
  }
})
```

The important part we want to focus on is inside the *result* function of the *CalculateButton* Class.  We take the two numbers and sum them. Once we have the sum, we create a `path` variable to hold the route we would like to go to next.  Then `browserHistory.push(path)` redirects the client to a new path of `localhost:3000/result`.  We then store the sum in sessionStorage in order to retrieve it on the next page.   


### result.js

This page is simply a page that will display your result from the calculation, but it serves as the page you redirected to with react-router.  Here is the code:

```
import React, { Component } from 'react'

export default class Result extends Component {
  render () {
    return (
      <div className={'result-page'} >
        Result :
        <DisplayNumber id='result' />
      </div>
    )
  }
}

var DisplayNumber = React.createClass({
  componentDidMount () {
    document.getElementById('result').innerHTML = window.sessionStorage.getItem('sum')
  },
  render: function () {
    return (
      <div className={'display-number'}>
        <p id={this.props.id} />
      </div>
    )
  }
})
```

We simply create a class that wraps a paragraph tag. It also has a *componentDidMount()* function, which allows us to access the sessionStorage for the sum once the component output has been rendered by the DOM.  We update the innerHTML of the paragraph element with the sum's value.

## Test

Let's get back to the *client* directory of our application.  Once we are there we can run: 

`$ npm start`

This should open a tab in your web browser at `localhost:3000`.  This is what it should look like when you add numbers in the text boxes (here I added 17 and 17).

![CalculatePage_Image](https://github.com/acucciniello/BlogPostImages/blob/master/Using-React-Router-for-Client-Side-Redirecting/CalculatePage.png)

This should redirect you to a page that looks like this:

![ResultPage_Image](https://github.com/acucciniello/BlogPostImages/blob/master/Using-React-Router-for-Client-Side-Redirecting/ResultPage.png)

## Conclusion 


There you go! You now have a web app that utilizes client-side redirecting! To summarize what we did, here is a quick breakdown of what happened:

1. Installed the prerequisites: node, npm
2. Installed create-react-app
3. Created a create-react-app
4. Installed react-router
5. Added our routing to our App.js
6. Created a module that calculated the sum of two numbers and redirected to a new page
7. Displayed the number on the new redirected page


If you enjoyed this post share it on [twitter][twit]. Check out the code for this tutorial on [GitHub][gitRepo]. 

## Possible Resources

Check out my [GitHub][mainGit]

View my personal [blog][pblog]

GitHub pages for:

 [react-router][reactRouter]
 
 [create-react-app][createReactApp]


[twit]: https://twitter.com/
[gitRepo]: https://github.com/acucciniello/client-redirecting-react-router
[mainGit]: https://github.com/acucciniello/
[pblog]: http://www.acucciniello.com/
[reactRouter]: https://github.com/ReactTraining/react-router
[createReactApp]: https://github.com/facebookincubator/create-react-app
[nodeInstall]: https://nodejs.org/en/download/