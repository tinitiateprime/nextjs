
# Next.js 

© TINITIATE.COM
[Back To Context](README.md) 
# API Routes in Next.js 
 
- Next.js allows developers to build **API routes**  as part of their application. These routes are **serverless functions**  that allow you to handle backend logic without needing a separate server. You can create API routes for handling tasks like database access, form submissions, authentication, and more, directly within the Next.js application.

## Key Concepts for API Routes: 
**1. Creating API Routes**  
- API routes in Next.js are stored in the `pages/api/` directory. Each file in this directory represents a different API endpoint, and the file name determines the route.
 
- **Example** : Creating an API route to return a JSON message:


```Copy code
# File path: pages/api/hello.js
```


```Copy code
// pages/api/hello.js
export default function handler(req, res) {
  res.status(200).json({ message: 'Hello from Next.js API route!' });
}
```
 
- To access this API route, navigate to `http://localhost:3000/api/hello`, and you’ll see the JSON response:


```Copy code
{
  "message": "Hello from Next.js API route!"
}
```
**2. Handling HTTP Methods**  
- Each API route can handle different HTTP methods such as `GET`, `POST`, `PUT`, `DELETE`, etc. You can inspect the `req.method` to determine which method is being used and handle requests accordingly.
 
- **Example** : Handling both **GET**  and **POST**  requests:


```Copy code
# File path: pages/api/greet.js
```


```Copy code
// pages/api/greet.js
export default function handler(req, res) {
  if (req.method === 'GET') {
    res.status(200).json({ message: 'Hello, this is a GET request!' });
  } else if (req.method === 'POST') {
    const { name } = req.body;
    res.status(200).json({ message: `Hello, ${name}! This is a POST request.` });
  } else {
    res.status(405).json({ message: 'Method Not Allowed' });
  }
}
```
 
- **GET Request** : Go to `http://localhost:3000/api/greet` in your browser, and you’ll receive:


```Copy code
{
  "message": "Hello, this is a GET request!"
}
```
 
- **POST Request** : To make a POST request, you can use a tool like Postman or `fetch()`:


```Copy code
// Sending a POST request with fetch()
fetch('/api/greet', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ name: 'John' }),
})
  .then(res => res.json())
  .then(data => console.log(data));
```

This will return:


```Copy code
{
  "message": "Hello, John! This is a POST request."
}
```
**3. Serverless Functions**  
- **API routes in Next.js are serverless functions** . This means that every time an API route is called, a lightweight function is executed on the server (such as Vercel’s serverless infrastructure). This eliminates the need for you to manage your own backend server.
 
- **Example** : Creating a serverless API route for fetching data from an external API:


```Copy code
# File path: pages/api/jokes.js
```


```Copy code
// pages/api/jokes.js
export default async function handler(req, res) {
  const response = await fetch('https://official-joke-api.appspot.com/random_joke');
  const joke = await response.json();

  res.status(200).json(joke);
}
```
 
- Visiting `http://localhost:3000/api/jokes` will trigger the serverless function, which fetches a random joke from the external API and returns it as a response.


```Copy code
{
  "id": 123,
  "type": "general",
  "setup": "Why don't programmers like nature?",
  "punchline": "It has too many bugs."
}
```
**Benefits of Serverless Functions** : 
- **Scalability** : API routes automatically scale depending on traffic. If no traffic is received, the function doesn’t run, minimizing server costs.
 
- **Ease of Deployment** : You don’t need to set up or maintain a server. These functions are deployed along with your Next.js app (e.g., on Vercel).
 
- **Integration** : They can handle things like interacting with databases, authentication, and third-party APIs easily.

[Back To Context](README.md) 

---

| © TINITIATE.COM | 
| --- | 



