
⚛️ **Managing Multiple State Variables in React**

A component rarely needs just one piece of state.

You might need to track:
👤 User name
📧 Email
🌙 Dark mode
🔄 Loading status
🛒 Cart count

Instead of putting everything into one state object, React lets you create **multiple independent state variables**.

### Example

```jsx id="multi01"
import { useState } from "react";

function Profile() {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");
  const [age, setAge] = useState(18);
  const [isSubscribed, setIsSubscribed] = useState(false);

  // ...
}
```

Each `useState` call manages its own piece of state.

---

### What happens when one state changes?

```text id="flow01"
User updates name
        ↓
setName("Alex")
        ↓
Only "name" state changes
        ↓
React re-renders the component
        ↓
UI displays the updated name
```

The other state values (`email`, `age`, `isSubscribed`) remain unchanged.

---

### Why use multiple state variables?

✅ Easier to read

```jsx id="good01"
const [loading, setLoading] = useState(false);
const [error, setError] = useState(null);
```

instead of:

```jsx id="bad01"
const [state, setState] = useState({
  loading: false,
  error: null,
});
```

for unrelated values.

---

### When should you group state?

If multiple values always change together, keeping them in an object can make sense.

```jsx id="group01"
const [user, setUser] = useState({
  name: "",
  email: "",
});
```

Update it like this:

```jsx id="group02"
setUser(prev => ({
  ...prev,
  name: "Alex",
}));
```

---

### Rule of Thumb

✅ Use **multiple `useState` hooks** for independent values.

✅ Use **one object state** when the values are closely related and usually updated together.

💡 Keeping state small and focused makes components easier to understand, update, and maintain.

Do you prefer multiple `useState` hooks or a single object state in your React components? Why?


![alt text](image-21.png)