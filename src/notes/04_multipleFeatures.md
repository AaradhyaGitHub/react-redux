### Understanding Centralized State Management with Redux Toolkit

#### Problem Breakdown:
When working with multiple components like `Header` and `Auth`, each will manage its own state and behavior. However, since `userProfile` will be displayed based on the state in `Header`, we need a **centralized state management** system. Redux Toolkit provides a structured way to manage this state efficiently.

---

### Step 1: Define the Initial State
We start by creating an initial state object for authentication:

```jsx
const initialAuthState = { isAuthenticated: false };
```

This defines the default authentication state for our application.

---

### Step 2: Create a New Slice
A slice in Redux Toolkit is a collection of state logic, including its reducers and actions. We create a new slice for authentication:

```jsx
const authSlice = createSlice({
  name: "auth", // The slice name, which is native to Redux Toolkit
  initialState: initialAuthState, // The initial state we defined earlier
  reducers: {
    login(state) {
      state.isAuthenticated = true; // Changes authentication state to logged in
    },
    logout(state) {
      state.isAuthenticated = false; // Changes authentication state to logged out
    }
  }
});
```

#### Explanation:
- `createSlice` takes an object with three properties:
  - `name`: The identifier for this slice.
  - `initialState`: The starting state for this slice.
  - `reducers`: An object containing functions that modify the state.
- Inside `reducers`, we define two functions:
  - `login`: Sets `isAuthenticated` to `true`.
  - `logout`: Sets `isAuthenticated` to `false`.
- **Important:** Redux Toolkit allows us to **mutate the state directly** because it uses the Immer library under the hood.

---

### Step 3: Configure the Store
Since Redux follows a single store principle, we configure our store by passing an object with multiple reducers:

```jsx
const store = configureStore({
  reducer: {
    counter: counterSlice.reducer,
    auth: authSlice.reducer
  }
});
```

#### Explanation:
- `configureStore` sets up our Redux store.
- Instead of passing a single reducer, we pass an object under the `reducer` key.
- We provide identifiers (`counter` and `auth`) and link them to their respective reducers:

```jsx
reducer: {
  counter: counterSlice.reducer,
  auth: authSlice.reducer
}
```

This structure allows us to manage multiple slices within a single store.

---

### Summary
1. We **defined an initial state** for authentication.
2. We **created a Redux slice** with `createSlice`, defining actions to log in and log out.
3. We **configured our Redux store** to include multiple slices.

This approach ensures that state updates are predictable and manageable across components, making it easier to scale the application.