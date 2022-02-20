<template>
  <div class="h-full flex flex-col">
      <div class="h-18 bg-gray-100 shadow-md p-4 border-b border-gray-200 flex text-center justify-center">
          <h1 class="text-2xl font-bold">Kira Sewa App</h1>
          
      </div>
      <div class="flex-1 flex flex-col justify-center items-center w-3/4 mx-auto text-center">
        <p class="text-center text-lg font-semibold">Hi Selamat Datang Ke KiraSewa Apps. Kini Pengiraan Sewa Rumah Lebih Mudah</p>
      </div>
      <div class="justify-end flex-none">
        <Footer text='Get Started' link="/kira"></Footer>
      </div>
    </div>
</template>

<script>
import Footer from '~/components/Footer/Footer.vue';
export default {
  components: { Footer},
  name: 'IndexPage',

  head() {
    return {
      title: 'Kira Sewa App',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Tutorial page',
        },
      ],
    };
  },
}
</script>

<style>

