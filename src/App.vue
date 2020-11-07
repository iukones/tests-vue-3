<template>
  <div id="nav">
    <router-link to="/episodes">Episodes</router-link> |
    <router-link to="/locations">locations</router-link> |
    <router-link to="/characters">Characters</router-link>
  </div>
  <router-view/>
  <hr />
  <nav>
    <div class="flex flex-col items-center my-12">
      <!-- {{info}} -->
      <div class="flex text-gray-700">
        <div class="h-8 w-8 mr-1 flex justify-center items-center rounded-full bg-gray-200 cursor-pointer">
          <router-link :to="prevComp">
            <svg xmlns="http://www.w3.org/2000/svg" width="100%" height="100%" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-chevron-left w-4 h-4">
                <polyline points="15 18 9 12 15 6"></polyline>
            </svg>
          </router-link>
        </div>
        <div class="flex h-8 font-medium rounded-full bg-gray-200">
            <div class="w-8 md:flex justify-center items-center hidden  cursor-pointer leading-5 transition duration-150 ease-in  rounded-full  ">1</div>
            <div class="w-8 md:flex justify-center items-center hidden  cursor-pointer leading-5 transition duration-150 ease-in  rounded-full  ">...</div>
            <div class="w-8 md:flex justify-center items-center hidden  cursor-pointer leading-5 transition duration-150 ease-in  rounded-full  ">3</div>
            <div class="w-8 md:flex justify-center items-center hidden  cursor-pointer leading-5 transition duration-150 ease-in  rounded-full bg-pink-600 text-white ">4</div>
            <div class="w-8 md:flex justify-center items-center hidden  cursor-pointer leading-5 transition duration-150 ease-in  rounded-full  ">5</div>
            <div class="w-8 md:flex justify-center items-center hidden  cursor-pointer leading-5 transition duration-150 ease-in  rounded-full  ">...</div>
            <div class="w-8 md:flex justify-center items-center hidden  cursor-pointer leading-5 transition duration-150 ease-in  rounded-full  ">15</div>
            <div class="w-8 h-8 md:hidden flex justify-center items-center cursor-pointer leading-5 transition duration-150 ease-in rounded-full bg-pink-600 text-white">4</div>
        </div>
        <div class="h-8 w-8 ml-1 flex justify-center items-center rounded-full bg-gray-200 cursor-pointer">
          <router-link :to="nextComp">
            <svg xmlns="http://www.w3.org/2000/svg" width="100%" height="100%" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-chevron-right w-4 h-4">
                <polyline points="9 18 15 12 9 6"></polyline>
            </svg>
          </router-link>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
  const { ref, provide, computed } = require('vue');
  const { useRoute } = require('vue-router');

  export const info = ref({
    count: 0,
    pages: 0,
    next: 0,
    prev: 0,
  });

  provide('info', info);

  export const route = useRoute();

  export const prevComp = computed(() => ({
    name: route.name,
    params: { page: info.value.prev || route.params.page },
  }));

  export const nextComp = computed(() => ({
    name: route.name,
    params: { page: info.value.next || route.params.page },
  }));

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
