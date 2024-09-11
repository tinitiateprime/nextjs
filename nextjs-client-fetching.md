# Next.js 

© TINITIATE.COM

[Back To Context](README.md) 
# Client-Side Data Fetching 
 
- In Next.js, data can be fetched on the **client-side**  using standard React hooks such as **useEffect**  in combination with the **Fetch API** . This approach allows fetching data after the page has loaded. Additionally, Next.js provides an optimized client-side data fetching library called **SWR**  (Stale-While-Revalidate) that simplifies and enhances the data fetching experience.

## Key Concepts for Client-Side Data Fetching: 
**1. useEffect and Fetch API**  
- The **useEffect**  hook in React allows you to perform side effects, such as fetching data, after the component has rendered. When combined with the **Fetch API** , useEffect is a simple way to fetch data from an API once the component is mounted on the client-side.
 
- **Example** : Fetching data inside a component using `useEffect` and displaying it on the page.


```Copy code
# File path: pages/client-fetch.js
```


```Copy code
import { useState, useEffect } from 'react';

export default function ClientFetch() {
  const [data, setData] = useState(null);

  // useEffect to fetch data from an API
  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/posts')
      .then((response) => response.json())
      .then((data) => setData(data));
  }, []);  // Empty array ensures this runs only once when the component mounts

  if (!data) {
    return <p>Loading...</p>;
  }

  return (
    <div>
      <h1>Client-Side Data Fetching</h1>
      <ul>
        {data.map((post) => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </div>
  );
}
```
 
- In this example, data is fetched from a placeholder API after the component is rendered. The useEffect hook ensures that the fetch request only happens once, and the `data` is stored in the state, which is then displayed on the page.
**2. Using SWR for Data Fetching**  
- **SWR**  (Stale-While-Revalidate) is a data fetching library built by the Vercel team (the creators of Next.js) that provides several benefits over traditional client-side data fetching. SWR automatically handles features such as **caching** , **revalidation** , **focus tracking** , and **pagination** .
 
- To use SWR, first install it using npm or yarn:


```Copy code
npm install swr
# or
yarn add swr
```
 
- **Example** : Using **SWR**  for client-side data fetching.


```Copy code
# File path: pages/swr-fetch.js
```


```Copy code
import useSWR from 'swr';

// Fetch function
const fetcher = (url) => fetch(url).then((res) => res.json());

export default function SWRFetch() {
  // Using SWR to fetch data from an API
  const { data, error } = useSWR('https://jsonplaceholder.typicode.com/posts', fetcher);

  if (error) return <div>Failed to load data</div>;
  if (!data) return <div>Loading...</div>;

  return (
    <div>
      <h1>Data fetched with SWR</h1>
      <ul>
        {data.map((post) => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </div>
  );
}
```
 
- Key advantages of **SWR** : 
  - **Caching** : The data is cached so if the same request is made again, it loads instantly from cache.
 
  - **Revalidation** : When the user revisits the page or refocuses the tab, the data is revalidated.
 
  - **Error Handling** : Built-in error handling to catch issues with the API.
 
- In the example, **SWR**  fetches data from the API and automatically handles revalidations, caching, and displaying the data.
**3. API Integration**  
- Client-side data fetching is essential when integrating **third-party APIs**  or services that require real-time interaction from the client. You can use libraries such as **Axios** , or simply rely on the **Fetch API**  or **SWR**  for making API calls.
 
- **Example** : Fetching data from a real-time API like a cryptocurrency price tracker using `useEffect`.


```Copy code
# File path: pages/crypto-prices.js
```


```Copy code
import { useState, useEffect } from 'react';

export default function CryptoPrices() {
  const [prices, setPrices] = useState(null);

  useEffect(() => {
    fetch('https://api.coindesk.com/v1/bpi/currentprice.json')
      .then((response) => response.json())
      .then((data) => setPrices(data.bpi));
  }, []);

  if (!prices) {
    return <p>Loading prices...</p>;
  }

  return (
    <div>
      <h1>Crypto Prices</h1>
      <p>Bitcoin: {prices.USD.rate} USD</p>
      <p>Bitcoin: {prices.EUR.rate} EUR</p>
    </div>
  );
}
```
 
- In this example, we are integrating a **real-time API**  (CoinDesk’s Bitcoin Price Index) into the application. The price data is fetched on the client side using `useEffect` and displayed to the user. This demonstrates how easy it is to fetch and integrate external APIs into your Next.js application.
**When to Use Client-Side Data Fetching**  
- **Real-time Updates** : When you need to fetch frequently updated data (e.g., stock prices, cryptocurrency rates, live scores).
 
- **User-Specific Content** : When you need to fetch data specific to a user after the page has already loaded (e.g., a user profile page).
 
- **Performance Optimization** : To avoid fetching data on the server and instead load it asynchronously after the page has rendered.

[Back To Context](README.md) 

---

| © TINITIATE.COM | 
| --- | 


---
