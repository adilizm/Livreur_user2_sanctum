<template>
  <div class="flex justify-center items-center pt-3 pb-2 ">
    <router-link class=" text-sm font-medium uppercase text-gray-600 hover:text-gray-800 hover:no-underline focus:text-red-300 px-2 " @click="store.methodes.showCategoreis" :class="{text_dark_mode:store.state.active_dark_mode }"  :to="{ name: 'categoreis' }"> {{  store.methodes.language("categoreis") }}</router-link>
    <span class=" text-sm font-medium text-gray-600 " :class="{text_dark_mode:store.state.active_dark_mode }"  > -</span>
    <router-link class=" text-sm font-medium uppercase text-gray-600 hover:text-gray-800 hover:no-underline  focus:text-red-300  px-2" @click="store.methodes.showOrders" :class="{text_dark_mode:store.state.active_dark_mode }"  :to="{ name: 'orders' }" > {{  store.methodes.language("orders") }}</router-link>
  </div>
  
</template>

<script>
import { inject } from "vue";
export default {
  setup() {
    const store = inject("store");

 function language(key) {
      if (store.state.language == "ar") {
        return store.state.ar[key];
      } else {
        return store.state.en[key];
      }
    }
    return { store ,language};
  },
};
</script>

<style>
.link {
  font-variant: all-small-caps;
  font-weight: 700;
  padding: 10px;
}
</style>