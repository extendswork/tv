<script>
  import { query, hasQuery, search } from '../store.js'
  import { onMount } from 'svelte'
  import SearchFieldMini from './SearchFieldMini.svelte'

  export let withSearch = false

  let dark = false
  function toggleDarkMode() {
    let mode = localStorage.theme || 'light'
    if (mode === 'dark' || window.matchMedia('(prefers-color-scheme: dark)').matches) {
      dark = false
      document.documentElement.classList.remove('dark')
      localStorage.theme = 'light'
    } else {
      dark = true
      document.documentElement.classList.add('dark')
      localStorage.theme = 'dark'
    }
  }

  function reset() {
    document.body.scrollIntoView()
    query.set('')
    hasQuery.set(false)
    search('')
  }

  onMount(() => {
    let mode = localStorage.theme || 'light'
    if (mode === 'dark' || window.matchMedia('(prefers-color-scheme: dark)').matches) {
      dark = true
    } else {
      dark = false
    }
  })
</script>

<nav
  class="bg-white border-b border-gray-200 px-2 sm:px-4 py-2.5 dark:border-gray-600 dark:bg-gray-800"
>
  <div class="container flex justify-between items-center max-w-6xl mx-auto px-4 sm:px-2">
    <div class="flex flex-start items-center basis-[24rem] shrink">
      <a href="/" on:click="{() => {reset()}}" class="flex mr-6">
        <span
          class="text-[1.15rem] text-[#24292f] self-center font-semibold whitespace-nowrap dark:text-white font-mono"
          >Onlive</span
        >
      </a>
      {#if withSearch}
      <SearchFieldMini />
      {/if}
    </div>

    <div class="flex flex-end items-center">
      <button
        type="button"
        on:click="{toggleDarkMode}"
        class="text-gray-500 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-700 rounded-full text-sm p-2.5"
        aria-label="Toggle Dark Mode"
      >
        <svg
          class="w-5 h-5"
          class:hidden="{dark}"
          fill="currentColor"
          viewBox="0 0 20 20"
          xmlns="http://www.w3.org/2000/svg"
          aria-hidden="true"
          focusable="false"
          role="img"
        >
          <path d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z"></path>
        </svg>
        <svg
          class="w-5 h-5"
          class:hidden="{!dark}"
          fill="currentColor"
          viewBox="0 0 20 20"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M10 2a1 1 0 011 1v1a1 1 0 11-2 0V3a1 1 0 011-1zm4 8a4 4 0 11-8 0 4 4 0 018 0zm-.464 4.95l.707.707a1 1 0 001.414-1.414l-.707-.707a1 1 0 00-1.414 1.414zm2.12-10.607a1 1 0 010 1.414l-.706.707a1 1 0 11-1.414-1.414l.707-.707a1 1 0 011.414 0zM17 11a1 1 0 100-2h-1a1 1 0 100 2h1zm-7 4a1 1 0 011 1v1a1 1 0 11-2 0v-1a1 1 0 011-1zM5.05 6.464A1 1 0 106.465 5.05l-.708-.707a1 1 0 00-1.414 1.414l.707.707zm1.414 8.486l-.707.707a1 1 0 01-1.414-1.414l.707-.707a1 1 0 011.414 1.414zM4 11a1 1 0 100-2H3a1 1 0 000 2h1z"
            fill-rule="evenodd"
            clip-rule="evenodd"
          ></path>
        </svg>
      </button>
    </div>
  </div>
</nav>
