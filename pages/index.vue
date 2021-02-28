<template>
  <section class="section">
    <div>
      <b-autocomplete
                rounded
                v-model="name"
                :data="filteredDataArray"
                placeholder="e.g. jQuery"
                icon="magnify"
                clearable
                @select="option => selected = option">
                <template #empty>No results found</template>
            </b-autocomplete>
    </div>
    <div class="columns is-mobile is-multiline">
      
      <card class="column" v-for="(land, index) in lands" :key="index" :title="land.name" :flag="land.flag">
        <NuxtLink :to="`land/${index}`">{{land.name}}</NuxtLink>
      </card>
<!--       
      <card
        title="Free"
        icon="github"
      >
        Open source on <a href="https://github.com/buefy/buefy">
          GitHub
        </a>
      </card>

      <card
        title="Responsive"
        icon="cellphone-link"
      >
        <b class="has-text-grey">
          Every
        </b> component is responsive
      </card>

      <card
        title="Modern"
        icon="alert-decagram"
      >
        Built with <a href="https://vuejs.org/">
          Vue.js
        </a> and <a href="http://bulma.io/">
          Bulma
        </a>
      </card>

      <card
        title="Lightweight"
        icon="arrange-bring-to-front"
      >
        No other internal dependency
      </card> -->
    </div>
  </section>
</template>

<script>
import Card from '~/components/Card'

import axios from "axios";
export default {
  name:'homepage',
  data(){
    return{
      lands:[],
      data:[],
      name:'',
      selected:null,
    }
  },
  computed: {
            filteredDataArray() {
                this.data = this.lands;
                return this.data.filter((option) => {
                    //console.log(option.name);
                    if(option.name.indexOf(this.name.toLowerCase()) >= 0){
                      console.log(option.name);
                      return option;
                    }
                    //console.log(this.name);
                    // console.log(option);
                    // return option
                    //     .toString()
                    //     .toLowerCase()
                    //     .indexOf(this.name.toLowerCase()) >= 0
                })
            }
        },
  mounted(){
    axios.get("https://restcountries.eu/rest/v2/all").then(response => this.lands = response.data);
    //this.getFlags();
    
  },

  components: {
    Card
  }
}
</script>
