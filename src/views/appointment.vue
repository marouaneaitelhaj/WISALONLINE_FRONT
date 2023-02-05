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
      <h1 class="text-center text-2xl font-bold blue-txt sm:text-3xl">
        Get started today
      </h1>

      <p class="mx-auto mt-4 max-w-md text-center text-gray-500">
        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Obcaecati sunt
        dolores deleniti inventore quaerat mollitia?
      </p>

      <div class="mt-6 mb-0 space-y-4 rounded-lg p-8 shadow-2xl">
        <p class="text-lg font-medium">Sign in to your account</p>

        <div>
          <label for="day" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Select Day</label>

          <div class="relative mt-1">
            <select v-model="day"
              class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
              <option value="" selected hidden>Choose Day</option>
              <option value="lundi">Lundi</option>
              <option value="mardi">Mardi</option>
              <option value="mercredi">Mercredi</option>
              <option value="jeudi">Jeudi</option>
              <option value="vendredi">Vendredi</option>
              <option value="samedi">Samedi</option>
            </select>
          </div>
        </div>

        <div v-if="show">
          <label for="Hour" class="text-sm font-medium">Hour</label>
          <div class="relative mt-1">
            <select v-model="hourselected"
              class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
              <option selected hidden>Choose Hour</option>
              <option v-for="h in hour">{{ h }}</option>
            </select>
          </div>
        </div>

        <button v-on:click="now" class="block w-full rounded-lg blue-bag px-5 py-3 text-sm font-medium text-white">
          HSEEEEEEN LIYA
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
      day: '',
      show: false,
      hour: [],
      hourselected: '',
      dataappointment: []
    }
  },
  mounted() {
    this.read()
  },
  methods: {
    read() {
      axios.get('http://localhost/wiSalonline/public/api/Rappointments')
        .then(response => {
          this.dataappointment = response.data
          for (let i = 0; i < this.dataappointment.length; i++) {
            if (this.dataappointment[i].jour == this.day) {
              for (let j = 0; j < this.hour.length; j++) {
                if (this.dataappointment[i].heure == this.hour[j]) {
                  this.hour.splice(j, 1)
                }
              }
            }
          }
        })
    },
    now() {
      axios.post('http://localhost/wiSalonline/public/api/Cappointments', [this.day, this.hourselected, "sssssssss", "sssssssss"])
      .then(response => {
        this.read()
      })
    }
  },
  components: {
    navbar,
    foot
  },
  watch: {
    day: function () {
      this.read()
      this.show = true;
      if (this.day == 'lundi' || this.day == 'mardi' || this.day == 'mercredi' || this.day == 'jeudi' || this.day == 'samdi') {
        this.hour = ['9h - 10h', '10h - 11h', '11h - 12h', '14h - 15h', '15h - 16h', '16h - 17h', '17h - 18h', '18h - 19h', '19h - 20h']
      } else if (this.day == 'vendredi') {
        this.hour = ['9h - 10h', '10h - 11h', '11h - 12h', '16h - 17h', '17h - 18h', '18h - 19h', '19h - 20h', '20h - 21h', '21h - 22h']
      } else if (this.day == 'samedi') {
        this.hour = ['9h - 10h', '10h - 11h', '11h - 12h']
      }
      this.read()
    }
  }
}
</script>
<style scoped>

</style>