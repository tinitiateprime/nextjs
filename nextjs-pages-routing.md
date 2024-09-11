# Next.js 

© TINITIATE.COM
[Back To Context](README.md) 
# Pages and Routing in Next.js 
 
- One of the key features of Next.js is its **file-based routing system** . This means that every file you create inside the `pages/` directory automatically becomes a route in the application. Next.js also supports **dynamic routes** , allowing for flexible and dynamic URL structures.

## Key Concepts in Pages and Routing: 
**1. File-based Routing**  
- In Next.js, each file inside the `pages/` directory is automatically mapped to a route based on its file name. You don't need to configure a router manually, as Next.js takes care of this for you.**Example** : 
  - A file named `pages/index.js` corresponds to the root route (`/`).
 
  - A file named `pages/about.js` corresponds to the `/about` route.
 
- **Example Structure** :


```Copy code
my-next-project/
├── pages/
│   ├── index.js        # Maps to '/'
│   ├── about.js        # Maps to '/about'
│   └── contact.js      # Maps to '/contact'
```

With this structure:
 
- Navigating to `http://localhost:3000/` will render the `index.js` page.
 
- Navigating to `http://localhost:3000/about` will render the `about.js` page.
 
- **Example Code**  for `pages/about.js`:


```Copy code
// pages/about.js
export default function About() {
  return (
    <div>
      <h1>About Us</h1>
      <p>This is the About page of our Next.js application.</p>
    </div>
  );
}
```
**2. Dynamic Routes**  
- Next.js supports **dynamic routes** , which are useful when you need to create pages for dynamic content, such as product pages, user profiles, or blog posts where the URL can change based on the data (e.g., `/products/123`, `/user/john`).
 
- To create a dynamic route, you can use square brackets (`[]`) in the file name within the `pages/` directory.**Example** : 
  - A file named `pages/products/[id].js` can handle routes like `/products/1`, `/products/2`, etc., where `id` is a dynamic parameter.
 
- **Example Code**  for a dynamic route (`[id].js`):


```Copy code
# File path: pages/products/[id].js
```


```Copy code
// pages/products/[id].js
import { useRouter } from 'next/router';

export default function Product() {
  const router = useRouter();
  const { id } = router.query;  // 'id' comes from the dynamic route

  return (
    <div>
      <h1>Product {id}</h1>
      <p>This page displays the details for product {id}.</p>
    </div>
  );
}
```
In this example, visiting `http://localhost:3000/products/123` will display:

```Copy code
Product 123
This page displays the details for product 123.
```
The `useRouter` hook from Next.js gives access to the `router.query` object, which contains the dynamic parameters (in this case, `id`).**3. Nested Dynamic Routes**  
- You can also create nested dynamic routes, which are helpful for representing complex URL structures like `/users/[userId]/posts/[postId]`.**Example Structure** :

```Copy code
pages/
├── users/
│   └── [userId]/
│       └── posts/
│           └── [postId].js   # Maps to /users/:userId/posts/:postId
```
**Example Code**  for nested dynamic route:

```Copy code
# File path: pages/users/[userId]/posts/[postId].js
```


```Copy code
import { useRouter } from 'next/router';

export default function Post() {
  const router = useRouter();
  const { userId, postId } = router.query;  // 'userId' and 'postId' from the dynamic route

  return (
    <div>
      <h1>User {userId}</h1>
      <h2>Post {postId}</h2>
      <p>This page displays the post {postId} by user {userId}.</p>
    </div>
  );
}
```
Now, visiting `http://localhost:3000/users/10/posts/5` will display:

```Copy code
User 10
Post 5
This page displays the post 5 by user 10.
```
**4. Linking Between Pages**  
- Use the `Link` component from Next.js to navigate between pages without full page reloads.**Example** : Linking from the home page to the about page:

```Copy code
# File path: pages/index.js
```


```Copy code
import Link from 'next/link';

export default function Home() {
  return (
    <div>
      <h1>Home Page</h1>
      <Link href="/about">
        <a>Go to About Page</a>
      </Link>
    </div>
  );
}
```
 
- This will create a seamless transition from the **Home**  page to the **About**  page.
[Back To Context](README.md) 

---

| © TINITIATE.COM | 
| --- | 


---