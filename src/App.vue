<template>
  <div id="app" class="h-screen w-full bg-gray-200 flex justify-center items-align">
    <div class="bg-white w-full lg:max-w-2xl py-10 px-8 mx-auto my-2 overflow-scroll">
      
     <div class="pt-2 relative mx-auto text-gray-600">
        <input 
          id="search"
          class="w-full h-12 rounded mb-8 focus:outline-none focus:shadow-outline text-xl px-10 shadow-lg"
          type="search" 
          placeholder="Search for Star Wars characters..."
          v-model="query"
        >
        <button type="submit" class="absolute left-3 top-6">
          <svg class="text-gray-600 h-4 w-4 fill-current" xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0px" y="0px"
            viewBox="0 0 56.966 56.966" style="enable-background:new 0 0 56.966 56.966;" xml:space="preserve"
            width="512px" height="512px">
            <path
              d="M55.146,51.887L41.588,37.786c3.486-4.144,5.396-9.358,5.396-14.786c0-12.682-10.318-23-23-23s-23,10.318-23,23  s10.318,23,23,23c4.761,0,9.298-1.436,13.177-4.162l13.661,14.208c0.571,0.593,1.339,0.92,2.162,0.92  c0.779,0,1.518-0.297,2.079-0.837C56.255,54.982,56.293,53.08,55.146,51.887z M23.984,6c9.374,0,17,7.626,17,17s-7.626,17-17,17  s-17-7.626-17-17S14.61,6,23.984,6z" />
          </svg>
        </button>
      </div>

      <div class="p-2 overflow-hidden">
        <profile v-for="u in searchResults" :key="u.name" :user="u" :query="query"/>
      </div>
    </div>
  </div>
</template>

<script>
var debounce = require('lodash.debounce');
import axios from 'axios';
import Profile from '@/components/Profile';

export default {
  name: 'App',
  data() {
    return {
      users: [],
      searchWord: '',
    }
  },
  computed: {
    query: {
      get: function () {
        return this.searchWord;
      },
      set: debounce( function (newValue) {
        this.searchWord = newValue.toLowerCase()
      }, 500)
    },
    searchResults() {
      return this.users.filter( user => 
          user.name.toLowerCase().includes( this.query ) ||
          user.mail.toLowerCase().includes( this.query ) ||
          user.description.toLowerCase().includes( this.query ) ||
          user.data.toLowerCase().includes( this.query )
        )
    }
  },
  components: {
    Profile
  },
  methods: {
    async fetchUsers () {
      try {
        const res = await axios.get('https://akabab.github.io/starwars-api/api/all.json');
        console.log(res)
        if( res.status === 200 ) {
          res.data.forEach( u => {
            this.users.push({
              name: u.name,
              mail: u.name.split(' ')[0].toLowerCase() + '@sw.com',
              description: `Is a ${u.species} born on ${u.homeworld ? u.homeworld : 'an unknown planet'}. 
                Has ${u.hairColor ? u.hairColor : 'no'} hair, ${u.eyeColor} eyes and ${u.skinColor ? u.skinColor : 'unknown'} skin`,
              data: `Weights ${u.mass ? u.mass : 'X'}kg and is ${u.height ? u.height : 'X'}m tall`,
              image: u.image
            })
          })
        }
      } catch (err) {
        console.log(err)
      }
    }
  },
  mounted() {
    this.fetchUsers()
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#search {
  background: #FAFAFA;
  box-shadow: 0px 0px 2px rgba(0, 0, 0, 0.12), 0px 2px 2px rgba(0, 0, 0, 0.24);
  border-radius: 2px;
}

</style>
