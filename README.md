# Streamy - A simple clone of twitch.tv building by React and Redux
## *This app can allow users to scream their desktop and post to the app, it also has the ability for the users of this app to view all the available streams and create, edit and delete their streams (This app focus on React/Redux, not any complicated backend pieces).*

### The challenges of this app:
1. Need to be able to navigate around to separate pages in the app.
2. Need to allow a user to login/logout.
3. Need to handle forms in Redux.
4. Need to master CRUD (Create Read Update Destroy) operations in React/Redux.

### Below are some key points that I learned from creating this screamy app:
* **react-router-dom** allows navigations between webpages. Compared to traditional link tag <a herf = ""></a> which is bad for our react/redux app because using these link tags will dump the old HTML and loss all data and variables, **react-router-dom** will prevent the browser to fetch a new HTML file.
* The true nature of **react-router-dom** is to show and hide different sets of components based upon the URL.
* We can use **semantic ui cdn** to handle the styling for our app.
* If we want to add some always visible header, we should add it outside the <BrowerRouter> import from **react-router-dom**.
  However, if the header contains <link to = ""></link> import from **react-router-dom**, it must inside the div tag under the \<BrowerRouter>.
* As for the authentication, I used **Google OAuth** which can not only capable of identification but can also take actions on behalf of users.
* **API** - Application Programming Interface can be thought of as the waiters or messages among different software systems.
* For OAuth, there are OAuth for severs -> actively access the users' data for like every 10 mins and OAuth for JS Brower Apps which just handle the login process.
* OAuth client ID is the token for the browser to use to make requests on behalf of the user.
* Since we only want the gapi.load('client:auth2') to be loaded only once when the component first renders on the screen, so, I put in into the lifecycle method of React called ComponentDidMount.
* Since the previous loading needs time, so, we can add a callback function after the loading process to init the gapi client:             gpai.client.init({clientId:..., scope(indicates which parts of the user profile we need to get access to):'email'})
* However, the previous init process is not sync as well, so we add ".then(() = > {this.auth = windows.gapi.auth2.getAuthInstance()})"     to get a return object this.auth which can call several functions: .signIn(), .isSignedInget(), .signOut(), .isSignedIn.listen().
* Inside .isSignedIn.listen(), we can pass a callback function which will be called everytime the isSignIn property changes.
* We must combine **Redux Store** inside the authentication component, so, in this way, not only the GoogleAuth component knows the authentication states, but also all other components.
* Once the user successfully signs or signout, the action creator inside the .isSignedIn.listen()'s callback function will be called,     then the actions will be dispatched and the state inside Redux store will be changed, and all other components can know the user's status.
* mapStateToProps is used if we need to get access to the state properties inside the Redux store inside any components.
* The format for state inside Redux store is state.auth(property come from auth reducer).isSignedIn(key).
* How to call action creators inside a component => connect(mapStateToProps, {action_creator})(component), then we can call               this.props.action_creator.
* As long as we pass mapStateToProps inside a component, once the states inside Redux store is changed, this component will automatically rerender itself.
* After using gapi.auth2.getAuthInstance().currentUser.get().getId() to get userID, we can use this userID to pass it to action creator   as props and we can assign this userID to action.payload.
* **redux-devtools-extension** can debug and check Redux store at any time.
* localhost:3000?debug-sesstion=<some_string> can open the debug mode where the data will lose between refresh the pages. We can name the "same_string" specifically so that we can have the ability to create check points.
* **Redux Form** can do two things for us automatically: 1. change state in Redux store by calling the action creator(then dispatch to the reducer to change states) 2. Pass the changed state back to components by calling mapStateToProps.
* Inside "import {Field, reduxForm} from 'redux-form'", the reduxForm just like connect for react-redux.
* Validation of form inputs: if validate(formValues) return null means all good, if it returns key-value pair, then it means that the     Redux form will show the error. The key should be matched with the <Field> name property.
* If we see the **error**: Cannot read "XXX" of undefined, it is quite like the issues related to "this", change the callback function into arrow function.
* The API server we used inside this app is the **JSON server** which adheres to the REST conventions.
* db.json serves as kind of backend database, and we can make GET, POST, PUT, DELETE request to it.
* We use **"axios"** and **redux-thunk** to write async action creator for URL request.
* We use object instead of string to store the data for the state inside Redux store. WHY? Because object is much easier to add, edit     ... compared to a string. Also remember, a newly created object must be returned.
* nums.map(num => ()) is just like for num in nums: in Python
* We use action creators to create/edit/delete streams where corresponding requests are sent to api server, then, we use different kinds of   reducer to update the state inside the Redux store
* We need to add userID for every stream being created. HOW? Inside the createStream action creator, since we are using redux-thunk middleware, the function automatically being passed with the state inside the redux store which contains the userID in the auth step     before.
* JSX: <div style = {{textAlign: 'right'}}>XXX</div> is to make XXX appears on the right side of the screen. the first {} is to indicate that we want to refer to a JS variable, the second {} is to indicate a normal object.
* There are two kinds of navigation: Intentional (<link>) and programmatic (run code to forcibly navigate the user through the app).
* We should navigate the user after the backend API responses with success or error.
* In order to implement programmatic navigation, we use the **history** object created by the BrowerRouter. However, even though this history object is easy to be referred inside the <BrowerRouter> since it is passed to it as a prop, it is hard to reference inside the action creators. So, we do not use BrowerRouter to create the history object, we will create it on our own using the plain Router.
  Then, we can use the history.push('') to do the programmatic navigation.
