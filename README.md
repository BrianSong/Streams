# *Streamy - A simple clone of twitch.tv building by React and Redux*
## This app can allow users to scream their desktop and post to the app, it also have the ability for the users of this app to view all the available streams and create, edit and delete their own streams (This app focus on React/Redux, not any complicated backend pieces).

The challenges of this app:
1. Need to be able to navigate around to separate pages in the app.
2. Need to allow a user to login/logout.
3. Need to handle forms in Redux.
4. Need to master CRUD (Create Read Update Destroy) operations in React/Redux.

Belows are some keypoints that I learned from creating this screams app:
* `react-router-dom` allows negivations between webpages. Compared to tranditional link tag <a herf = ""></a> which is bad for our react/redux app because using these link tags will dump the old HTML and loss all data and variables, `react-router-dom` will prevent the brower to fetch a new HTML file.
