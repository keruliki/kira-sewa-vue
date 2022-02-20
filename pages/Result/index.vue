<template>
  <div class="h-full">
    <div class="h-full flex flex-col">
      <div
        class="h-18 bg-gray-100 shadow-md p-4 border-b border-gray-200 flex text-center justify-center  items-center relative"
      >
        <div class="absolute left-4">
            <button @click="goToPrev()" class="h-full float-left bg-blue-600 rounded-md py-2 px-3 text-white text-xs">Back</button>
        </div>
        <h1 class="text-2xl font-bold text-center">Kira Sewa App</h1>
      </div>
      <div class="flex-1 flex flex-col gap-4 mx-4 mt-8 overflow-scroll">
        <h4 class="text-lg mb-2 font-bold">Calculation Result</h4>
        <div>
          <textarea
            name=""
            id=""
            rows="10"
            class="border border-gray-400 rounded-md p-2 resize-none w-full"
            id="result"
            v-model="textResult"
          ></textarea>
        </div>
      </div>
      <div class="justify-end flex-none">
        <div class="grid grid-cols-2 px-4 mb-4">
          <div><h3 class="text-lg font-bold">Jumlah:</h3></div>
          <div class="flex justify-end">RM {{ totalPrice }}</div>
          <div><h3 class="text-lg font-bold">Sewa Per Head:</h3></div>
          <div class="flex justify-end">RM {{ pricePerHead }}</div>
        </div>
        <div class="h-20 bg-gray-100 shadow-md p-4">
          <button
            @click="copy"
            class="w-full rounded-lg text-white bg-blue-400 h-full"
          >
            Salin
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      totalPrice: 0,
      pricePerHead: 0,
      textResult: "",
      utilities: [],
      price: 0,
      count: 0,
    };
  },
  mounted() {
    if (typeof window !== "undefined") {
      console.log("You are on the browser");
      // 👉️ can use localStorage here
      this.utilities = localStorage.getItem("tasks")
        ? JSON.parse(localStorage.getItem("tasks"))
        : [];
      this.price = localStorage.getItem("price")
        ? localStorage.getItem("price")
        : 0;
      this.count = localStorage.getItem("count")
        ? localStorage.getItem("count")
        : 0;

      this.totalPrice += parseInt(this.price);
      this.utilities.forEach((element) => {
        this.totalPrice += parseInt(element.value);
      });

      this.pricePerHead = this.totalPrice / this.count;

      this.textResult =
        "Hi Gais. \n\nTotal Sewa untuk bulan ni : RM " +
        this.totalPrice +
        "\nSewa Per Head : RM " +
        this.pricePerHead +
        "\n";

      document.getElementById("result").value = this.textResult;
    } else {
      console.log("You are on the server");
      // 👉️ can't use localStorage
    }
  },

  methods: {
    copy() {
      let testingCodeToCopy = document.querySelector("#result");

      testingCodeToCopy.select();
      try {
        var successful = document.execCommand("copy");
        alert("Copied to clipboard");
      } catch (err) {
        alert("Oops, unable to copy");
      }
    },
    goToPrev() {
    this.$router.go(-1);
  },
  },
};
</script>

<style></style>
