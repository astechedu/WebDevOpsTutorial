# Javascipt Apis 

<a name="top"></a>


Topics:



[Different Ways to fetch data from API in Reactjs](#)

1. [Fetch Api](#fetch_api)

2. [Axios Library](#axios_library)

3. [async-await](#async_await)

4. [Custom Hoks](#custom_hooks)

5. [React Query](#react_query)




[Different Ways to fetch data from API in Vuejs](#)


1. [Fetch Api](#fetch_api1)

2. [Axios Library](#axios_library1)

3. [async-await](#async_await1)

4. [Custom Hoks](#custom_hooks1)

5. [React Query](#react_query1)






# Different Ways to fetch data from API in Reactjs


Introduction

    In this blog, we will cover the basics of Web API.
    We will try to learn different ways to fetch data from API.
    Let’s begin without any further delay.



Web APIs

API stands for Application Programming Interface. The most popular Web Api used is a Representational state transfer API or RESTful API. Web APIs are used to fetch data from a database and save data back to the database. Using Web APIs requires the use of HTTP request methods there are different HTTP request methods like GET,POST,PUT,DELETE, etc. Let’s have a brief description of the mentioned HTTP request.

    GET   : Used to request data from an endpoint
    POST  : Sends data to an endpoint
    DELETE: Remove data from an endpoint.
    PUT   : Update a record or data value at an endpoint.


Ways of Fetching Data from API

There are different of fetching data:

    By using Fetch API
    By using Axios library
    By using async-await syntax
    By using custom hooks
    By using React Query






[Go To Top](#top)
<a name="fetch_api"></a>
# 1. Fetch API

We can fetch data by using javascript fetch() method. It will request sever and load the information on the web pages. It will return a promise.

Let’s start with the example. We will create a fetchData() method. It will call fetch() the method with the given URL then converts the result to a JSON object.


                    import React, { useEffect, useState } from "react";

                    function App() { 
                      const [user, setUser] = useState([]);

                      const fetchData = () => {
                        return fetch("https://jsonplaceholder.typicode.com/users")
                              .then((response) => response.json())
                              .then((data) => setUser(data));
                      }

                      useEffect(() => {
                        fetchData();
                      },[])

                      return (
                        <main>
                          <h1>User List</h1>
                          <ul>
                            {user && user.length > 0 && user.map((userObj, index) => (
                                <li key={userObj.id}>{userObj.name}</li>
                              ))}
                          </ul>
                        </main>
                      );
                    }

                    export default App;






[Go To Top](#top)
<a name="axios_library"></a>
# 2. Axios

Axios is a javascript library that we use to make HTTP requests same as fetch(). There is a difference between these two as in fetch() we have to convert the result to a JSON object but in Axios it already returns the result as a JSON object, so we don’t need to convert it.

Let’s take the example of Axios library. First, we have to install the Axios library then we have to import Axios from Axios.


         npm install axios


                import axios from "axios";

                const fetchData = () => {
                    return axios.get("https://jsonplaceholder.typicode.com/users")
                          .then((response) => setUser(response.data));
                  }

                  useEffect(() => {
                    fetchData();
                  },[])






[Go To Top](#top)
<a name="async_await"></a>
# 3. Using async and await

We use Async-Await as it is an asynchronous technique that is operated via an event loop. Async functions will always return a value. It is the preferred way of fetching the data from an API as it enables us to remove our .then() callbacks and return asynchronously resolved data. In the async block, we can use Await function to wait for the promise.

            async function fetchData() {
                try {
                  const response = await axios.get("https://jsonplaceholder.typicode.com/users")
                  setUser(response.data)
                } catch (error) {
                  console.error(error);
                }
              }

              useEffect(() => {
                fetchData();
              },[])





[Go To Top](#top)
<a name="custom_hooks"></a>
# 4. Custom Hooks

Let’s have a brief understanding that what are custom hooks. So, we use custom hooks when we have a component logic that can be used by other components in our application. It is basically a React functional component whose name will start with “use” like useFetch. Custom Hooks can use one or more React hooks inside them.

We also have a React library React-Fetch-Hook for fetching data from API. This library has several properties that we can use like data it will give us data fetched from API, the error we use this for handling errors, and isLoading is used for loading.

Firstly we have to install that library for use that by

            npm i react-fetch-hook


            import useFetch from "react-fetch-hook"

            const {data} = useFetch("https://jsonplaceholder.typicode.com/users");
            console.log(data);

            Now, we will create our custom hook useFetch.

            useFetch.js

            import { useEffect, useState } from "react";
            import axios from "axios";

            const useFetch = (method, url, body) => {
              const [isLoading, setIsLoading] = useState(false);
              const [apiData, setApiData] = useState([]);
              const [apiError, setApiError] = useState('');

              useEffect(() => {
                setIsLoading(true);
                const fetchData = async () => {
                  try {
                    const response = await axios({
                      method: method,
                      url: url,
                      data: body
                    });
                    const data = await response?.data;

                    setApiData(data);
                    setIsLoading(false);
                  } catch (error) {
                    setApiError(error);
                    setIsLoading(false);
                  }
                };

                fetchData();
              }, [url, method, body]);

              return { isLoading, apiData, apiError };
            };

            export default useFetch;



App.js


            import useFetch from "../src/useFetch";

            function App() { 
              const { isLoading, apiError, apiData } = useFetch(
                "GET",
                "https://jsonplaceholder.typicode.com/users",
                {}
              );






[Go To Top](#top)
<a name="react_query"></a>
# 5. React Query

For optimizing the request operations in our application we use React Query library which helps us to handle complex application caching. It is far simpler to write in React Query than React-Redux. It performs pre-fetching of data so that the application can update stale data in the background.

So for using React Query first we have to install React Query library by.

            npm i react-query

So to configure react-query in our React.js application, we need to wrap our components with the QueryClientProvider component. We will do configuration in our root directory file index.js.



            import React from "react";
            import ReactDOM from "react-dom";
            import { QueryClient, QueryClientProvider } from "react-query";
            import App from "./App";

            const queryClient = new QueryClient();

            const rootElement = document.getElementById("root");
            ReactDOM.render(
              <React.StrictMode>
                <QueryClientProvider client={queryClient}>
                  <App />
                </QueryClientProvider>
              </React.StrictMode>,
              rootElement
            );


Let’s see how we fetch data by useQuery

First, we have to import useQuery from react-query. The useQuery hook returns some states that we can use in our application like isLoading, data, error, Is Error,


            import React, { useState } from "react";
            import { useQuery } from "react-query";
            import axios from "axios";

            function App() {
              async function fetchUser() {
                const { data } = await axios.get(
                  "https://jsonplaceholder.typicode.com/users"
                );
                return data;
              }

              const { data, error, isError, isLoading } = useQuery("getUser", fetchUser);

              return (
                <main>
                  <h1>User List</h1>
                  <ul>
                    {data &&
                      data.length > 0 &&
                      data.map((userObj, index) => (
                        <li key={userObj.id}>{userObj.name}</li>
                      ))}
                  </ul>
                </main>
              );
            }

            export default App;



We will create a functional component and import useQuery in that. Then we will create an async function fetchUser() that will return an array of users.
For updating data, we use useMutation hook

So, we use a mutation hook for doing operations like Create, Update, Delete in our components. We will pass the payload as parameters in our mutate function after our async call is done, we will be passed to onSuccess where we can invalidate query that we used for fetching data so that we can get updated data after update into the database.

First, we will see how to use useMutation,



            import React, { useState } from "react";
            import { useQuery, useMutation } from "react-query";
            import axios from "axios";

            function App() {
              async function addUser(payload) {
                return await axios.post(
                  "https://jsonplaceholder.typicode.com/users",payload
                );
              }

              const {mutate : createNewUser} = useMutation(addUser, {
                onSuccess: () => {
                  console.log('success')
                },
              });

              return (
                <main>
                  <h1>User List</h1>
                  <button onClick={() => {
                      createNewUser({
                        id: Date.now(),
                        userName: 'New User',
                      });
                    }}>Add User</button>
                </main>
              );
            }

            export default App;



So now we will invalidate our fetch query in onSuccess. First, we have to declare a new query client to have access to the cache.



            import React, { useState } from "react";
            import { useQuery, useMutation ,useQueryClient} from "react-query";
            import axios from "axios";

            function App() {
              const queryClient = useQueryClient();

              async function addUser(payload) {
                return await axios.post(
                  "https://jsonplaceholder.typicode.com/users",payload
                );
              }


              const {mutate : createNewUser} = useMutation(addUser, {
                onSuccess: () => {
                  queryClient.invalidateQueries('getUser');
                },
              });



So, in invalidateQueries, we are passing fetch query name (‘getUser’) that will fetch the data.


:end:










# How to Interact With an API from a Vue.js Application

 API

A lot of developers build applications using JavaScript and this constitutes the fact that most web applications have JavaScript as one of their main programming languages. JavaScript frameworks were built to make the development process easier and quicker for developers. Vue.js is one of many popular JavaScript frameworks. Others of which include React and Angular.
What is Vue.js

Vue.js is a progressive framework for JavaScript which is used to develop interactive user interfaces. Vue.js is called a progressive framework because it is user-friendly and can be easily merged with different frameworks or libraries.

When developing most projects using Vue.js, there’ll be a need to fetch or consume data from an API. This is used to make the front-end interact with the back-end of the application. The fetched data can then be consumed on the front-end of the application.
What is an API?

API stands for Application Programming Interface, which is a set of protocols that allow applications to share data. It’s more of a software intermediary. To use APIs in Vue.js, you’ll have to make an API request using either one of these methods: Axios or Fetch methods.

These concepts will be discussed extensively in the course of this article.
Prerequisites

To understand and follow this article, you should have:

    Node.js installed on your computer.
    Vue.js installed on your computer. If you don’t already have it installed, refer to the documentation.
    Understood the key concepts in Vue.js. You can learn them from this Vue.js guide.

Overview

    Using Axios to consume an API
    Using the Fetch API method
    Using APIs in Vuex
    

If you don’t know how to create a Vue project, check out this documentation to walk you through the process.


# Using Axios to consume APIs

Axios is a promise-based HTTP client which makes it suitable for fetching data during server-side display. It works on both browser and Node apps. Axios is a library that is built around the Fetch API.
Axios Installation

To use Axios in your project, you should install it. This can be done in two ways:

    By using npm; a standard package manager for the JavaScript runtime environment Node.js. You can now see why having Node.js installed on your computer was a prerequisite.

    By using yarn; a package manager that also acts as a project manager. It is synergetic with the npm registry and has the same features. To install yarn in your project, paste the following line of code in your terminal npm install --global yarn

With npm:

`           npm i axios

With yarn:

             yarn add axios

Next, you should import Axios in your src/main.js file


            import axios from 'axios';
            Vue.prototype.$http = axios;


How to make an API request and display data using Axios

Now, we’ll make our first API request using the GET method. A GET method is used to fetch data from an API. We want this API request running asynchronously therefore, we use a promise-based function with the keywords async/await.

You may wonder why we used a promise-based function. This is because a promise is a stand-in for a value not necessarily known when the promise is created. Since API requests take an undeterminable amount of time, we use promises. You can learn more about Promises in the MDN docs.

We also need to test for errors using the try/catch method. try is used to check for errors while catch is used to handle the error if one occurs.

Copy the code below to your App.vue file:


        <template></template>

        <script>
        export default {
          data() {
            return {
              posts: [],
            };
          },

          methods: {
            async getData() {
              try {
                const response = await this.$http.get(
                  "http://jsonplaceholder.typicode.com/posts"
                );
                // JSON responses are automatically parsed.
                this.posts = response.data;
              } catch (error) {
                console.log(error);
              }
            },
          },
        };
        </script>

The above block of code in the methods property will be explained line by line.


        async getData (){


Here a function named getData() is created. In this function, the API will be called. The async keyword is prepended on the getData function to show that the function will make use of promises and we’ll be using it to await to pause the execution of the function until the promise is resolved.


        try {
            const response = await this.$http.get('http://jsonplaceholder.typicode.com/posts');


try property defines a block of code to be tested for errors as the code is executed. In the block of code const response = await this.$http.get('http://jsonplaceholder.typicode.com/posts');, a get request is made with the get keyword using axios i.e.$http to get data from the URL.

await is prepended to the request because the get function will return a promise. The data returned from the API after the promise is resolved and will be stored in the variable response.

            this.posts = response.data

The data we get from the request is then saved to the posts array which is created in the data property.

            catch (error) {
                console.log(error);
            }

If any error occurs during the execution, the error will be caught and logged in the console.

After requesting data from the API, you will need to call it on a lifecycle hook. Here we will use the created() lifecycle hook, this is because we will be able to retrieve sensitive data and events that are active with the created hook.



        <template></template>

        <script>
        export default {
          data() {
            return {
              posts: [],
            };
          },

          methods: {
            async getData() {
              try {
                const response = await this.$http.get(
                  "http://jsonplaceholder.typicode.com/posts"
                );
                // JSON responses are automatically parsed.
                this.posts = response.data;
                console.log(posts);
              } catch (error) {
                console.log(error);
              }
            },
          },

          created() {
            this.getData();
          },
        };
        </script>


We can now display the data in the template by looping through the posts using v-for directive.


        <template>
          <div>
            <div v-for="post in posts" v-bind:key="post.id">
              <h2>{{ post.title }}</h2>
              <p>{{ post.body }}</p>
            </div>
          </div>
        </template>

        <script>
        export default {
          data() {
            return {
              posts: [],
            };
          },

          methods: {
            async getData() {
              try {
                const response = await this.$http.get(
                  "http://jsonplaceholder.typicode.com/posts"
                );
                this.posts = response.data;
              } catch (error) {
                console.log(error);
              }
            },
          },

          created() {
            this.getData();
          },
        };
        </script>



# Using Fetch API method



Fetch API is a powerful and flexible method of flexible APIs. It produces a global fetch() method that provides a simple and rational way to fetch resources asynchronously over the network.

To request with the Fetch API, you just have to make the request directly with the fetch object and follow all other steps used in the Axios call above.

        <template>
          <div>
            <ul v-for="post in posts" v-bind:key="post.id">
              <li>{{ post.title }}</li>
              <p>{{ post.body }}</p>
            </ul>
          </div>
        </template>

        <script>
        export default {
          data() {
            return {
              posts: [],
            };
          },

          methods: {
            async getData() {
              try {
                let response = await fetch("http://jsonplaceholder.typicode.com/posts");
                this.posts = await response.json();;
              } catch (error) {
                console.log(error);
              }
            },
          },

          created() {
            this.getData();
          },
        };
        </script>



# Creating APIs in Vuex


Vuex is a state management library for Vue.js applications. It provides a centralized store for all elements in an application.

Installing Vuex

To make use of Vuex, you will first need to install the Vuex package on your Vue application.

        vue create project

OR

        npm install vuex --save


Then, in your store folder, access the index.js file and write the following code


        import Vue from 'vue'
        import Vuex from 'vuex'
        import axios from "axios";


        Vue.use(Vuex);



Making the API request

We will be working with the store/index.js file. First, we create a state object which will contain all the application-level state. It serves as the data object for the store in a vuex project.


        export default new Vuex.Store({
         state: {
            posts: [],
          },
        }) 


Next, we create a getters property. Getters are like computed properties for stores. It is used to determine derived states based on store states. In this tutorial, we will use it to return posts in the state.


      getters: {
        posts: state => {
          return state.posts;
        }
      },



Next, we create a mutation property. The mutation property is where we can change the state in the Vuex store. There are very similar to events where we carry out actual state alterations.


          mutations: {
            SET_ITEMS (state, posts) {
              state.posts = posts
            }
          },


Now we can call our API in the actions property. Actions are equivalent to mutations only that actions commit mutations rather than mutating the state and also actions can hold asynchronous operations. Let’s go ahead with the API call.



          actions: {
           async loadPosts ({ commit }) {
             try {
                const response = await this.$http.get('http://jsonplaceholder.typicode.com/posts');
                // JSON responses are automatically parsed.
                commit('SET_ITEMS', response.data)
              }
              catch (error) {
               console.log(error);
             }
           }
          },


Now, we should import the store in src/main.js and pass it to our Vue app.



        import store from "../store/index";

        new Vue({
          render: (h) => h(App),
          store,
        }).$mount("#app");



Now, we can display the data in our vue file. To do that, some steps need to be taken:

    Using the computed property, we access the content of the getters method in the store.


        <script>
        export default {
          computed: {
              posts() {
                   return this.$store.getters.posts;
                },
            },


    Call the API on a lifecycle hook created and employ the dispatch method to call the action.


          created() {
            this.$store.dispatch('loadPosts');
          },
        }
        </script>


    Finally display data on your template.


        <template>
          <div>
            <div v-for="post in posts" v-bind:key="post.id">
              <h2>{{ post.title }}</h2>
              <p>{{ post.body }}</p>
            </div>
          </div>
        </template>


Here is the whole code snippet:


For the store file:


        import Vue from 'vue'
        import Vuex from 'vuex'
        import axios from "axios";

        Vue.use(Vuex);


        export default {
          computed: {
            posts() {
                 return this.$store.getters.posts;
              },
          },
          created() {
            this.$store.dispatch('loadPosts');  
          },
        }
        </script>



:end:


[Go To Top](#top)
