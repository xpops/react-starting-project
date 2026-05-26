# React Core Concepts Notes

## 1. Importing Images as Paths

```js
import reactImg from "./assets/react-core-concepts.png";
```

- **Explicit Reference:** When building the project, importing explicitly tells the build tool that this JS/JSX file references this image file.
- **Prevents Broken Paths:** Unlike hardcoding the path string to the image (e.g., `./assets/image.png`), using `import` prevents the image file from getting lost or broken during the build process, as the build tool automatically manages the hashed production path.

---

## 2. React State Summary

```jsx
import { useState } from "react";
const [selectedTopic, setSelectedTopic] = useState("Please click a button");
```

### What is State?

Essentially, **State is a variable**—but one that is managed internally by React.

### The Key Difference (Normal Variables vs. State)

- **Normal Variables:** Changing their values does not tell React to do anything. The UI remains frozen.
- **State Variables:** When you change their values using their **updater (set) function**, it triggers React to **re-execute (re-call) the entire component function**.

### How It Works

1. **Trigger:** You call the `set` function (e.g., `setTitle('New Value')`).
2. **Re-execution:** React re-runs the component function from top to bottom.
3. **Memory Retrieval:** During this re-run, `useState` retrieves and returns the newly updated value from React's internal memory.
4. **Re-rendering:** The component returns the new JSX, and React automatically updates only the changed parts on the screen (this is _re-rendering_, not a full page reload/refresh).
