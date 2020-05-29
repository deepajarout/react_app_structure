# react_app_structure

**CRUV(Containers, Routes, Utils, Views): Structure React apps in 4 directories and 3 files**
Creating a CRUV app is simple. All you do is generate an app with create-react-app, and then create 4 folders and 2 files. You can try it out by copying and pasting this into your terminal:
```terminal

create-react-app myapp
cd myapp/src
mkdir containers routes utils views
touch config.js contexts.js 
mv App.* routes
sed -i '' -e 's/.\/App/.\/routes\/App/g' index.js

```
**But what do the 4 directories and 2 files in this structure actually do?**

# /containers

This directory contains reusable container components. These components handle business logic, delegate style/markup to view components, and importantly, are used in more than one place.
Container components can also communicate with the server. In larger apps, they may delegate this to a Redux or Apollo store. But in smaller apps, they’ll usually just call the server directly.

# /routes
Routes are general purpose components that are only used once. They can handle both business logic and presentation internally, or they can delegate it to containers or presentation components.

# /utils
This is the place to put files that get copied and pasted between many different projects. Things like vanilla JavaScript functions and classes, higher order components, and other utilities.

# /views
Put components that render markup and styles here, along with components that receive and display user input.Dan Abramov calls them presentational components. I call them “views”, because it’s faster to type within import statements.I tend to start by creating one .js, .css and .test.js file per component, and putting them directly in the /views directory.

# /config.js
Apps often have configuration that differs depending on the environment. For example, an API_KEY environment variable that differs between development, staging and production. While you can access this kind of configuration directly from process.env, I prefer to export it from a top-level config.js file. For example:

```javascript
export default {
  server: process.env.REACT_APP_SERVER || 'http://localhost:3000',
  publicURL: process.env.PUBLIC_URL,
  stripeKey: process.env.REACT_APP_STRIPE_KEY,
}
```
# /contexts.js
To use React’s Context API, you’ll frequently need to import <Context.Consumer /> components, which often don’t fit in any of the other categories. I like to keep these components in a single top-level file, making them easy to access, and also discouraging over-use of context. Here’s an example:

```javascript
import * as React from 'react'

// Current route and methods for interacting with browser history
export const NavContext = React.createContext(undefined)

// Data received from server
export const StoreContext = React.createContext(undefined)

// UI context, including whether the subtree is disabled, is a form, etc.
export const UIContext = React.createContext(undefined)

```
# /index.js

This is your application’s entry point, as created by create-react-app!

**But where do my reducers go?**
Article by one of the creators of **Redux: You Might Not Need Redux**.
The reason that there are no /reducers or /actions directories in the **CRUV structure** is that Redux is optional.
But what if you do use Redux? Or MobX? Or Govern? In that case, recommendation is that you add a **/store** directory, and put all your store related code in there. Stores hold global state that isn’t tied to a specific component, so they generally shouldn’t be very large.


 **James K Nelson article**
