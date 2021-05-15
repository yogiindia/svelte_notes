## Two way binding
***Props passed to component will act as inner state of componet inside it. Any change to prop inside a componet will not reflect to outside world. To achieve that behaviour two way binding is used. In the example open and close button will work as expected without binding. But if user clicks on cross, then inner isOpen is changed to false,but isOpen in app.svelte is still true. So when open button is clicked nothing will happen as its state is still in open state. So binding is used to fix that bug.***

```javascript

App.svelte
==========

<script>
	import Dialog from './Dialog.svelte'
	let isOpen = false;
</script>

<Dialog bind:isOpen />

<button on:click={()=>isOpen=true}>
	open
</button>

<button on:click={()=>isOpen=false}>
	close
</button>


Diaglog.svelte
==============

<script>
	export let isOpen = false;
	let email = '';
	let name = ''
	
	function reset(){
		name = '';
		email = '';
	}
	
	function closeModal(){
		isOpen = false;
		reset();
	}
	
	function openModal(){
		isOpen = true;
	}
</script>

{#if isOpen}
<div class="dialog">
	<span class="close" on:click={closeModal}>X</span>
	<label>
		Name
		<input bind:value={name} />
	</label>
	<label>
		Email
		<input bind:value={email} />
	</label>
</div>
{/if}
```