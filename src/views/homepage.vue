<template>
  <navbar></navbar>
  <div class="bg-gray-50">
    <div class="mx-auto max-w-screen-xl px-4 py-32 lg:flex lg:h-screen lg:items-center">
      <div class="mx-auto max-w-xl text-center">
        <h1 class="text-3xl font-extrabold sm:text-5xl">
          A good barber
          <strong class="font-extrabold red-bag sm:block">
            is a good friend...
          </strong>
        </h1>

        <p class="mt-4 sm:text-xl sm:leading-relaxed">
          Best in Town ✂️
        </p>

        <div class="mt-8 flex flex-wrap justify-center gap-4">
          <a class="block w-full rounded red-bag px-12 py-3 text-sm font-medium text-white shadow hover:red-bag focus:outline-none focus:ring active:red-bag sm:w-auto"
            href="/get-started">
            Get Started
          </a>

          <a class="block w-full rounded px-12 py-3 text-sm font-medium text-red-600 shadow hover:red-bag focus:outline-none focus:ring active:text-red-500 sm:w-auto"
            href="/about">
            Learn More
          </a>
        </div>
      </div>
    </div>
  </div>
  <foot></foot>
</template>
<script>
import navbar from '../components/navbar.vue';
import foot from '../components/footer.vue';
export default {
  components: {
    navbar,
    foot
  }
}
</script>
<style scoped>

</style>