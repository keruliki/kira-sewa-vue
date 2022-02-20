<template>
  <div class="h-full">
    <Modal :show="showModal" @close="modalClose"></Modal>
    <div class="h-full flex flex-col">
      <div
        class="h-18 bg-gray-100 shadow-md p-4 border-b border-gray-200 flex text-center justify-center relative"
      >
        <div class="absolute left-4">
            <button @click="reset()" class="h-full float-left bg-red-600 rounded-md py-2 px-3 text-white text-xs">Reset</button>
        </div>
        <h1 class="text-2xl font-bold">Kira Sewa App</h1>
      </div>
      <div class="flex-1 flex flex-col gap-4 mx-2 mt-8 overflow-scroll">
        <div class="flex flex-col">
          <label for="" class="mb-2">Harga Sewa (per month): </label>
          <input
            @keyup="calculate"
            type="number"
            name="price"
            v-model="price"
            class="border-b border-gray-400 h-10 p-2"
            placeholder="1200"
            value="100"
            required
          />
        </div>
        <div class="flex flex-col">
          <label for="" class="mb-2">Bilangan Penyewa: </label>
          <input
            @keyup="calculate"
            type="number"
            name="count"
            v-model="count"
            class="border-b border-gray-400 h-10 p-2"
            placeholder="5"
            value="1"
            required
          />
        </div>
        <div class="mt-2">
          <button
            class="bg-blue-400 px-3 py-2 text-white font-semibold h-10 rounded-lg w-full"
            @click="showModal = true"
          >
            Add utilities
          </button>
        </div>
        <div class="border-b border-gray-300 my-2"></div>
        <div v-for="(task, index) in utilities" :key="index" class="border border-gray-300 py-2 px-4 rounded-md flex justify-between items-center">
            <div>
                <p class="text-base font-bold mb-1">{{task.name}}</p>
                <p class="text-sm text-gray-700">RM {{task.value}}</p>
            </div>
            <div>
                <button @click="remove(task, index)" class="bg-red-600 p-2 text-white w-8 h-8 rounded-md text-xs">X</button>
            </div>
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
      price: 0,
      count: 1,
      utilities: [],
      taskSelected: [],
    };
  },
  mounted() {
    if (typeof window !== 'undefined') {
    console.log('You are on the browser')
    // 👉️ can use localStorage here
    this.utilities = (localStorage.getItem("tasks")) ? JSON.parse(localStorage.getItem("tasks")) : []
    this.price = (localStorage.getItem("price")) ? localStorage.getItem("price") : 0
    this.count = (localStorage.getItem("count")) ? localStorage.getItem("count") : 0
    }
    else {
    console.log('You are on the server')
    // 👉️ can't use localStorage
    }
  },

  methods: {
    remove(task, index) {
      this.taskSelected = task
      this.taskSelected.index = index
      this.utilities.splice(this.taskSelected.index, 1)
      localStorage.setItem("tasks", JSON.stringify(this.utilities))
    },
    modalClose() {
      this.showModal = false;
      this.utilities = (localStorage.getItem("tasks")) ? JSON.parse(localStorage.getItem("tasks")) : []
    },
    calculate()
    {
        localStorage.setItem("price", this.price)
        localStorage.setItem("count", this.count)
    },
    reset(){
        localStorage.removeItem("tasks")
        localStorage.removeItem("price")
        localStorage.removeItem("count")
        this.utilities = []
        this.price = 0
        this.count = 1
    }
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
