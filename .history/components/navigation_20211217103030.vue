<template>
  <nav>
    <!-- <a href="/">Menü</a> !-->

    <div class="dropdown inline-block relative">
      <button
        class="
          text-white
          font-semibold
          py-2
          px-4
          rounded
          inline-flex
          items-center
        "
      >
        <img class="fixed" src="../assets/img/logo.svg" alt="Abstraktes Logo" />
      </button>
      <ul class="dropdown-content absolute hidden pt-10">
        <li>
          <NuxtLink
            class="bg-black hover:bg-red-600 py-2 px-4 block"
            to="/home"
            >Home</NuxtLink
          >
        </li>
        <li>
          <NuxtLink
            class="bg-black  hover:bg-gray-800 py-2 px-4 block"
            to="/impressum"
            >Impressum</NuxtLink
          >
        </li>
        <li>
          <NuxtLink
            class="bg-black  hover:bg-gray-800 py-2 px-4 block"
            to="/datenschutz"
            >Datenschutz</NuxtLink
          >
        </li>
      </ul>
    </div>
  </nav>
</template>

<style>
.dropdown:hover > .dropdown-content {
  display: block;
}
</style>