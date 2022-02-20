<template>
  <div class="h-full">
    <Modal :show="showModal" @close="showModal = false">
      <template #header>
        <h3>Add New Utilities</h3>
      </template>
      <template #body>
        <div class="flex flex-col gap-2">
          <div class="grid grid-cols-4 items-center">
            <label for="" class="">Nama: </label>
            <input
              type="text"
              name="utilties-name"
              class="border-b border-gray-400 h-10 p-2 col-span-3"
              placeholder="TNB/SYABAS/UNIFI"
              required
            />
          </div>
          <div class="grid grid-cols-4 items-center">
            <label for="" >Bill: </label>
            <input
              type="number"
              name="utilties-name"
              class="border-b border-gray-400 h-10 p-2 col-span-3"
              placeholder="500"
              value=""
              required
            />
          </div>
        </div>
      </template>
    </Modal>
    <div class="h-full flex flex-col">
      <div
        class="h-18 bg-gray-100 shadow-md p-4 border-b border-gray-200 flex text-center justify-center"
      >
        <h1 class="text-2xl font-bold">Kira Sewa App</h1>
      </div>
      <div class="flex-1 flex flex-col gap-4 mx-2 mt-8 overflow-scroll">
        <div class="flex flex-col">
          <label for="" class="mb-2">Harga Sewa (per month): </label>
          <input
            type="number"
            name="price"
            class="border-b border-gray-400 h-10 p-2"
            placeholder="1200"
            value="100"
            required
          />
        </div>
        <div class="flex flex-col">
          <label for="" class="mb-2">Bilangan Penyewa: </label>
          <input
            type="number"
            name="count"
            class="border-b border-gray-400 h-10 p-2"
            placeholder="5"
            value="1"
            required
          />
        </div>
        <div class="mt-2">
          <button
            class="bg-blue-400 px-3 py-2 text-white font-semibold h-10 rounded-lg"
            @click="showModal = true"
          >
            Add utilities
          </button>
        </div>
      </div>
      <div class="justify-end flex-none">
        <Footer text="Kira Sekarang" link="/result"></Footer>
      </div>
    </div>
  </div>
</template>

<script>
import Footer from "~/components/Footer/Footer.vue";
import Modal from "~/components/Modal/Modal.vue";
export default {
  components: { Footer, Modal },
  name: "IndexPage",
  data() {
    return {
      showModal: false,
      harga: 0,
      count: 1,
      utilities: [],
    };
  },
  head() {
    return {
      title: "Kira Sewa App",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Tutorial page",
        },
      ],
    };
  },
};
</script>
