create app:
```bash
npx create-next-app pingmint
```

install react developer in chrome

# components
can only have one parent element - use `React.Fragment` as a generic parent, aka `<>` and `</>`

# style
`foo.module.css` - CSS for `Foo` 

```jsx

import styles from "./foo.module.cs"

// Note: prefer separate CSS instead of inline styles
const inlineStyle = { fontStyle: "italic" }

const Foo = () => {
	return (
		<div 
		  className={styles.someclassname} 
		  style={inlineStyle} >
		blah
		</div>
	)
};
```

# Props
```jsx
// Convention: parameter called "props"
const Foo = (props) => {
	return (
		<h1>{props.headerText}</h1>
	)
};

// Later on using Foo
const Bar = () => {
	return (
		<Foo headerText="Hello, World" />
	)
}
```

Props are read-only

`props.children` contains all markup

# Random
`key` necessary when generating arrays of components - like SwiftUI identity

# Hooks
Function with `use` prefix

Rules:
- Only call them at the top level of the function
- Only call them in a function component (except custom hooks)
- Always called, i.e. not conditional
- May call `useState` multiple times

## state
internal data managed by the component

```jsx
const [foo, setFoo] = useState(bar); // bar is initial value
// return `foo` in the component below
// use `setFoo` to change state, do not modify `bar`

const addFoo = () => {
	setFoo([
		...foo, // spread existing elements
		{ id: 123, label: "hi" } // add one more
	])
}

const [counter, setCounter] = useState(0);
setCounter(current => current + 1); // can take a function that provides current value

return (
	<>
		{foo}
		<button onClick={addFoo}>Add</button>
	</>
)
```
