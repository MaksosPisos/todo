<script>
  let todoItem = "";
  let arrayTodo = [
    {
      id: 1,
      name: "todo item 1",
      ready: false,
    },
    {
      id: 2,
      name: "todo item 2",
      ready: true,
    },
  ];
  const addTodoItem = () => {
    let newTodoItem = {
      id: arrayTodo.length + 1,
      name: todoItem,
      ready: false,
    };
    arrayTodo = [...arrayTodo, newTodoItem];
    todoItem = "";
  };
  const todoItemReady = (id) => {
    let index = arrayTodo.findIndex((todo) => todo.id === id);
    arrayTodo[index].ready = !arrayTodo[index].ready;
    arrayTodo = [...arrayTodo];
  }
  
  function delTodoItem(id){
    let index = arrayTodo.findIndex((todo) => todo.id === id);
    arrayTodo.splice(index, 1)
    arrayTodo = [...arrayTodo]
  }
  
</script>

<main
  class="min-h-screen bg-teal-900 text-slate-100 w-full flex items-center justify-center"
>
  <div class="flex flex-col w-80 bg-teal-700 rounded-md gap-4 p-4">
    <h1 class=" text-center text-2xl font-bold">TODO</h1>
    <div class="flex items-center justify-between">
      <input
        type="text"
        placeholder="Please enter... "
        class="flex-grow bg-teal-900 p-2 rounded-l-lg"
        bind:value={todoItem}
      />
      <button
        class="flex items-center justify-center bg-teal-500 p-2 rounded-r-lg hover:bg-teal-400 transition active:bg-teal-600 disabled:pointer-events-none disabled:bg-teal-800"
        on:click={addTodoItem}
        disabled={todoItem.length < 3}
      >
        <span class="material-icons"> add </span>
      </button>
    </div>
    <ul>
      {#each arrayTodo as name, index}
        <li
          class=" bg-teal-800 p-2 rounded-lg flex justify-between items-center mb-2 gap-2"
        >
          {#if name.ready}
            <p class="flex-grow italic line-through">{name.name}</p>
          {:else}
            <p class="flex-grow ">{name.name}</p>
          {/if}

          <button
            class=" flex justify-center items-center text-sky-300 hover:text-sky-400 transition" on:click={() => todoItemReady(name.id)}
            ><span class="material-icons"> library_add_check </span></button
          >
          <button
            class=" flex justify-center items-center text-rose-300 hover:text-rose-400 transition" on:click={() => delTodoItem(name.id)}
            ><span class="material-icons"> remove_circle </span></button
          >
        </li>
      {/each}
    </ul>
  </div>
</main>
