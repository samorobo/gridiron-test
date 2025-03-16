<template>
  <section class="mx-auto max-w-2xl px-4 sm:pb-6 lg:max-w-7xl lg:px-8">
    <div class="mb-8 flex flex-wrap justify-between md:mb-16">
      <div class="mb-6 flex w-full flex-col justify-center sm:mb-12 lg:mb-0 lg:w-1/3 lg:pb-24 lg:pt-48">
        <h1 class="mb-4 text-4xl font-bold text-black sm:text-5xl md:mb-8 md:text-6xl">
          Top Fashion for a top price!
        </h1>
        <p class="max-w-md leading-relaxed text-gray-500 xl:text-lg">
          We sell only the most exclusive and high quality products for you.
          We are the best so come and shop with us.
        </p>
      </div>

      <div class="mb-12 flex w-full md:mb-16 lg:w-2/3">
        <div class="relative left-12 top-12 z-10 -ml-12 overflow-hidden rounded-lg bg-gray-100 shadow-lg md:left-16 md:top-16 lg:ml-0">
          <img
            :src="womanListen"
            alt="Great Photo"
            class="h-full w-full object-cover object-center"
            width="500"
            height="500"
          />
        </div>

        <div class="overflow-hidden rounded-lg bg-gray-100 shadow-lg">
          <img
            :src="manListen"
            alt="Great Photo"
            class="h-full w-full object-cover object-center"
            width="500"
            height="500"
          />
        </div>
      </div>
    </div>

    <div class="flex flex-col items-center justify-between gap-8 md:flex-row">
      <div class="flex h-12 w-64 divide-x overflow-hidden rounded-lg border">
        <router-link
          to="/Men"
          class="flex w-1/3 items-center justify-center text-gray-500 transition duration-100 hover:bg-gray-100 active:bg-gray-200"
        >
          Men
        </router-link>
        <router-link
          to="/Women"
          class="flex w-1/3 items-center justify-center text-gray-500 transition duration-100 hover:bg-gray-100 active:bg-gray-200"
        >
          Women
        </router-link>
        <router-link
          to="/Teens"
          class="flex w-1/3 items-center justify-center text-gray-500 transition duration-100 hover:bg-gray-100 active:bg-gray-200"
        >
          Teens
        </router-link>
      </div>
    </div>
  </section>
</template>

<script setup>
import manListen from '@/assets/images/man-listen.jpg';
  import womanListen from '@/assets/images/woman-listen.jpg';
// If you want to fetch data (like with Sanity), you could use Vue’s Composition API.
// For now, the data fetching code is commented out as in your original React component.

// import { ref, onMounted } from 'vue';
// async function getData() {
//   const query = "*[_type == 'heroImage'][0]";
//   // const data = await client.fetch(query);
//   // return data;
// }
// const data = ref(null);
// onMounted(async () => {
//   data.value = await getData();
// });
</script>

<!-- You can add scoped styles if needed -->
<style scoped>
/* Add any component-specific styles here */
</style>
