# ReactJs-Interview-Questions


## 1. Difference Between CSR, SSR, SSG, and ISR

| Rendering Type | Meaning | Best Use Cases |
|---|---|---|
| CSR | Client-Side Rendering | Dashboards, SPAs |
| SSR | Server-Side Rendering | SEO-heavy dynamic websites |
| SSG | Static Site Generation | Blogs, documentation |
| ISR | Incremental Static Regeneration | Frequently updated static pages |

### CSR
- Rendering happens in the browser
- Faster navigation after initial load
- Poor SEO if not optimized

### SSR
- HTML generated on the server for each request
- Better SEO and initial page load

### SSG
- Pages generated during build time
- Very fast and cacheable

### ISR
- Updates static pages incrementally without rebuilding the whole app
- Useful for content-heavy applications

---

## 2. Designing a Scalable Role-Based Authentication System

### Core Components
- JWT Authentication
- Refresh Tokens
- Role-Based Access Control (RBAC)
- Middleware Authorization
- Secure HTTP-only Cookies

### Flow
1. User logs in
2. Backend generates access + refresh token
3. Role stored in token/database
4. Middleware validates permissions
5. Unauthorized access is blocked

### Best Practices
- Token expiration
- Refresh token rotation
- Centralized permissions
- API route protection

---

## 3. Structuring a Large-Scale Frontend Application

```bash
src/
 ├── components/
 ├── pages/
 ├── hooks/
 ├── services/
 ├── store/
 ├── routes/
 ├── utils/
 └── assets/
```

### Best Practices
- Feature-based architecture
- Reusable UI components
- Centralized API handling
- Proper state management
- Environment-based configuration
- Scalable folder structure

---

# ⚛️ React Internals & Performance

## 4. React Reconciliation Algorithm

React compares:
- Previous Virtual DOM
- Updated Virtual DOM

Using the diffing algorithm, React updates only changed nodes in the Real DOM instead of re-rendering everything.

### Benefits
- Faster UI updates
- Efficient rendering
- Improved performance

---

## 5. Virtual DOM vs Real DOM

| Virtual DOM | Real DOM |
|---|---|
| Lightweight JS object | Actual browser DOM |
| Faster updates | Expensive updates |
| React updates selectively | Full reflow/repaint possible |

### Why Virtual DOM Improves Performance
- Reduces direct DOM manipulation
- Uses batching updates
- Efficient diffing process

---

## 6. Avoiding Unnecessary Re-renders in React

### Strategies
- React.memo
- useMemo
- useCallback
- Lazy loading
- Code splitting
- State colocation
- Proper key usage

---

## 7. React.memo vs useMemo vs useCallback

| Hook | Purpose |
|---|---|
| React.memo | Prevent component re-render |
| useMemo | Memoize computed values |
| useCallback | Memoize function references |

---

# 🚀 Performance & Real-World Scenarios

## 11. Optimizing a Slow React Application

### Techniques
- Lazy loading
- Code splitting
- Memoization
- Image optimization
- Virtualization
- Debouncing & throttling
- API optimization

---

## 12. Race Conditions in Frontend Applications

Race conditions occur when multiple asynchronous operations complete unpredictably.

### Prevention Methods
- AbortController
- Request cancellation
- Tracking latest requests
- Proper async handling

---

## 13. Handling Global API Token Expiration

### Common Approach
- Axios interceptors
- Detect 401 responses
- Refresh expired access token
- Retry failed requests
- Logout user if refresh fails

---

## 14. Reusable Custom Hook for API Requests

### Features
- Loading state
- Error handling
- Data caching
- Cleanup support
- Reusable logic

### Example

```javascript
const { data, loading, error } = useFetch("/api/users");
```

### Benefits
- Cleaner components
- Centralized API logic
- Better maintainability

---

## ❓ Virtual DOM vs Real DOM

| Virtual DOM | Real DOM |
|---|---|
| Lightweight JavaScript object | Actual browser DOM |
| Faster updates | Slower updates |
| Efficient diffing | Expensive manipulation |

### Why Virtual DOM Is Faster

1. Creates a virtual representation
2. Compares previous and new trees
3. Updates only changed nodes

---

## ❓ What are Custom Hooks in React?

Custom Hooks are reusable JavaScript functions that contain React Hook logic.

### Example

```javascript
import { useState } from "react";

function useCounter() {
  const [count, setCount] = useState(0);

  return {
    count,
    setCount
  };
}
```

### Benefits

- Reusable logic
- Cleaner components
- Better maintainability

---

## ❓ Stateful vs Stateless Components

| Stateful Components | Stateless Components |
|---|---|
| Manage state | No state |
| Uses hooks/state | Receives props |
| Handles logic | Primarily UI |

### Stateful Example

