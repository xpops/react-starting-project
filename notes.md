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

---

## 3. Prop Forwarding (or Proxying Props)

Using the JavaScript rest/spread operator (`...`) to automatically forward built-in or custom attributes from a parent component to an underlying HTML element inside a custom component.

### The Problem

When creating wrapper components like `<Section>` or custom `<TabButton>`, you often need to support standard HTML attributes (like `id`, `className`, `onClick`, `disabled`, etc.) on the underlying element. Manually defining all of these props and passing them down is tedious and non-scalable.

### The Solution: Using Rest & Spread (`...props`)

1. **Destructuring with Rest Operator (`...props`):** Collect all remaining props that were not explicitly destructured into a single `props` object.
2. **Spreading onto the Element (`{...props}`):** Spread that object onto the destination HTML element or component.

### Code Examples

#### Wrapper Component (`Section.jsx`)

```jsx
// Destructure title and children, and gather everything else into 'props'
export default function Section({ title, children, ...props }) {
  return (
    // Forward all extra props (like id, className, style, etc.) onto the <section>
    <section {...props}>
      <h2>{title}</h2>
      {children}
    </section>
  );
}
```

#### Custom Interactive Component (`TabButton.jsx`)

```jsx
// Collect event handlers like onClick, disabled, etc., into 'props'
export default function TabButton({ children, isSelected, ...props }) {
  return (
    <li>
      {/* className is explicitly managed, but other attributes are forwarded via {...props} */}
      <button className={isSelected ? "active" : undefined} {...props}>
        {children}
      </button>
    </li>
  );
}
```

#### Usage (`Examples.jsx`)

```jsx
// 'id' is forwarded to the underlying <section> element inside <Section>
// 'onClick' is forwarded to the <button> inside <TabButton>
<Section id="examples" title="Examples">
  <menu>
    <TabButton
      isSelected={selectedTopic === "components"}
      onClick={() => handleSelect("components")}
    >
      Components
    </TabButton>
  </menu>
</Section>
```