* **URL-based selection**: inside/edit/:id, : means id is a variable, and it will be passed into the props.match.params of the page component due to the <Route> system.
* The **ownProps** passed in an argument inside the mapStateToProps can be called in order to get access to the props inside the components as long as the connect() connect the mapStateToProps with the component.
* With React-Router, each component needs to be designed to **work in isolation**, which means to have the ability to fetch its own data inside each component.
* For function react components, use "props"; for class-based react components, use "this.props".
* As long as the state inside the Redux store update, the class-based component wiwll be rerendered as long as it is connected by  connect().
* After import _ from 'lodash', _.pick{someobject, key} can return a specific key-value pair object.
* formValues is all the form information inside Redux form, it can be automatically passed into the onSubmit callback function inside the   <form> in Redux form.
* Since **PUT** request will update all properties, we use **PATCH** which updates only some properties instead.
* **Modal window**: higher **z-index** means higher priority to be showed in the top of the screen. It is very hard for us to use modal 
  window directly inside the normal react system because in that case, the modal window will be deeply nested inside all levels of \<div>, and it is very hard to set appropriate z-index for all of them for letting the modal window show on the toppest of the screen.
  So, we use **portal** because it lets us to render some element not as a direct child, in this way, we can kind of break through the
  nested system and let modal window be a child of the body and assgin a very high z-index to it.
* Use portal for modal window: ReactDOM.createPortal + document.querySelector(#(under the root in index.html))
* EventHandler has a bubble up property, a e.stopPropagation() can be used to stop it.
* We cannot allow to assign multiple JSX elements into a single variable, so we must use div tag to wrap them up.
* We should use onClick = {()=>{some_call_back_func}} instead of onClick = {some_call_back_func}, because without the ()=> arrow 
  function, this callback function will be called automatically for the first time.
* Use switch tag to only show one Route at a time.
* To make the app works, we need all three (npm app + api + RTMP server) on.
* **flv.js** will make the video player inside our app.
* By the set the setting(URL and STREAM-NAME) inside **OBS (open broadcaster software)**, we can pass the stream into the **RTMP**
  server.
* **componentWillUnmount()** will take care of the cleanup process: as long as we navigate away from the streamShow component, the flv
  player is destroyed by it.
* **RTMP server will be in charge of recording the user's desktop together with OBS, it will connect to the JSON server so that the backend API will have a list of all available streams. The users inside the browser will first take a look at the stream list by sending a request to the JSON server, and when they click on some particular stream, the RTMP server will feed the stream to them.**
