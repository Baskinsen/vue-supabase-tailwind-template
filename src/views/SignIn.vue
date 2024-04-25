<template>
  <div class="flex w-full h-screen items-center flex-col m-auto">
    <div class="m-auto shadow-md flex flex-col gap-10 px-10 py-10 bg-gray-200">
      <h1 class="text-center text-xl font-semibold">Sign In</h1>
      <form class="flex flex-col gap-10" @submit.prevent="handleSubmit()">
        <section class="flex flex-col gap-5">
          <label for="email" class="text-lg">Email</label>
          <input
            type="email"
            id="email"
            v-model="user.email"
            required
            class="w-full rounded-md px-5 py-3"
            placeholder="johndoe@email.com"
          />
        </section>
        <section class="flex flex-col gap-5">
          <label for="password" class="text-lg">Password</label>
          <input
            type="password"
            id="password"
            v-model="user.password"
            required
            class="w-full rounded-md px-5 py-3"
            placeholder="********"
          />
        </section>
        <section class="flex gap-20">
          <button class="bg-green-300 px-10 py-3 rounded-md text-[#fafafa]" type="submit">
            Sign In
          </button>
          <a href="/signup" class="my-auto text-[#60A5FA]">Dont Have an Account? Sign Up</a>
        </section>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { supabase } from "../lib/supabase";
import { useRouter } from "vue-router";

const router = useRouter()
const user = ref({
  email: "",
  password: "",
});

const handleSubmit = async () => {
    try{
       
        const {error} = await supabase.auth.signInWithPassword({
            email: user.value.email,
            password: user.value.password
        })
        if(error) throw error
        router.push('/')
    }catch(error){
        console.error(error.message)
    } finally {
        
    }
}
</script>

<style></style>
