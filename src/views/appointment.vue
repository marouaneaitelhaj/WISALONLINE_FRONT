<template>
  <navbar></navbar>
  <alerterror v-if="alerterror"></alerterror>
  <alertsuccess v-if="alertsuccess"></alertsuccess>
  <div class="mainpage mx-auto max-w-screen-xl px-4 py-16 sm:px-6 lg:px-8">
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
            <div>
              <input min="today"
                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                v-model="month" type="date">
            </div>
          </div>
        </div>

        <div v-if="show">
          <!-- {{ taken }} -->
          <label for="Hour" class="text-sm font-medium">Hour</label>
          <div class="relative mt-1" v-for="h in hour">
            <!-- <select v-model="hourselected"
              class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
              <option value="" selected hidden>Choose Hour</option>
              <option v-for="h in hour">{{ h }}</option>
            </select> -->

            <div v-if="taken.hour.includes(h) && taken.client[taken.hour.indexOf(h)] == local" v-on:click="now(h)"
              class="transform  hover:scale-105 transition duration-300 shadow-xl rounded-lg  p-4 bg-blue-200">
              {{ h }}
            </div>
            <div v-else-if="taken.hour.includes(h) && taken.client.includes(h) !== local" v-on:click="now(h)"
              class="transform  hover:scale-105 transition duration-300 shadow-xl rounded-lg  p-4 bg-red-200">
              {{ h }}
            </div>
            <div v-if="!taken.hour.includes(h)" v-on:click="now(h)"
              class="transform  hover:scale-105 transition duration-300 shadow-xl rounded-lg  p-4 bg-white">
              {{ h }}
            </div>
          </div>
        </div>

        <!-- <button v-on:click="now" class="block w-full rounded-lg blue-bag px-5 py-3 text-sm font-medium text-white">
          HSEEEEEEN LIYA
        </button> -->

      </div>
    </div>
  </div>

  <foot></foot>
</template>
<script>
import navbar from '../components/navbar.vue';
import foot from '../components/footer.vue';
import alertsuccess from '../components/alertsuccess.vue'
import alerterror from '../components/alerterror.vue'
export default {
  data() {
    return {
      day: '',
      local: localStorage.getItem('key'),
      show: false,
      hour: [],
      taken: {
        hour: [],
        client: []
      },
      hourselected: '',
      dataappointment: [],
      id: '',
      alertsuccess: false,
      alerterror: false,
      month: '',
      week: ''
    }
  },
  mounted() {
    this.hour = ['9h - 10h', '10h - 11h', '11h - 12h', '14h - 15h', '15h - 16h', '16h - 17h', '17h - 18h', '18h - 19h', '19h - 20h']
    // if (localStorage.getItem('key') == null) {
    //   this.$router.push('/login')
    // }
    this.read()
    axios.post('http://localhost/wiSalonline/public/FromKeyToId', [localStorage.getItem('key')])
      .then(response => {
        this.id = response.data[0].id
      })
  },
  methods: {
    alertshowFUNC() {
      this.alertsuccess = false
    },
    alerterrorFUNC() {
      this.alerterror = false
    },
    read() {
      this.taken.hour = []
      this.taken.client = []
      axios.get('http://localhost/wiSalonline/public/api/Rappointments')
        .then(response => {
          this.dataappointment = response.data
          for (let i = 0; i < this.dataappointment.length; i++) {
            if (this.dataappointment[i].jour == this.day || this.dataappointment[i].date == this.day) {
              for (let j = 0; j < this.hour.length; j++) {
                if (this.dataappointment[i].heure == this.hour[j] && this.dataappointment[i].date == this.month) {
                  this.taken.hour.push(this.hour[j])
                  this.taken.client.push(this.dataappointment[i].reference)
                }
              }
            }
          }
        })
    },
    now(hourselected) {
      if (this.taken.hour.includes(hourselected)) {
        this.alerterror = true
        setTimeout(this.alerterrorFUNC, 3000)
        return
      } else {
        axios.post('http://localhost/wiSalonline/public/api/Cappointments', [this.day, hourselected, this.id, this.month])
          .then(response => {
            console.log(response)
            this.read()
            this.alertsuccess = true
            setTimeout(this.alertshowFUNC, 3000)
            this.hourselected = ''
          })
      }
    }
  },
  components: {
    navbar,
    foot,
    alertsuccess,
    alerterror
  },
  watch: {
    day: function () {
      this.read()
      this.show = true;
      if (this.day == 'Monday' || this.day == 'Tuesday' || this.day == 'Wednesday' || this.day == 'Thursday' || this.day == 'Saturday') {
        this.hour = ['9h - 10h', '10h - 11h', '11h - 12h', '14h - 15h', '15h - 16h', '16h - 17h', '17h - 18h', '18h - 19h', '19h - 20h']
      } else if (this.day == 'Friday') {
        this.hour = ['9h - 10h', '10h - 11h', '11h - 12h', '16h - 17h', '17h - 18h', '18h - 19h', '19h - 20h', '20h - 21h', '21h - 22h']
      } else if (this.day == 'Sunday') {
        this.hour = ['9h - 10h', '10h - 11h', '11h - 12h']
      }
      this.read()
    },
    month: function () {
      this.read()
      let input = new Date(this.month);
      let dayName = input.toLocaleString("default", { weekday: "long" });
      this.day = dayName
      this.read()

    }
  }
}
</script>
<style scoped></style>