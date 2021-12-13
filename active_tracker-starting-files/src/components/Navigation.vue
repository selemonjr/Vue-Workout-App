<template>
  <header class="bg-at-light-green text-white">
    <nav class="container py-5 px-4 flex flex-col gap-4 items-center sm:flex-row">
      <div class="flex items-center gap-x-4 ">
        <img class="w-14" src="../assets/images/dumbbell-light.png" alt="">
        <h1 class="text-lg">Active Tracker</h1>
      </div>
      <ul class="flex flex-1 justify-end gap-x-10">
        <router-link class="cursor-pointer" :to="{name:'Home'}">Home</router-link>
         <router-link v-if="user" class="cursor-pointer" :to="{name:'Create'}">Create</router-link>
          <router-link v-if="!user" class="cursor-pointer" :to="{name:'Login'}">Login</router-link>
          <li v-if="user" class="cursor-pointer" @click="LogOut">
            Logout
          </li>
      </ul>
    </nav>
  </header>
</template>

<script>
import {supabase} from "../supabase/init";
import { useRouter } from "vue-router";
import store from "../store/index";
import {computed} from "vue";
export default {
  setup() {
    const user = computed(() => {
      return store.state.user
    });

    const router = useRouter();
    const LogOut = async () => {
      await supabase.auth.signOut();
      router.push({name:"Login"})
    }

    return {
      LogOut,
      user
    };
  },
};
</script>
