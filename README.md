# Journal-App

![Blogpage1](https://user-images.githubusercontent.com/61579772/84015389-58f3d580-a9ae-11ea-9ab4-fa1d748dca83.jpg)

- This simple app let's you compose,view and edit journals in real time.
- An intermediate tutorial guide for using MongoDB,Express, NodeJs to create your own journling app.
- At the end of this you should be able to set up and deploy your own app on Heroku or Netifly.You'll get familiar using Node.JS,Express,Lodash and a couple of tricks up your sleeve too.

## What You'll Learn🤷‍♂️
- How to configure and setup NodeJS to a MongoDb Database
- Integrate Mongoose 
- Integrate Express.Js-Node web framework
- Routing parameters
- What is Lodash and Body parser
- Deploying your own app


# Introduction
## Step 1 
> Setting up your local environment.
#### Install Node.js
First, make sure you have a supported version of Node.js installed 
- https://nodejs.org/en/download/

#### Install the MongoDB Node.js Driver
The MongoDB Node.js Driver allows you to easily interact with MongoDB databases from within Node.js applications. You’ll need the driver in order to connect to your database and execute the queries.
- npm install mongodb 
- yarn install mongodb

#### Create a free MongoDB Atlas cluster ✔
The documentation is really great refrence source and guide if you choose this option.
-https://docs.atlas.mongodb.com/getting-started/
![Cluster](https://user-images.githubusercontent.com/61579772/84018832-0ff25000-a9b3-11ea-97e8-70c9f236fe5e.jpg)

- This is how everything should look like after yoou finished setting up your cluster with some test data.
- You🤔: Where did the data come from ?
- Me 🧐: We have a backend server that allows us to connect to our cluster using Node.js and Express.
- You🤒: Sounds complex,Could you break it down?


## Step 2 
-Now we are all set up.Two more things to do to initialize our project.
a) Pop up your command line interface. 
- > Mongod -This command is simply to start  your database
- > Mongo- This command provides a powerful interface for system administrators.
b)
- Set up your project folder to resemble the folder structure below
![HOme view](https://user-images.githubusercontent.com/61579772/84022777-66628d00-a9b9-11ea-97ac-19f746ca91c8.jpg)

c)
-Set Up our App.js which is the entry point of our app.
```
//jshint esversion:6

const express = require("express");
const bodyParser = require("body-parser");
const ejs = require("ejs");
const mongoose = require('mongoose');

const app = express();
app.set('view engine', 'ejs');

app.use(bodyParser.urlencoded({ extended: true }));
app.use(express.static("public"));

mongoose.connect("mongodb+srv://admin-name:12345678@cluster0-abcd.mongodb.net/blogDB", { useNewUrlParser: true });

let port = process.env.PORT;
if (port == null || port == "") {
    port = 3000;
}
app.listen(port, function() {
    console.log("Server started on port 3000");

});

```
- You🤔: Bro what doesall this boilerplate code do?
- Me 🧐: The first 4 lines basically require dependeacies for our projects (Express,Body-parser,EJS,Mongoose)
- Me 😏: We later tell our app to use this 4 dependacies and then we connect our database cluster using Mongoose.
- You🤨:```mongoose.connect("mongodb+srv://admin-name:12345678@cluster0-abcd.mongodb.net/blogDB"```
- You🧐: Where did you get this stuff up here?
- Me 😄: Ooh this stuuff comes from our Atlas account.
- Me 😏: Open your Atlas Dashboard and you should see a connect button.

![connext](https://user-images.githubusercontent.com/61579772/84020788-facaf080-a9b5-11ea-90b0-2998df1e8b9a.jpg)

- Me 😎: Now select ```Connect with MongoShell ```
- Me : Copy the code generted for you and now let's paste it in our project and move on to the next step.

## Step 3
- a) On our app.js let's create a schema for our journal posts.
- b)Our journal will contain many posts.Each with a title  and some content.
```
const postSchema = {
    title: String,
    content: String
};

const Post = mongoose.model("Post", postSchema);

```
- b) Let's define some logic on how our App should look like when you go to the home route ("/")

```app.get("/", function(req, res) {
    Post.find({}, function(err, posts) {
            res.render("home", { posts : posts });
    });
});
```

- You🤔: Where is the Front-end of this stuff,it's abit confusing.
- Me 🧐: We set up a folder earlier under views.We named this folder Partiasls.

![HOme view](https://user-images.githubusercontent.com/61579772/84022414-cad11c80-a9b8-11ea-992e-9293a7f60ba8.jpg)

- You🤔: What the #### is happening here.
- You 🧐: We have alot of non-html code in here and my linter is blowing up with errors
- You🤔: Maybe I should look for an easier tutorial to follow 
- Me 🧐: Relax bro!
- Me 😄: Let's break it down.
- Me 😏: When creating a Node applications, an easy and fast way to template our application is sometimes necessary. 
- Me 😏:When it comes to templating,EJS is one alternative that does that job well and is very easy to set up.
- You🤔: Now ,I understand why we did this ```const express = require("express");``` in the begining.
- You🤔: ```<%- include("partials/header"); -%>``` What about this thing here.
- Me 😄: This is EJS syntax and it's basically saying that there is a file in partials containing our header let's include it here.
- Me 🧐: Make's it easier to reuse our components otherwise we would need to style a header and footer for each page.

## Step 4

![Compose](https://user-images.githubusercontent.com/61579772/84024881-3ddc9200-a9bd-11ea-910a-70e178fc139f.jpg)

We created a form to add posts to our Journal.

### Conclusion
I hope at the end of this you were able to set up your local environment and set up a simple database using MongoDB and NodeJs.
- Perform basic CRUD operations
- Start Living Healthy and eat fruits. 😋

### References❤
- 1.https://docs.mongodb.com/manual/reference/mongo-shell/#mongo-shell-command-history
- 2.https://stackoverflow.com/questions/4883045/mongodb-difference-between-running-mongo-and-mongod-databases
- 3.https://mongoosejs.com/
- 4.https://www.mongodb.com/blog/post/quick-start-nodejs-mongodb--how-to-get-connected-to-your-database


## Alternative
### Download Robo 3T
This is a GUI and IDE for developers and data engineers who work with MongoDB. Data management features such as in-place editing and easy database connections(In this case I used Robo 3T for convinience and simplicity)

![Blogpage2](https://user-images.githubusercontent.com/61579772/84015390-598c6c00-a9ae-11ea-989a-980925242c04.jpg)