```javascript
function Counter() {
  const [count, setCount] = useState(0);

  return <button>{count}</button>;
}
```

### Stateless Example

```javascript
function Greeting({ name }) {
  return <h1>{name}</h1>;
}
```

---

## ❓ How to Create Context in React?

### Step 1: Create Context

```javascript
import { createContext } from "react";

export const UserContext = createContext();
```

### Step 2: Provide Context

```javascript
<UserContext.Provider value={user}>
  <App />
</UserContext.Provider>
```

### Step 3: Consume Context

```javascript
const user = useContext(UserContext);
```

---

## ❓ How Will You Handle Complex State Logic in React?

### Recommended Approaches

- useReducer
- Context API
- Redux Toolkit
- Zustand

### When to Use useReducer

- Multiple state transitions
- Related state updates
- Complex business logic

---

## ❓ How Rendering Works in React?

### Rendering Flow

1. State or props change
2. React creates a new Virtual DOM
3. React compares previous and current Virtual DOM
4. Diffing algorithm identifies changes
5. React updates only changed nodes in Real DOM

### Benefits

- Faster UI updates
- Better performance
- Efficient DOM manipulation

---

# 📚 Quick Revision

### HTML
- Shadow DOM

### CSS
- Inline vs Block Elements
- CSS Isolation
- Adaptive vs Responsive Design
- Tailwind CSS

### JavaScript
- Garbage Collection
- Promises
- Async/Await
- TypeScript
- Generics
- API Security
- Error Handling
- API Versioning
- API Monitoring

### React
- Virtual DOM
- Custom Hooks
- Context API
- Stateful vs Stateless Components
- Complex State Management
- React Rendering Process

---
---

# 1️⃣6️⃣ Fetch Data Using useEffect

```jsx
import { useEffect, useState } from "react";

function Users() {

  const [users, setUsers] =
    useState([]);

  useEffect(() => {

    async function fetchUsers() {

      const response =
        await fetch(
          "https://jsonplaceholder.typicode.com/users"
        );

      const data =
        await response.json();

      setUsers(data);
    }

    fetchUsers();

  }, []);

  return (
    <div>
      {users.map(user => (
        <p key={user.id}>
          {user.name}
        </p>
      ))}
    </div>
  );
}

export default Users;
```

---

# 1️⃣7️⃣ What are Controlled Components?

Controlled components are form elements whose value is controlled by React state.

### Example

```jsx
import { useState } from "react";

function InputField() {

  const [name, setName] =
    useState("");

  return (
    <input
      type="text"
      value={name}
      onChange={(e) =>
        setName(e.target.value)
      }
    />
  );
}
```

### Benefits

- Single source of truth
- Easier validation
- Better form control

---

# 1️⃣8️⃣ What is Redux?

Redux is a predictable state management library used to manage global application state.

---

## Redux Flow

```text
Component
   ↓
Dispatch Action
   ↓
Reducer
   ↓
Store Updated
   ↓
Component Re-renders
```

---

## Core Concepts

### Store

Central place that stores application state.

```javascript
const store =
  configureStore({
    reducer: {}
  });
```

---

### Action

Describes what happened.

```javascript
{
  type: "ADD_TODO"
}
```

---

### Reducer

Updates state based on actions.

```javascript
function reducer(
  state,
  action
) {
  switch(action.type) {

    case "ADD_TODO":
      return {
        ...state
      };

    default:
      return state;
  }
}
```

---

### Why Redux?

- Centralized state
- Predictable updates
- Easier debugging
- Middleware support
- Scalable for large applications

---

## Context API vs Redux

| Context API | Redux Toolkit |
|------------|---------------|
| Built into React | External library |
| Small to medium apps | Large applications |
| Less boilerplate | Advanced tooling |
| Simpler setup | Better scalability |

---

## 6. How Does React Re-rendering Work?

React re-renders when:

- State changes
- Props change
- Context changes
- Parent component re-renders

### Example

```jsx
const [count, setCount] = useState(0);

setCount(count + 1);
```

React creates a new Virtual DOM and compares it with the previous one.

---

## 7. Difference Between useMemo vs useCallback

### useMemo

Memoizes a value.

```jsx
const total = useMemo(() => {
  return products.reduce(
    (sum, p) => sum + p.price,
    0
  );
}, [products]);
```

### useCallback

Memoizes a function.

```jsx
const handleClick = useCallback(() => {
  console.log("Clicked");
}, []);
```

### Real Use Cases

#### useMemo

- Expensive calculations
- Filtering large datasets

#### useCallback

- Passing callbacks to child components
- React.memo optimization

---

## 8. How to Prevent Unnecessary Re-renders?

### Use React.memo

```jsx
export default React.memo(UserCard);
```

### Use useMemo

```jsx
const filteredUsers =
  useMemo(() => {
    return users.filter(Boolean);
  }, [users]);
```

