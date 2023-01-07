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
     
     




