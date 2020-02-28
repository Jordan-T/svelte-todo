<script>
  import { createEventDispatcher, tick } from 'svelte';

  export let todo;

  let isEditing = false;
  let editText = '';
  let editInput;

  const dispatch = createEventDispatcher();

  function handleEdit() {
    editText = todo.title;
    isEditing = true;

    tick()
      .then(() => {
        editInput.focus()
      });
  }

  function handleCancel() {
    editText = '';
    isEditing = false;
  }

  function handleSubmit() {
    dispatch('edit', {
      ...todo,
      title: editText,
    });

    editText = '';
    isEditing = false;
  }

  function handleDelete() {
    dispatch('delete');
  }

  function handleToggle() {
    dispatch('edit', {
      ...todo,
      done: !todo.done,
    })
  }

  function handleKeyUp(event) {
    if(event.key === "Enter"){
      handleSubmit();
    } else if(event.key === "Escape") {
      handleCancel()
    }
  }
</script>


<li class:completed={todo.done} class:editing={isEditing}>
  <div class="view">
    <input class="toggle" type="checkbox" on:click={handleToggle} checked={todo.done} >
    <label on:dblclick={handleEdit}>{todo.title}</label>
    <button class="destroy" on:click|preventDefault={handleDelete}></button>
  </div>
  {#if isEditing}
    <input type="text" class="edit" bind:value={editText} on:keyup={handleKeyUp} on:blur={handleCancel} bind:this={editInput}>
  {/if}
</li>
