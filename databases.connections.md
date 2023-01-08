# All Databases Connections


<a name="top"></a>

Topics:

1. [MongoDB Connection](#mongodb)
 
3. [Mysql Connection](#mysql)

4. [Sqlite Connection](#sqlite)

5. [sqlserer Connection](#sqlserver)









[Go To Top](#top)
<a name="mongodb"></a>
# MongoDB Database


Setting up MongoDB Atlas Nodejs Integration Simplified:


The database industry has undergone a number of changes in recent years, resulting in a greater shift toward a Database as a Service (DBaaS) model versus On-Premise Infrastructure. Most business apps rely on Databases, and Cloud-based DBaaS services provide users with a Flexible, Scalable, and On-demand Platform that eliminates the need to set up costly physical hardware. MongoDB Atlas is one such fully Cloud-based Database Service that hosts your data on MongoDB Instances. On the other hand, the Node.js driver provides an interface for connecting to and communicating with MongoDB Instances. 

Upon a complete walkthrough of this article, you will gain a holistic understanding of MongoDB Atlas and Node JS. This article will also provide you with a step-by-step guide on how to connect to MongoDB Atlas from a Node JS application and set up MongoDB Atlas Nodejs Integration.




Connect to your Database

    Head back to the home page of MongoDB Atlas and select the Clusters option.
    Now, click on the Connect Your Application option to set up a connection between your application and cluster using MongoDB’s native drivers.
    Select Node.js as the native driver and save the Connection String provided by MongoDB Atlas 

It’s now time to use Mongoose to create your database connection. Install Mongoose in your project by using the npm install mongoose command. Copy and paste the code below into db.js.



//db.js


      const mongoose = require('mongoose')

      const url = `Connection String`;

      const connectionParams={
          useNewUrlParser: true,
          useCreateIndex: true,
          useUnifiedTopology: true 
      }
      mongoose.connect(url,connectionParams)
          .then( () => {
              console.log('Connected to the database ')
          })
          .catch( (err) => {
              console.error(`Error connecting to the database. n${err}`);
          })


    Replace password with your own password and dbname with the name that you would like to give to your database. Once you have successfully executed the above code, you will see a Connected to the Database message on your console.












[Go To Top](#top)
<a name="mysql"></a>
# Mysql Database
















[Go To Top](#top)
<a name="top"></a>
# MongoDB Database













[Go To Top](#top)
<a name="top"></a>
# MongoDB Database


















[Go To Top](#top)
<a name="top"></a>
# MongoDB Database
















[Go To Top](#top)
<a name="top"></a>
# MongoDB Database




:end:








[Go To Top](#top)

