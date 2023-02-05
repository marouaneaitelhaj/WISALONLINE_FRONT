<template>
  <header aria-label="Site Header" class="bg-white">
    <div class="mx-auto max-w-screen-xl px-4 sm:px-6 lg:px-8">
      <div class="flex h-16 items-center justify-between">
        <div class="flex-1 md:flex md:items-center md:gap-12">
          <router-link to="/" class="block text-teal-600">
            <span class="sr-only">Home</span>
            <p class="font-black blue-txt  text-3xl">WiBarber</p>
          </router-link>
        </div>
        <div class="md:flex md:items-center md:gap-12">
          <nav aria-label="Site Nav" class="hidden md:block">
            <ul class="flex items-center gap-6 text-sm">
              <li>
                <router-link class="text-black font-semibold transition hover:text-gray-500/75" to="/">
                  Home
                </router-link>
              </li>

              <li>
                <router-link class="text-black font-semibold transition hover:text-gray-500/75" to="/appointment">
                  Appointment
                </router-link>
              </li>
            </ul>
          </nav>

          <div v-if="show" class="flex items-center gap-4">
            <div class="sm:flex sm:gap-4">
              <router-link class="rounded-md blue-bag px-5 py-2.5 text-sm font-medium text-white shadow" to="/login">
                Login
              </router-link>
              <div class="hidden sm:flex">
                <router-link class="rounded-md text-white  red-bag px-5 py-2.5 text-sm font-medium text-teal-600"
                  to="/register">
                  Register
                </router-link>
              </div>
            </div>
            <div class="block md:hidden">
              <button class="rounded red-bag p-2 text-gray-600 transition hover:text-gray-600/75">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24"
                  stroke="currentColor" stroke-width="2">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M4 6h16M4 12h16M4 18h16" />
                </svg>
              </button>
            </div>
          </div>
          <div v-if="!show" class="flex items-center gap-4">
            <div class="sm:flex sm:gap-4">
              <button class="rounded-md blue-bag px-5 py-2.5 text-sm font-medium text-white shadow" v-on:click="logout">
                Logout
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </header>

</template>
<script>
export default {
  data() {
    return {
      show: true
    }
  },
  methods: {
    logout() {
      console.log("logout")
      // how to delete cookie
      document.cookie = "key=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;"
      this.$router.push('/')
      this.show = true
    }
  },
  mounted() {
    if (document.cookie != "") {
      this.show = false
    }
  },
}
</script>
<style scoped>

</style>