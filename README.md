# *Streamy - A simple clone of twitch.tv building by React and Redux*
## This app can allow users to scream their desktop and post to the app, it also have the ability for the users of this app to view all the available streams and create, edit and delete their own streams (This app focus on React/Redux, not any complicated backend pieces).

The challenges of this app:
1. Need to be able to navigate around to separate pages in the app.
2. Need to allow a user to login/logout.
3. Need to handle forms in Redux.
4. Need to master CRUD (Create Read Update Destroy) operations in React/Redux.

Belows are some keypoints that I learned from creating this screamy app:
* **react-router-dom** allows negivations between webpages. Compared to tranditional link tag <a herf = ""></a> which is bad for our react/redux app because using these link tags will dump the old HTML and loss all data and variables, **react-router-dom** will prevent the brower to fetch a new HTML file.
* The true nature of **react-router-dom** is to show and hide differernt sets of components based upon the URL.
* We can use **semantic ui cdn** to handle the styling for our app.
* If we want to add some always visible header, we should add it outside the <BrowerRouter> import from **react-router-dom**.
  However, if the header contains <link to = ""></link> import from **react-router-dom**, it must inside the <div></div> under the <BrowerRouter>.
* As for the authetication, I used **Google OAuth** which can not only capable of identifiation but can also make actions on behalf of users.
* **API** - Application programming Interface can thought as the waiters or messages among different software systems.
* For OAuth, there are OAuth for severs -> actively access the users date for like each 10 mins and OAuth for JS Brower Apps which just handle the login process.
* OAuth client ID is the token for the browser to use to make requests on behalf of the user.
* Since we only want the gapi.load('client:auth2') to be loaded only once when the component first render on th screen, so, I put in into the lifecycle method of React called ComponentDidMount.
* Since the previous loading needs time, so, we can add a callback funtion after the loading process to init the gapi client: gpai.client.init({clientId:..., scope(indicates which parts of the user profile we need to get access to):'email'})
* However, the previous init process is not sync as well, so we add ".then(() = > {this.auth = windows.gapi.auth2.getAuthInstance()})" to get a return object this.auth which can call several functions: .signIn(), .isSignedInget(), .signOut(), .isSignedIn.listen().
* Inside .isSignedIn.listen(), we can pass a callback function which will be called everytime the isSignIn property changes.
* We must combine **Redux Store** inside the authetication component, so, in this way, not only the GoogleAuth component knows the states, all other components know.

