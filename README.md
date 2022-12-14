<h2 style="text-align:center">React Use Effect, Reducers, and Context API</h2>

</br></br>

- [Use Effect](#use-effect)
  - [Adding Dependencies (to stop the loop!)](#adding-dependencies-to-stop-the-loop)
- [Using Reducers and useReducer()](#using-reducers-and-usereducer)
  - [</br></br>](#brbr)
- [Context API](#context-api)


---
# Use Effect

Essentially, `useEffect()` is used when you want to continually track the state of something in the event that it changes. So something like a login page is practical here, Take a look!

![alt-text](/01-starting-project/photo-examples/side-effect-1.PNG)

if you look at the `loginHandler` we see that a key value pair is stored in the `localStrage.setItem()` method. This takes those key value pairs and stores them in our browser. if you look at the `useEffect()` method, it's written as an anonymous function. If you see the empty brackets at the end, this means this function hjas no dependencies, meaning that this function will only run once when the app starts. For a login page, this is perfect, considering we dont want to check continually for a login key pair in local storage.

---
</br>

## Adding Dependencies (to stop the loop!)

So let's take a look at adding dependencies to `useEffect()`

![alt-text](/01-starting-project/photo-examples/side-effect-2.PNG)

In this instance, we've added the dependencies `enteredEmail` and `enteredPassword` meaning that if any of these variables change, the `useEffect()` will run again to check the validity of the form via the `setFormIsValid()` method.

This is one example, but of course this could be set for any variable you need to track continually. 

A couple notes:

You DON'T need to add state updating functions (as we did in the last lecture with `setFormIsValid`): React guarantees that those functions never change, hence you don't need to add them as dependencies (you could though)

You also DON'T need to add "built-in" APIs or functions like `fetch()`, `localStorage` etc (functions and features built-into the browser and hence available globally): These browser APIs / global functions are not related to the React component render cycle and they also never change

You also DON'T need to add variables or functions you might've defined OUTSIDE of your components (e.g. if you create a new helper function in a separate file): Such functions or variables also are not created inside of a component function and hence changing them won't affect your components (components won't be re-evaluated if such variables or functions change and vice-versa)

So long story short: You must add all "things" you use in your effect function if those "things" could change because your component (or some parent component) re-rendered. That's why variables or state defined in component functions, props or functions defined in component functions have to be added as dependencies!

---
</br>

# Using Reducers and useReducer()

</br>

Use reducer is used when we need stronger state mangement for elements that depend on each other. It works similarly to the `useState` method. Take a look:

![alt-text](/01-starting-project/photo-examples/reducer-3.PNG)

So let's go back to our login page, here's our first block of code:

![alt-text](/01-starting-project/photo-examples/reducer-1.PNG)

so in our `emailReducer()` arrow function that we've attached to our reducre hook before, `state` and `action` come default. The `state` refers to the latest state of our value, and the `action` to the attribute we assign our input. The very last return statement is our default state in which we'll set the value types for each condition, like this:

![alt-text](/01-starting-project/photo-examples/reducer-2.PNG)

So here we're just doing a couple things in our `emailChangeHandler` arrow function.

- we're calling our `dispatchEmail` hook function to insert an object that has a type (we can name it anything we want), and a value. which we've named "val", and this is pretty much doing the same thing as the code below it keeping track of state. 
</br></br>
---
</br>

# Context API

</br>

The Context API is how we pass information to other components with out having to pass the props from each child component. First we want to create a new file and add it as a component. Like this:

![alt-text](/01-starting-project/photo-examples/context-1.PNG)

So for this module. we're to use the `isLoggedIn` boolean as it's important to multiple components. We use it like this:

![alt-text](/01-starting-project/photo-examples/context-2.PNG)

- First we import `useContext` from react
- then we assign a const variable to a `useContext()` method, in this case, it's the `AuthContext` module in our `auth-context.js` file mentioned in the first screenshot.
  
  So how do we communicate to the rest of the app that the `isLoggedIn` variable has changed? Like this!

  ![alt-text](/01-starting-project/photo-examples/context-3.PNG)

  we use the `<AuthContext.Provider>` tag and wrap our JSX element into it. Then we pass the value in as `isLoggedIn`. We do this because this is the original file in which the login status is kept. So when the `isLoggedIn` status changes, the other modules that include the `AuthContext` module is made aware of the login status as well!