### Use useCallback

```jsx
const onClick =
  useCallback(() => {}, []);
```

### Split Components

Avoid large parent re-renders.

---

## 9. How Does React Reconciliation Work?

Reconciliation is React's diffing algorithm.

### Process

```text
Old Virtual DOM
↓
New Virtual DOM
↓
Compare Differences
↓
Update Only Changed Nodes
```

### Benefits

- Faster updates
- Efficient DOM manipulation

---

## 10. When NOT to Use useEffect?

Avoid useEffect for:

### Derived State

❌

```jsx
useEffect(() => {
  setFullName(first + last);
}, [first, last]);
```

✅

```jsx
const fullName = first + last;
```

### Event Handlers

❌

```jsx
useEffect(() => {
  if (clicked) {
    save();
  }
}, [clicked]);
```

✅

```jsx
<button onClick={save}>
```

---

# 🔥 Real-World Scenarios

---

## 11. API is Getting Called Twice — How Would You Debug It?

### Common Reasons

#### React Strict Mode

Development mode intentionally runs effects twice.

#### Dependency Issues

```jsx
useEffect(() => {
  fetchData();
}, [data]);
```

Can create loops.

### Debugging Steps

- Check dependency array
- Inspect StrictMode
- Use React DevTools
- Add logs

---

## 12. How Do You Handle Loading, Error, and Empty States?

```jsx
if (loading)
  return <p>Loading...</p>;

if (error)
  return <p>Error Occurred</p>;

if (!data.length)
  return <p>No Data Found</p>;
```

---

## 13. How Do You Structure a Large React Application?

```text
src
├── components
├── pages
├── hooks
├── services
├── context
├── redux
├── routes
├── utils
└── assets
```

### Benefits

- Scalability
- Maintainability
- Better organization

---

## 14. How Do You Manage State Across Multiple Components?

### Small Apps

- Props
- Context API

### Medium Apps

- useReducer
- Context API

### Large Apps

- Redux Toolkit
- Zustand

---

## 15. How Do You Handle Role-Based UI Permissions?

```javascript
const permissions = {
  admin: ["create", "delete"],
  user: ["view"]
};
```

```jsx
{
  role === "admin" &&
  <DeleteButton />
}
```

### Backend Must Also Validate

Frontend permissions are only for UI control.

---

# ⚡ Performance & Optimization

---

## 16. How to Optimize Large Table/List Rendering?

### Virtualization

Use:

- react-window
- react-virtualized

### Example

```jsx
<FixedSizeList
  height={500}
  itemCount={10000}
  itemSize={50}
/>
```

### Benefits

Render only visible rows.

---

## 17. What is Code Splitting and Lazy Loading?

### Example

```jsx
const Dashboard =
  React.lazy(() =>
    import("./Dashboard")
  );
```

```jsx
<Suspense fallback={<Loading />}>
  <Dashboard />
</Suspense>
```

### Benefits

- Smaller bundles
- Faster initial load

---

## 18. How to Improve Initial Load Time?

### Techniques

- Lazy Loading
- Code Splitting
- Image Optimization
- Tree Shaking
- CDN Usage
- Caching
- Virtualization

---

# 💻 Coding Round

---

## 19. Searchable List with Debouncing

```jsx
const [query, setQuery] =
  useState("");

useEffect(() => {
  const timer =
    setTimeout(() => {
      search(query);
    }, 500);

  return () =>
    clearTimeout(timer);

}, [query]);
```

---

## 20. API Fetch with Loading & Error Handling

```jsx
const [loading, setLoading] =
  useState(true);

const [error, setError] =
  useState(null);

const [data, setData] =
  useState([]);

useEffect(() => {

  async function fetchData() {

    try {
      const res =
        await fetch("/api");

      const json =
        await res.json();

      setData(json);

    } catch (err) {

      setError(err);

    } finally {

      setLoading(false);

    }
  }

  fetchData();

}, []);
```

---

## 21. Optimize a Component to Avoid Re-renders

```jsx
const Child = React.memo(
  ({ onClick }) => {
    return (
      <button
        onClick={onClick}
      >
        Click
      </button>
    );
  }
);
```

```jsx
const handleClick =
  useCallback(() => {
    console.log("Clicked");
  }, []);
```

### Why?

Without useCallback, a new function reference is created on every render.

---

# 📌 Quick Revision

### JavaScript
- Closures
- Event Loop
- Microtasks vs Macrotasks
- Debouncing
- Memory Leaks

### React
- Re-rendering
- useMemo
- useCallback
- Reconciliation
- useEffect

### Real-World
- API Debugging
- Loading States
- State Management
- Role-Based Access

### Performance
- Virtualization
- Lazy Loading
- Code Splitting
- Memoization

---
