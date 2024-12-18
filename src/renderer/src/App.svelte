<script lang="ts">
  import { flip } from 'svelte/animate'

  let inputValue: string = ''
  let taskId: number = 0

  const task = localStorage.getItem('tasks')

  let tasks = task ? JSON.parse(task) : []

  // eslint-disable-next-line @typescript-eslint/explicit-function-return-type
  function deleteTask(index) {
    tasks.splice(index, 1)
    tasks = tasks
    localStorage.setItem('tasks', JSON.stringify(tasks))
  }

  // eslint-disable-next-line @typescript-eslint/explicit-function-return-type
  function addArray() {
    if (inputValue === '') {
      return
    }

    const newObj = { name: `${inputValue}`, id: taskId++ }
    tasks = [...tasks, newObj]
    localStorage.setItem('tasks', JSON.stringify(tasks))
    inputValue = ''
  }
</script>

<div class="overflow-y-auto">
  <div class="relative pb-4">
    <div class="fixed bottom-1 right-0 left-0 z-10 flex justify-center p-3">
      <div
        class="flex flex-wrap items-center justify-between bg-gray-700/5 backdrop-blur-lg border-2 border-gray-600 border-opacity-25 p-3 rounded-[20px]"
      >
        <input
          placeholder="What to do..."
          type="text"
          bind:value={inputValue}
          class="text-white p-2 bg-[#5D5D5D]/5 backdrop-blur-md h-[3.5rem] w-80 mr-2 rounded-xl text-3xl font-semibold"
        />

        <button
          on:click={addArray}
          class="relative group p-4 bg-blue-500 text-white rounded-xl overflow-hidden w-20 h-[3.5rem]"
        >
          <span
            class=" text-white font-semibold block transition-scale group-hover:scale-0 ease-in-out duration-300"
            >Add</span
          >
          <span
            class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 scale-0 text-lg text-white transition-transform duration-300 group-hover:scale-100"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              height="40px"
              viewBox="0 -960 960 960"
              width="40px"
              fill="#e8eaed"
              ><path d="M440-440H200v-80h240v-240h80v240h240v80H520v240h-80v-240Z" /></svg
            >
          </span>
        </button>
      </div>
    </div>
  </div>

  <div class="flex items-center justify-center">
    <div class="flex items-center justify-center flex-col gap-2">
      {#each tasks as tasks, index (index)}
        <div
          class="w-96 rounded-xl bg-[#5D5D5D]/5 backdrop-blur-md"
          animate:flip={{ duration: 300 }}
        >
          <div class="p-3">
            <div
              class="font-semibold text-grey-500 text-xl flex items-center justify-between overflow-x-scroll"
            >
              <input type="checkbox" class="checkbox p-2" />

              {tasks.name}
              <button
                style="float: right"
                class="inline-block bg-red-600 rounded-lg p-2"
                aria-label="joe"
                on:click={() => deleteTask(index)}
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  class="feather feather-trash-2"
                  ><polyline points="3 6 5 6 21 6"></polyline><path
                    d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"
                  ></path><line x1="10" y1="11" x2="10" y2="17"></line><line
                    x1="14"
                    y1="11"
                    x2="14"
                    y2="17"
                  ></line></svg
                >
              </button>
            </div>
          </div>
        </div>
      {/each}
    </div>
  </div>
</div>

<div class="flex flex-col w-44 h-screen top-0 left-0 fixed bg-gray-600">
  <h1>hi</h1>
</div>

<style>
  @import './main.css';
  :global(body) {
    height: auto;
    overflow-y: scroll;
    background-color: #1e1f22;
    margin: 0;
    padding: 0;
  }
</style>
