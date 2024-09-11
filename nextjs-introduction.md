# Next.js 

© TINITIATE.COM

[Back To Context](README.md) 
# Introduction to Next.js 
 
- Next.js is a **React framework**  that enables developers to build powerful web applications with features like **Server-Side Rendering (SSR)** , **Static Site Generation (SSG)** , and **API Routes**  out of the box. It streamlines many of the processes required for developing production-ready applications while enhancing SEO, performance, and developer experience.

## Key Concepts in Next.js: 
**What is Next.js?**  
- Next.js is a **full-stack React framework**  that supports both front-end and back-end development, making it easier to create fast, scalable, and optimized web applications. It is built on top of React and enhances its functionality by providing tools and conventions to simplify tasks such as routing, server-side rendering, and static site generation.


```Copy code
// Example of a basic Next.js page
export default function Home() {
  return <h1>Welcome to Next.js!</h1>;
}
```
**Next.js vs React**  
- **Routing** : Unlike React, which requires third-party libraries like `react-router-dom` for routing, Next.js offers **file-based routing**  where every file in the `pages/` directory automatically becomes a route.
 
- **SSR and SSG** : React on its own is a client-side framework, but Next.js provides **Server-Side Rendering**  (SSR) and **Static Site Generation**  (SSG) to enhance performance and SEO.
 
- **API Routes** : Next.js allows you to create backend API routes directly within the same project, something that requires separate configuration in a standard React application.

#### Example: 


```Copy code
// React Example: Setting up routing with react-router-dom
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

function App() {
  return (
    <Router>
      <Switch>
        <Route path="/" component={Home} />
        <Route path="/about" component={About} />
      </Switch>
    </Router>
  );
}
```


```Copy code
// Next.js Example: No routing setup required, automatically routes based on file names
// pages/index.js
export default function Home() {
  return <h1>Home Page</h1>;
}

// pages/about.js
export default function About() {
  return <h1>About Page</h1>;
}
```
**Key Features of Next.js** **1. Server-Side Rendering (SSR)**  
- **Server-Side Rendering**  ensures that the content of a page is generated on the server at each request, providing better SEO and faster first load times for users. This is especially useful for dynamic content that changes frequently.


```Copy code
// pages/posts.js
export async function getServerSideProps() {
  const res = await fetch('https://jsonplaceholder.typicode.com/posts');
  const posts = await res.json();

  return {
    props: {
      posts,
    },
  };
}

export default function Posts({ posts }) {
  return (
    <div>
      <h1>Posts</h1>
      <ul>
        {posts.map(post => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </div>
  );
}
```
**2. Static Site Generation (SSG)**  
- **Static Site Generation**  builds pages at compile time, making them fast to load. This is ideal for content that doesn’t change frequently, such as blog posts or product pages.


```Copy code
// pages/blog.js
export async function getStaticProps() {
  const res = await fetch('https://jsonplaceholder.typicode.com/posts');
  const posts = await res.json();

  return {
    props: {
      posts,
    },
  };
}

export default function Blog({ posts }) {
  return (
    <div>
      <h1>Blog Posts</h1>
      <ul>
        {posts.map(post => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </div>
  );
}
```
**3. API Routes**  
- Next.js allows you to create backend API routes within the `pages/api` directory. These routes are useful for handling backend logic without setting up a separate server.


```Copy code
// pages/api/hello.js
export default function handler(req, res) {
  res.status(200).json({ message: 'Hello from Next.js!' });
}
```
[Back To Context](README.md) 

---

| © TINITIATE.COM | 
| --- | 


---