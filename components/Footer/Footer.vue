<template>
  <div class="h-20 bg-gray-100 shadow-md p-4">
       <nuxt-link  :to="link">
           <button class="w-full rounded-lg text-white bg-blue-400 h-full">{{text}}</button>
        </nuxt-link>
  </div>
</template>

<script>
export default {
    props: {
        text: {
            type: String,
            default: 'Button'
        },
        link: {
            type: String,
            default: '/'
        }
    },
}
</script>

<style>

</style>