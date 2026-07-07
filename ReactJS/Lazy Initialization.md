⚛️ **React `useState` Lazy Initialization Explained**

Did you know `useState` can accept a **function** instead of a value?

This small feature can improve performance by avoiding unnecessary work on every render.

### ❌ Normal Initialization

```jsx id="lazy01"
const [data, setData] = useState(expensiveCalculation());
```

At first glance this looks fine...

But `expensiveCalculation()` is **executed every time the component renders**, even though React only uses its result for the initial state.

---

### ✅ Lazy Initialization

Pass a function instead:

```jsx id="lazy02"
const [data, setData] = useState(() => expensiveCalculation());
```

Now React calls `expensiveCalculation()` **only once**—during the initial render.

Every later render reuses the stored state value.

---

### What happens behind the scenes?

```text id="flow01"
Component Mounts
        ↓
Initializer Function Runs
        ↓
Initial State Stored
        ↓
Component Re-renders
        ↓
Initializer is NOT called again
        ↓
Existing State is Reused
```

---

### A practical example

Reading from `localStorage`:

```jsx id="local01"
const [user, setUser] = useState(() => {
  return JSON.parse(localStorage.getItem("user"));
});
```

Without lazy initialization, `localStorage.getItem()` would run on every render.

With lazy initialization, it runs only once.

---

### When should you use it?

✅ Reading from `localStorage` or `sessionStorage`

✅ Expensive calculations

```jsx id="calc01"
const [result] = useState(() => heavyCalculation());
```

✅ Computing complex default values

---

### When NOT to use it

For simple values like these:

```jsx id="simple01"
const [count, setCount] = useState(0);
const [name, setName] = useState("");
const [isOpen, setIsOpen] = useState(false);
```

There's no need for lazy initialization.

---

### 💡 Rule of Thumb

Use:

```jsx id="rule01"
useState(initialValue)
```

for simple values.

Use:

```jsx id="rule02"
useState(() => initialValue)
```

when calculating the initial value is expensive.

Small optimization, big difference in components that render frequently.

Were you aware that `useState` accepts a function as its initial value?


![alt text](image-25.png)