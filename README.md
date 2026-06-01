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

# 🧠 JavaScript Core Concepts

## 8. Closures in JavaScript

A closure allows a function to access variables from its outer scope even after the outer function has finished execution.

### Example

```javascript
function counter() {
  let count = 0;

  return function() {
    count++;
    return count;
  };
}

const increment = counter();
```

### Real-World Uses
- Data privacy
- Event handlers
- Timers
- Memoization

---

## 9. JavaScript Event Loop

JavaScript is single-threaded.

### Flow
1. Call Stack executes synchronous code
2. Async tasks move to Web APIs
3. Completed tasks move to Callback Queue
4. Event Loop pushes them back to Call Stack

### Purpose
Enables asynchronous non-blocking behavior.

---

## 10. Event Delegation

Instead of attaching events to multiple child elements, a single event listener is attached to the parent element using event bubbling.

### Benefits
- Better performance
- Less memory usage
- Handles dynamically added elements

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
