<template>
  <nav class=" bg-gray-50 shadow-md z-10 flex justify-between">
    <a class="navbar-brand pl-3 d-flex justify-content-center text-center items-center" href="#">
      <img class=" align-middle mx-2" src="/images/logo.png" width="50" height="50" alt="" /> 
      <span class=" capitalize text-xl text-blue-500 font-bold" style=" font-family:Goblin One">Livraison</span>
    </a>
   <div v-if="store.state.userconected || store.state.livreurconected"  @click="store.methodes.logout" class="mr-3 cursor-pointer  justify-center items-center hover:text-gray-900   flex font-medium  transform hover:-translate-x-4 transition ease-in-out"> <span>Logout</span> <span><svg xmlns="http://www.w3.org/2000/svg" class="ml-2 w-6 " fill="none" viewBox="0 0 24 24" stroke="currentColor">
  <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1" />
</svg></span> </div>
  </nav>
</template>

<script>
import { inject } from "vue";
export default {
  setup() {
    const store = inject("store");
    return { store };
  },
};
</script>
 
<style>
.nav-link {
  cursor: pointer;
}
@media only screen and (max-width: 600px) {
  .navnav {
    margin-left: 45vw;
  }
}
@media only screen and (min-width: 601px) {
  .navnav {
    margin-left: 47vw;
  }
}
@media only screen and (min-width: 992px) {
  .navnav {
    margin-left: 75vw;
  }
}
</style>
