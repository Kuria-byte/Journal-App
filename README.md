# Journal-App

![Blogpage1](https://user-images.githubusercontent.com/61579772/84015389-58f3d580-a9ae-11ea-9ab4-fa1d748dca83.jpg)

- This simple app let's you compose,view and edit journals in real time.
- An intermediate tutorial guide for using MongoDB,Express, NodeJs to create your own journling app.
- At the end of this you should be able to set up and deploy your own app on Heroku or Netifly.You'll get familiar using Node.JS,Express,Lodash and a couple of tricks up your sleeve too.

Hosted my Journal at 😎 @ https://pacific-savannah-54567.herokuapp.com/compose ,Be sure to have a look.I'm open to suggestions and Improvments.

## What You'll Learn🤷‍♂️
- How to configure and setup NodeJS to a MongoDb Database
- Integrate Mongoose 
- Integrate Express.Js-Node web framework
- Routing parameters.
- What is Lodash and Body parser
- Deploying your own app


# Introduction
## Step 1 
> Setting up your local environment.
#### Install Node.js
First, make sure you have a supported version of Node.js installed 
- https://nodejs.org/en/download/

#### Install the MongoDB Node.js Driver
- npm install mongodb 


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
- a) Pop up your command line interface. 
- > Mongod -This command is simply to start  your database
- > Mongo- This command provides a powerful interface for system administrators.
- b)
- Set up your project folder to resemble the folder structure below
![File structrure](https://user-images.githubusercontent.com/61579772/84025284-dd9a2000-a9bd-11ea-9e4f-db1e61fdebb1.jpg)
- c)
Inside our project folder remeber to use the following dependancies
``` {
  "name": "ejs-challenge",
  "version": "1.0.0",
  "description": "",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "body-parser": "^1.18.3",
    "ejs": "^2.6.1",
    "express": "^4.16.3",
    "lodash": "^4.17.11",
    "mongoose": "^5.3.6"
  }
}
```
d)
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
- What to look out for while creating a form
- [x] Your form has a POST method
- [ ] Your button has a type
- [ ] Our textArea,Input and Buttons have names that will uniqely identify them.

## Step 5
At this point if you headback to your app.js and start the server a few things should happen.
- You🤔: What should happen
- Me 🧐: Wuld be able to go to our Compose route on the browser and view the Compose page.
- You🤔: Nothing special about that
- Me 🧐: I agree let's hook up some code and make some post request to add some data.

```
app.get("/compose", function(req, res) {
    res.render("compose");
});

app.post("/compose", function(req, res) {
    const post = new Post({
        title: req.body.postTitle,
        content: req.body.postBody
    });

    post.save(function(err) {
        if (!err) {
            res.redirect("/");
        }
    });
});
```
- You🤔: So what is happening up here
- Me 🧐: We are creating an Object assigning it to a constant.
- Me 🤔: This Object will contain the contents of our post ccapturedd from our Compose form.
- Me 🧐: Once the user hits the compose button,the post get's saved in our databse and we get redirected back home.
- Me 🧐: In order to read HTTP POST data , we have to use "body-parser" node module.
- You🤔: So what is body parser?
- Me 🧐: Body-parser is a piece of express middleware that reads a form's input and stores it as a javascript object accessible through ```req.body```

## Step 6
We are almost done a few more tweaks and you'll be ready to deploy your app.

- a)Finsih the rest of your app by adding the about and contacts Page.
- b)A small hack ,you could hard home,contact and about content for now.So that we wouldn't have to worry about creating different schemas for this individual content

```
app.get("/about", function(req, res) {
    res.render("about", { aboutContent: aboutContent });
});

app.get("/contact", function(req, res) {
    res.render("contact", { contactContent: contactContent });
});

```
# Deploying our App
- Me 🧐: Time to move from local host and meet Heroku
- You🤔: My app is working fine here no need to complicate everything.
- Me 🧐: I guess I have to move on with the courageous ones!

### What we need to ddeploy our app
- 1)[ ] Heroku Account-https://www.heroku.com/
- 2)[ ] Understand basic Git commands
- 3)[ ] Configure our app to run in different environment
- 4)[ ] Procfile
- 5)[ ] npm install heroku CLI
- 6)[ ] Read this heroku deployment tutorial.https://devcenter.heroku.com/articles/deploying-nodejs#:~:text=Run%20the%20npm%20install%20command,json%20file.&text=Start%20your%20app%20locally%20using,part%20of%20the%20Heroku%20CLI.&text=Your%20app%20should%20now%20be,http%3A%2F%2Flocalhost%3A5000%2F.

Once all this is set up lets proceed.
```
git init
git add .
git commit -m "My first commit"
heroku login

Enter your Heroku credentials.
...
heroku create
Git remote heroku added
git push heroku master
```
- Me 🧐: I know you followed up through till this point and maybe are still encounteeing some errors
- You🤔: Can you read my brain or something ?
- Me 🧐: That my friend is called programming,you can't escape the process all you could do is atleast enjoy and love the journey.
- Me 🧐: Solve your bugs,slowly this are the hidden gems to learning new concepts.


### Conclusion
I hope at the end of this you were able to deploy your app to heroku and have learned a couple of new things.
- Me 🧐: You can view my app here @https://pacific-savannah-54567.herokuapp.com/compose.

### References❤
- 1.https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/Introduction
- 2.https://scotch.io/tutorials/use-ejs-to-template-your-node-application
- 3.https://mongoosejs.com/
- 4.https://www.mongodb.com/blog/post/quick-start-nodejs-mongodb--how-to-get-connected-to-your-database


