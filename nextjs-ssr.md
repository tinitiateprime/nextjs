# Next.js 

© TINITIATE.COM

[Back To Context](README.md) 
# Server-Side Rendering (SSR) 
 
- **Server-Side Rendering (SSR)**  in Next.js allows pages to be rendered on the server at each request rather than on the client-side. This is useful for delivering content that changes frequently and improving SEO performance by serving fully-rendered HTML to search engines.

## Key Concepts in SSR: 
**1. Server-Side Rendering Overview**  
- **SSR**  generates HTML for each page request at runtime on the server, which is then sent to the client. This ensures that the content is always up to date, which is beneficial for dynamic data, such as user-specific content or frequently updated data (e.g., a news website or a dashboard).
 
- Unlike static generation (SSG), which pre-renders content at build time, SSR renders content on-demand.
 
- **Example**  of how SSR works: 
  - The user requests a page (`/products`).

  - The server fetches the data for products and generates the HTML for the page.

  - The complete HTML is sent to the browser.
**2. getServerSideProps**  
- The **The `getServerSideProps`**  function is a key feature of SSR in Next.js. It fetches data on the server every time a request is made to the page. This function runs only on the server side and ensures that the data is up-to-date for every request.
 
- To use SSR in a page, you can export the `getServerSideProps` function, which will be executed before rendering the page.
 
- **Example** : Using `getServerSideProps` to fetch dynamic data at each request.


```Copy code
# File path: pages/products.js
```


```Copy code
// pages/products.js
export async function getServerSideProps() {
  // Fetch data from an external API or database
  const res = await fetch('https://fakestoreapi.com/products');
  const products = await res.json();

  // Pass the data to the page via props
  return {
    props: {
      products,
    },
  };
}

export default function Products({ products }) {
  return (
    <div>
      <h1>Products List</h1>
      <ul>
        {products.map((product) => (
          <li key={product.id}>
            {product.title} - ${product.price}
          </li>
        ))}
      </ul>
    </div>
  );
}
```
 
- In this example, the **products**  data is fetched server-side and passed as props to the `Products` component. Every time a user visits `/products`, the data is fetched in real-time from the server and rendered on the page.
**3. Use Cases for SSR vs SSG**  
- Choosing between **SSR**  and **SSG**  depends on the type of data being displayed and how often it changes.
**When to Use SSR (Server-Side Rendering)** : 
- **Dynamic Content** : If the content changes frequently and needs to be updated on every request, SSR is a better option. For example, a user-specific dashboard or a live stock ticker would benefit from SSR.
 
- **SEO for Dynamic Pages** : If you need better SEO for dynamic content, such as user-specific content or e-commerce product pages that change frequently, SSR ensures that the search engines receive fully rendered content.
 
- **Authentication-Based Content** : Pages where user-specific data is displayed (e.g., personalized dashboards, logged-in user profiles) work well with SSR, as the data is fetched at request time.
**Example** : A product page where the product data changes frequently and needs to be fetched in real-time:

```Copy code
# File path: pages/product/[id].js
```


```Copy code
export async function getServerSideProps(context) {
  const { id } = context.params;
  const res = await fetch(`https://fakestoreapi.com/products/${id}`);
  const product = await res.json();

  return {
    props: {
      product,
    },
  };
}

export default function Product({ product }) {
  return (
    <div>
      <h1>{product.title}</h1>
      <p>Price: ${product.price}</p>
      <p>{product.description}</p>
    </div>
  );
}
```
**When to Use SSG (Static Site Generation)** : 
- **Static Content** : Use SSG when the content doesn't change often or can be pre-rendered at build time. Examples include blogs, documentation sites, or marketing pages where the content remains relatively static.
 
- **Performance** : Since SSG pre-renders pages at build time, the resulting static files are fast to load and don’t need to be rendered at every request.
 
- **Less Dynamic Data** : For content that doesn’t change frequently, such as a product listing page, using SSG allows the content to be built once and served as static HTML.
**Example** : A blog post that is created once and doesn’t change often can be pre-rendered using **SSG**  (`getStaticProps`):

```Copy code
# File path: pages/blog/[slug].js
```


```Copy code
export async function getStaticProps({ params }) {
  const res = await fetch(`https://api.example.com/blog/${params.slug}`);
  const post = await res.json();

  return {
    props: {
      post,
    },
  };
}

export default function BlogPost({ post }) {
  return (
    <div>
      <h1>{post.title}</h1>
      <p>{post.content}</p>
    </div>
  );
}
```
**Summary: SSR vs SSG**  
- **SSR**  (Server-Side Rendering):
  - Fetches data at request time.

  - Ideal for frequently updated data.

  - Pages are rendered dynamically on the server.
 
- **SSG**  (Static Site Generation):
  - Fetches data at build time.

  - Ideal for content that doesn’t change frequently.

  - Pages are pre-rendered and served as static HTML.
  
[Back To Context](README.md) 

---

| © TINITIATE.COM | 
| --- | 


---
