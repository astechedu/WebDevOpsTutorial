# Javascipt Apis 

[Go To Top](#top)








Different Ways to fetch data from API in Reactjs
Introduction

    In this blog, we will cover the basics of Web API.
    We will try to learn different ways to fetch data from API.
    Let’s begin without any further delay.

Web APIs

API stands for Application Programming Interface. The most popular Web Api used is a Representational state transfer API or RESTful API. Web APIs are used to fetch data from a database and save data back to the database. Using Web APIs requires the use of HTTP request methods there are different HTTP request methods like GET,POST,PUT,DELETE, etc. Let’s have a brief description of the mentioned HTTP request.

    GET: Used to request data from an endpoint
    POST: Sends data to an endpoint
    DELETE: Remove data from an endpoint.
    PUT: Update a record or data value at an endpoint.

Ways of Fetching Data from API

There are different of fetching data:

    By using Fetch API
    By using Axios library
    By using async-await syntax
    By using custom hooks
    By using React Query

1. Fetch API

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

2. Axios

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

4. Using async and await

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

4. Custom Hooks

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

5. React Query

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

Conclusion

In this blog, we have covered different API fetch practices.

In our upcoming blog, we will try to learn about React Hooks.

For more interesting blogs visit- StatusNeo Blogs

Thanks for reading, Ba-Bye for now.
0 Comments
Like
Different Ways to fetch data from API in Reactjs, React, react js, utkarsh chaturvedi blogs, Web Development

Utkarsh Chaturvedi

I am always eager to learn new tech stacks to overcome my challenges in every field. I love playing games, bike riding, and recharging in nature.
Utkarsh Shukla blogs	
A complete guide to SQL from scratch
May 15, 2022
Utkarsh Shukla blogs	
How to do Database Designing
May 22, 2022
Related Posts


