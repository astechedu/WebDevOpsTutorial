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


###### 1. Setting up MongoDB Atlas Nodejs Integration Simplified:


What is MongoDB Atlas?

MongoDB Atlas is a Multi-Cloud Database Service offered by MongoDB that simplifies Database Deployment and Management while providing the flexibility required to build resilient and performant global applications on the Cloud providers of your choice. Atlas provides all of MongoDB’s features while automating database administration tasks such as Database Configuration, Infrastructure Provisioning, Patches, Scaling Events, Backups, and more, allowing developers to focus on what matters the most to them.
Key Features of MongoDB

    Operational Efficiency: MongoDB Atlas comes with built-in operational best practices, that allows the user to focus on delivering business value and accelerating application development rather than managing databases.
    Multi-Cloud Clusters: With MongoDB Atlas’ Multi-Cloud Clusters, you can take advantage of unique tools and services native to all three major Cloud providers (AWS, Google Cloud, and Azure) without adding any unnecessary complexity to your Data Management experience.
    Performance: MongoDB Atlas performs admirably with most of the applications. Since it can be co-located with any Cloud provider of your choice, there is no additional network latency, and the boxes are nicely tuned to ensure MongoDB runs smoothly.



The database industry has undergone a number of changes in recent years, resulting in a greater shift toward a Database as a Service (DBaaS) model versus On-Premise Infrastructure. Most business apps rely on Databases, and Cloud-based DBaaS services provide users with a Flexible, Scalable, and On-demand Platform that eliminates the need to set up costly physical hardware. MongoDB Atlas is one such fully Cloud-based Database Service that hosts your data on MongoDB Instances. On the other hand, the Node.js driver provides an interface for connecting to and communicating with MongoDB Instances. 

Upon a complete walkthrough of this article, you will gain a holistic understanding of MongoDB Atlas and Node JS. This article will also provide you with a step-by-step guide on how to connect to MongoDB Atlas from a Node JS application and set up MongoDB Atlas Nodejs Integration.



What is Node.js?


Node.js is an Open-Source Server-Side Runtime Environment that is solely based on the V8 JavaScript Chrome Engine. It offers an Event-driven, Non-Blocking (Asynchronous) I/O and Cross-Platform runtime environment for developing highly scalable Server-Side JavaScript applications. Node.js can be used to create a variety of applications, including Command-Line Applications, Web Applications, Real-time Chat Applications, REST API Servers, and so on. Its Event-Driven Runtime handles all types of HTTP requests and sleeps when not required. This allows developers to leverage JavaScript and write Server-Side scripts to generate Dynamic Web Content before it is delivered to the user’s web browser. 



Connect to your Database:

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

