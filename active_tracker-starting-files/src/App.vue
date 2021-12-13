<template>
  <div bv-if="appReady" class="min-h-full font-Poppins box-border">
    <Navigation/>
    <router-view />
  </div>
</template>

<script>
import Navigation from "./components/Navigation.vue";
import {supabase} from "./supabase/init";
import {ref} from "vue";
import store from "./store";
export default {
  name:"App",
  components: {
    Navigation,
  },
  setup() {
    const appReady = ref(null);
    const user = supabase.auth.user();
    if(!user) {
      appReady.value = true;
    }
    supabase.auth.onAuthStateChange((_,session) => {
      console.log(user.email)
      store.methods.setUser(session);
      appReady.value = true;
    })

    return {
      appReady
    };
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@100;200;300;400;500;600;700&display=swap");
</style>
