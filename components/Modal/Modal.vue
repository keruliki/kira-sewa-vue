

<template>
  <Transition name="modal">
    <div v-if="show" class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
          <div class="modal-header flex justify-between">
            <h3>Add New Utilities</h3>
            <button class="modal-default-button" @click="$emit('close')">
              X
            </button>
          </div>
          <div class="modal-body">
            <div class="flex flex-col gap-2">
              <div class="grid grid-cols-4 items-center">
                <label for="" class="">Nama: </label>
                <input
                  type="text"
                  name="name"
                  v-model="utilities.name"
                  class="border-b border-gray-400 h-10 p-2 col-span-3"
                  placeholder="TNB/SYABAS/UNIFI"
                  required
                />
              </div>
              <div class="grid grid-cols-4 items-center">
                <label for="">Bill: </label>
                <input
                  type="number"
                  name="value"
                  v-model="utilities.value"
                  class="border-b border-gray-400 h-10 p-2 col-span-3"
                  placeholder="500"
                  value=""
                  required
                />
              </div>
            </div>
          </div>
          <button
            class="modal-default-button bg-green-400 rounded-md py-2 w-full text-white"
            @click="saveList"
          >
            CONFIRM
          </button>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script>
export default {
  props: {
    show: Boolean,
  },

  data() {
    return {
      utilities: {
        name: "",
        value: 0
      },
    };
  },

  methods:{
    saveList(){
      let tasks = (localStorage.getItem("tasks")) ? JSON.parse(localStorage.getItem("tasks")) : []
      tasks.push(this.utilities) 
      localStorage.setItem("tasks", JSON.stringify(tasks)) // Salvando as informações no localstorage
      this.$emit('close')
      this.utilities.name = ""
      this.utilities.value = 0
      
    }
  }
};
</script>

<style>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: flex;
  align-items: center;
  height: inherit;
}

.modal-container {
  width: 90%;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 16px 0;
}

.modal-default-button {
  float: right;
}

.modal-enter-from {
  opacity: 0;
}

.modal-leave-to {
  opacity: 0;
}

.modal-enter-from .modal-container,
.modal-leave-to .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>
