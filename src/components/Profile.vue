<template>
  <label
    tabindex="0"
    class="rounded mb-6 overflow-hidden w-full flex flex-wrap md:flex-nowrap items-center justify-center cursor-pointer group shadow transition duration-300 ease-in-out hover:shadow-md transform hover:-translate-y-1 active:shadow-none focus:shadow-md focus:-translate-y-1"
  >
    <input
      type="checkbox"
      class="hidden"
    />
    <div
      class="bg-cover rounded h-40 md:h-48 w-full md:w-48" 
      :style="`background-image: url(${user.image})`"
    ></div>
    <div class="w-full flex flex-col">
      <div class="text-left md:ml-3">
        <div class="text-4xl">
          <div v-html="highlight(user.name)"></div>
        </div>
        <div class="md:absolute md:right-1 md:top-1 text-gray-500">
          <div v-html="highlight(user.mail)"></div>
        </div>
        <div class="text-gray-600 font-bold">
          <div v-html="highlight(user.description)"></div>
        </div>
        <div class="text-gray-600">
          <div v-html="highlight(user.data)"></div>
        </div>
        <div class="mt-2 py-4 px-6 h-full w-full flex items-center text-green-600 font-bold uppercase border-t-2">
          Mark as suitable
        </div>
      </div>
    </div>
  </label>
</template>

<script>
export default {
  name: 'profile',
  props: {
    user: {
      type: Object,
      required: true,
    },
    query: {
      type: String,
      required: false,
    },
  },
  methods: {
    highlight( content ) {
      if(!this.query) {
          return content;
      }
      return content.replace(new RegExp(this.query, "gi"), match => {
          return '<span class="bg-yellow-300">' + match + '</span>';
      });
    }
  }
}
</script>

<style scoped>
</style>
