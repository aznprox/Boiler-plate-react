# boiler-plate-react

# React App Initial Setup Instructions

1. Create repository on GitHub
    -Initialize README
    -Initialize gitignore 
    -Initialize node

2. Clone repository to drive

3. Open `server.js` file, add the following code, and save:

const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const app = express();

mongoose.Promise = global.Promise;
mongoose.connect(process.env.MONGODB_URI || "mongodb://localhost/happy-choice"); //mongodb://localhost/fullstack-jeopardy

const connection = mongoose.connection;
connection.on('connected', () => {
  console.log('Mongoose Connected Successfully');    
}); 

// If the connection throws an error
connection.on('error', (err) => {  
  console.log('Mongoose default connection error: ' + err);
}); 

app.use(bodyParser.json());


app.use(express.static(__dirname + '/client/build/'));
app.get('/', (req,res) => {
    res.sendFile(__dirname + '/client/build/index.html')
  })

const PORT = process.env.PORT || 3001;
app.listen(PORT, () => {
  console.log("Magic happening on port " + PORT);
})

4. Test by running `node server.js`

5. Commit to GitHub 

6. Run `create-react-app client`

7. Paste the following code into `client/package.json`:

`"proxy": "http://localhost:3001",`

8. Test React.js app by running `node server.js`

9. Commit to GitHub

10. Replace the script code in `package.json` with the following: 

"scripts": {
    "start": "node server.js",
    "dev": "concurrently \"nodemon server.js\" \"cd ./client  && yarn start \" ",
    "test": "echo \"Error: no test specified\" && exit 1",
    "postinstall": "cd client && npm install && npm run build"
  },

11. Test React.js app by running `npm run dev`

12. Commit to GitHub

13. Create Heroku folder by running `heroku create appname`

14. Check if folder is created by running `git remote -v`

15. Open Heroku in browser and go into Resources tab for the folder and add `mLab:Mongod`

16. Test Heroku React.js app through terminal/bash by running `heroku open`