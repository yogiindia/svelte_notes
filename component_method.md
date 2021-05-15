## Component Method
***Exposing component method to outside world, which in turn changes inner state of Component.***
```javascript

App.svelte
==========

<script>
	import Dialog from './Dialog.svelte'
	let dialog;
</script>

<Dialog bind:this={dialog} />

<button on:click={()=>dialog.openModal()}>
	open
</button>

<button on:click={()=>dialog.closeModal()}>
	close
</button>


Diaglog.svelte
==============

<script>
	let isOpen = false;
	let email = '';
	let name = ''
	
	function reset(){
		name = '';
		email = '';
	}
	
	export function closeModal(){
		isOpen = false;
		reset();
	}
	
	export function openModal(){
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