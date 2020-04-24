---
layout: post
title:      "Nook Services"
date:       2020-04-24 06:13:16 +0000
permalink:  nook_services
---


Here we are, at the end of the road. My time as a student at Flatiron School is at an end and it honestly feels like such a blur. Thinking back to six months ago when I started this program, I couldn't have imagined then the amount of knowledge and skills I would gain, nor how quickly it would have passed me by. It's very surreal to be finally writing the last blog for the program, having just completed my final React/ Redux project. I feel so accomplished in what I have learned and created here, as well as eager to continue learning since I know this ending is still just the beginning of my journey as a web developer.

My React/ Redux project is called Nook Services. It is designed to be a companion application to the Nintendo Switch game Animal Crossing: New Horizons. I was inspired to get into programming by my love for video games and their communities, and for my final project I wanted to challenge myself to create something that I wish existed for this game and its community. I wanted to be able to look back after completing this project and say that it was something that I could release to friends and the community, and that they would actually want to use it.

The application features two tracking sections, one each for bugs and fish (the game's main collectible items), as well as informational sections on flowers, mystery islands, and Sow Joan's Stalk Market (the game's version of a stock market). Logged in users are able to persist their tracked data with the help of a Rails API that was built to support the front end application. 

The basic functionality of the application relys heavily on the use of the Redux store to hold on to user and site data as well ask Thunk middleware to allow the application to make asynchronous fetch requests to the Rails API in my Redux actions. This functionality is probably the most important aspect of the application, as I needed to store the state of so much collectible data. (80 each for just the fish and bugs) Since this data determines how those items are displayed to the user, even just the simple rendering of most pages relies on this functionality.

So how does one go about implementing this important feature? When I first started creating the application I was wasn't too sure I really understood myself. But, after a lot of research and lesson review (and a little help from classmates and coaches) I feel like I have a firm enough grasp to explain the process.

The first think you will need is to import all of the necessary files to pull this off:

```
import {Provider} from 'react-redux'
import {createStore, applyMiddleware, compose} from 'redux'
import thunk from 'redux-thunk'
```

You will also need some action functions (this is where the magic happens so to speak) as well as a basic reducer function to handle updating the Redux store when we dispatch those actions later.

Create a redux store by using the `createStore()` method. This method takes a reducer function and an optional function as arguments. This optional function will allow us to set up the Thunk middleware that will allow us to use asychronous code in our actions. Your final store setup should look something like this:

```
const store = createStore(appReducer, compose(applyMiddleware(thunk))
```

Now you want to pass that store variable into a Provider component that will wrap all other components in your render. It should look something like this:

```
ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

After that is all set up, you are ready to use asynchronous code in your actions! To give a clearer idea of what that looks like take a look at a small action from the application that I use to fetch the data pertaining to Mystery Islands.

```
export function fetchIslands(){
    return (dispatch) => {
        dispatch({type: 'START_LOADING_ISLANDS'})
        fetch(`http://localhost:3001/islands`)
        .then(response => response.json())
        .then(islands => dispatch({type: 'LOAD_ISLANDS', islands}))
    }
}
```

This function, when mapped to props in my component, can be used to trigger a fetch request to the Rails API. The function itself returns a function which accepts the Redux `dispatch()` as an argument. What this allows us to do is to call that `dispatch()` function inside of the .then block of my fetch request. This ensures that the fetch request resolves, and we have the data we need for our dispatch before sending it off to be handled by the reducer. Without the ability to pass `dispatch()` as an argument, it would be called outside of the fetch request and most likely run before we have the data we need to operate on. 

I hope this brief overview highlights just how essential the Thunk middleware is in providing a bridge between our API and front end application. If you are new to working with these tools as I am, I also hope that this might be helpful or at least nudge you in the right direction. If you would like to check it out, I have provided links to the repo and video walkthrough for this project. Feel free to dig through the code and maybe find solutions to things you are struggling with, or even find ways that my solutions could have been better implemented. If I have learned anything at all at my time in this program, one of the big take aways is that there is always something to be learned from looking at the ways others have solved problems.

Github Repo: https://github.com/kjdowns/nook-services

Video Walkthrough: https://www.youtube.com/watch?v=L-uKSyvmdc0

