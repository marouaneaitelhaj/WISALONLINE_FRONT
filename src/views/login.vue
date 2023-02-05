<template>
  <navbar></navbar>
  <!--
    This component uses @tailwindcss/divs
  
    yarn add @tailwindcss/divs
    npm install @tailwindcss/divs
  
    plugins: [require('@tailwindcss/divs')]
  -->

  <div class="mx-auto max-w-screen-xl px-4 py-16 sm:px-6 lg:px-8">
    <div class="mx-auto max-w-lg">
      <h1 class="text-center text-2xl font-bold text-indigo-600 sm:text-3xl">
        Get started today
      </h1>

      <p class="mx-auto mt-4 max-w-md text-center text-gray-500">
        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Obcaecati sunt
        dolores deleniti inventore quaerat mollitia?
      </p>

      <div action="" class="mt-6 mb-0 space-y-4 rounded-lg p-8 shadow-2xl">
        <p class="text-lg font-medium">Sign in to your account</p>

        <div>
          <label for="key" class="text-sm font-medium">Key</label>

          <div class="relative mt-1">
            <input type="text" v-model="key" class="w-full rounded-lg border-gray-200 p-4 pr-12 text-sm shadow-sm"
              placeholder="Enter key" />

            <span class="absolute inset-y-0 right-4 inline-flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24"
                stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M16 12a4 4 0 10-8 0 4 4 0 008 0zm0 0v1.5a2.5 2.5 0 005 0V12a9 9 0 10-9 9m4.5-1.206a8.959 8.959 0 01-4.5 1.207" />
              </svg>
            </span>
          </div>
        </div>

        

        <button type="submit" v-on:click="login" class="block w-full rounded-lg bg-indigo-600 px-5 py-3 text-sm font-medium text-white">
          Sign in
        </button>

      </div>
    </div>
  </div>

  <foot></foot>
</template>
<script>
import navbar from '../components/navbar.vue';
import foot from '../components/footer.vue';
export default {
  data() {
    return {
      key: ''
    }
  },
  mounted(){
    if(document.cookie != ""){
      this.$router.push('/')
    }
  },
  methods: {
    login() {
      axios.post('http://localhost/wiSalonline/public/login', [this.key])
        .then(response => {
          console.log(response.data)
          if (response.data == 1) {
            document.cookie = "key=" + this.key
            this.$router.push('/')
          } else {
            alert('Invalid Key')
          }
        })
    }
  },
  components: {
    navbar,
    foot
  }
}
</script>
<style scoped>

</style>