<template>
  <navbar></navbar>
  <div class="mx-auto max-w-screen-xl px-4 py-16 sm:px-6 lg:px-8">
    <div class="mx-auto max-w-lg">
      <h1 class="text-center text-2xl font-bold blue-bag sm:text-3xl">
        Get started today
      </h1>

      <p class="mx-auto mt-4 max-w-md text-center text-gray-500">
        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Obcaecati sunt
        dolores deleniti inventore quaerat mollitia?
      </p>

      <div class="mt-6 mb-0 space-y-4 rounded-lg p-8 shadow-2xl">
        <p class="text-lg font-medium">Sign in to your account</p>
        <div v-if="error" class="p-4 mb-4 text-sm text-red-800 rounded-lg bg-red-50 dark:bg-gray-800 dark:text-red-400"
          role="alert">
          <span class="font-medium">Warning!</span> Change a few things up and try submitting again.
        </div>
        <div>
          <label for="name" class="text-sm font-medium">Name</label>

          <div class="relative mt-1">
            <input type="text" v-model="name" class="w-full rounded-lg border-gray-200 p-4 pr-12 text-sm shadow-sm"
              placeholder="Enter your name" required />

            <span class="absolute inset-y-0 right-4 inline-flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24"
                stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M16 12a4 4 0 10-8 0 4 4 0 008 0zm0 0v1.5a2.5 2.5 0 005 0V12a9 9 0 10-9 9m4.5-1.206a8.959 8.959 0 01-4.5 1.207" />
              </svg>
            </span>
          </div>
        </div>
        <div>
          <label for="email" class="text-sm font-medium">Email</label>

          <div class="relative mt-1">
            <input type="email" v-model="email" class="w-full rounded-lg border-gray-200 p-4 pr-12 text-sm shadow-sm"
              placeholder="Enter your email" required />

            <span class="absolute inset-y-0 right-4 inline-flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24"
                stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M16 12a4 4 0 10-8 0 4 4 0 008 0zm0 0v1.5a2.5 2.5 0 005 0V12a9 9 0 10-9 9m4.5-1.206a8.959 8.959 0 01-4.5 1.207" />
              </svg>
            </span>
          </div>
        </div>

        <div>
          <label for="password" class="text-sm font-medium">Number phone</label>

          <div class="relative mt-1">
            <input type="text" v-model="numberphone" class="w-full rounded-lg border-gray-200 p-4 pr-12 text-sm shadow-sm"
              placeholder="Enter your number phone" required />

            <span class="absolute inset-y-0 right-4 inline-flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24"
                stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
              </svg>
            </span>
          </div>
        </div>

        <button v-if="champe" v-on:click="signup"
          class="block w-full rounded-lg blue-bag px-5 py-3 text-sm font-medium text-white">
          Sign up
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
      name: '',
      numberphone: '',
      email: '',
      error: false
    }
  },
  mounted() {
    if (localStorage.getItem('key') != null) {
      this.$router.push('/')
    }
  },
  methods: {
    signup() {
      if (this.name == '' || this.numberphone == '' || this.email == '') {
        this.error = true
      } else {
        this.error = false
        axios.post('http://localhost/wiSalonline/public/signup', [this.name, this.numberphone, this.email])
          .then(response => {
            // this.$router.push('/login')
            console.log(response.data)
            if (response.data == 'good') {
              this.$router.push('/login')
            }
          })
      }
    }
  },
  components: {
    navbar,
    foot
  },
  computed: {
    champe() {
      if (this.name == '' || this.numberphone == '' || this.email == '') {
        return false
      } else {
        return true
      }
    }
  }
}
</script>
<style scoped></style>