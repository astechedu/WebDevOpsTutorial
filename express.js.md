# Express js 








Installing

Assuming you’ve already installed Node.js, create a directory to hold your application, and make that your working directory.

    mkdir myapp
    cd myapp
    npm init

    entry point: (index.js)


    npm install express


To install Express temporarily and not add it to the dependencies list:

    npm install express --no-save





index.js



      const express = require('express')
      const app = express()
      const port = 3000

      app.get('/', (req, res) => {
        res.send('Hello World!')
      })

      app.listen(port, () => {
        console.log(`Example app listening on port ${port}`)
      })




Running Locally

     index.js  or  app.js  or  server.js
     
     



Express application generator:

     npx express-generator
     npm install -g express-generator
     express
     express -h

Usage: express [options] [dir]

express --view=pug myapp



Then install dependencies:

$ cd myapp
$ npm install

On MacOS or Linux, run the app with this command:

$ DEBUG=myapp:* npm start

On Windows Command Prompt, use this command:

> set DEBUG=myapp:* & npm start

On Windows PowerShell, use this command:

PS> $env:DEBUG='myapp:*'; npm start

Then load http://localhost:3000/ in your browser to access the app.

The generated app has the following directory structure:

.
├── app.js
├── bin
│   └── www
├── package.json
├── public
│   ├── images
│   ├── javascripts
│   └── stylesheets
│       └── style.css
├── routes
│   ├── index.js
│   └── users.js
└── views
    ├── error.pug
    ├── index.pug
    └── layout.pug

7 directories, 9 files






