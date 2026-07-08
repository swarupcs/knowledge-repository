
⚛️ **What is `useEffect` in React?**

If `useState` lets your component **remember data**, then **`useEffect` lets it interact with the outside world.**

It's the React Hook used for **side effects**—work that happens **after** React updates the UI.

### What are side effects?

Things like:

🌐 Fetching data from an API
⏰ Starting timers (`setInterval`, `setTimeout`)
🎧 Adding event listeners
💾 Reading/writing `localStorage`
🔌 Connecting to WebSockets

These shouldn't happen during rendering.

---

### Basic Syntax

```jsx id="effect01"
useEffect(() => {
  // Side effect

  return () => {
    // Cleanup (optional)
  };
}, [dependencies]);
```

The effect runs **after React renders the component**.

---

### How `useEffect` works

```text id="flow01"
Render
   ↓
React updates the DOM
   ↓
useEffect runs
   ↓
Side effect executes
```

Unlike rendering, effects happen **after** the UI is painted.

---

### The dependency array

**1️⃣ Run after every render**

```jsx id="dep01"
useEffect(() => {
  console.log("Rendered");
});
```

---

**2️⃣ Run only once (on mount)**

```jsx id="dep02"
useEffect(() => {
  fetchData();
}, []);
```

The empty dependency array tells React to run the effect only after the initial render.

---

**3️⃣ Run when specific values change**

```jsx id="dep03"
useEffect(() => {
  document.title = count;
}, [count]);
```

The effect runs whenever `count` changes.

---

### Cleanup function

Some effects need cleanup to avoid memory leaks.

```jsx id="cleanup01"
useEffect(() => {
  const id = setInterval(fetchData, 1000);

  return () => {
    clearInterval(id);
  };
}, []);
```

React calls the cleanup function before the effect runs again (if dependencies change) and when the component unmounts.

---

### 💡 Best Practices

✅ Use `useEffect` for side effects, not for calculations you can do during render.
✅ Include all values your effect depends on in the dependency array.
✅ Always clean up timers, subscriptions, and event listeners.
✅ Split unrelated side effects into separate `useEffect` calls.

`useEffect` isn't for rendering UI—it's for synchronizing your component with things **outside React**.

Understanding **when** and **why** an effect runs is one of the biggest steps toward writing predictable React applications.

What's the most common thing you use `useEffect` for—API calls, event listeners, or something else?


![alt text](image-28.png)