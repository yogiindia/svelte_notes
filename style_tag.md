## Using variables within style tag.
There a number of ways to bind variable with css styles.
1. `<p style="font-size: {size}px;color:{color};">hello</p>`

But we can't use svelte variables inside style tag as brackets are invalid syntax in css. Instead we can use css variables. To use svelte variables we have to bind it with css variables.

```javascript
//declaring css variables and binding with svelte variables
<p style="--size:{size};--color:{color}">hello</p>

<style>
p{
    font-size: var(--size)px;
    color: var(--color);
}
</style>
```

***An elegant way to achieve same behaviour is by using svlete actions***

```javascript
App.svelte
==========

<script>
	import cssVariables from './cssVariables'
	let size = 32;
	let color = '#ff0000';
</script>

<input bind:value={size} type="range" min="12" max="50" />
<input bind:value={color} type="color" />
<p>font-size: {size}px, color: {color}</p>

<p use:cssVariables={{size, color}}>
	Hello world
</p>

<style>
	p {
		font-size: calc(var(--size) * 1px);
		color: var(--color);
		border: var(--color) 1px solid;
	}
</style>

cssVariables.js
===============

export default function cssVariables(node, variables) {
    setCssVariables(node, variables);
    
    return {
        update(variables) {
            setCssVariables(node, variables);
        }
    }
}
function setCssVariables(node, variables) {
    for (const name in variables) {
        node.style.setProperty(`--${name}`, variables[name]);
    }
}

```