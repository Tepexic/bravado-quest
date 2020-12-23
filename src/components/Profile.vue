<template>
  <label
    tabindex="0"
    class="rounded mb-6 overflow-hidden w-full
      flex flex-wrap md:flex-nowrap items-center justify-center
      cursor-pointer group
      transition duration-300 ease-in-out 
      hover:shadow-md transform hover:-translate-y-1
      focus:shadow-md focus:-translate-y-1"
    :class="selected ? 'border border-blue-600' : 'border-b'"
  >
    <input
      type="checkbox"
      class="hidden"
      v-model="selected"
      @change="$emit('change', selected)"
    />
    <div
      class="bg-cover rounded-l h-60 md:h-48 w-full md:w-48" 
      :style="`background-image: url(${user.image})`"
    ></div>
    <div class="w-full flex flex-col p-2 md:p-0">
      <div class="text-left">
        <div class="text-4xl md:ml-4">
          <div v-html="highlight(user.name)"></div>
        </div>
        <div class=" md:absolute md:right-1 md:top-1 text-gray-500 text-sm">
          <div v-html="highlight(user.mail)"></div>
        </div>
        <div class="text-gray-600 font-bold md:ml-4 pr-1">
          <div v-html="highlight(user.description)"></div>
        </div>
        <div class="text-gray-600 md:ml-4">
          <div v-html="highlight(user.data)"></div>
        </div>
        <div class="mt-2 pt-4 md:px-6 h-full w-full flex items-center text-green-600 text-xs font-bold uppercase border-t-2">
          {{ selected ? 'skip selection' : 'Mark as suitable'}}
        </div>
      </div>
    </div>
  </label>
</template>

<script>
export default {
  name: 'profile',
  data () {
    return {
      selected: false,
    }
  },
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
label {
  background: #FAFAFA;
}
</style>
