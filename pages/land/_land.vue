<template>
    <div>
        <h1>{{land.name}} / {{land.nativeName}}</h1>
        <img :src="land.flag" />
        <ul>
            <li>Continent: {{land.region}}</li>
            <li>Capitale: {{land.capital}}</li>
            <li>Population : {{land.population}}  habitants</li>
        </ul>
        
    </div>
</template>
<script>
import axios from "axios";
export default {
  data(){
    return{
      land:[],
      nbr:null,
    }
  },
  mounted(){
    let nbr = this.$route.params.land;
    axios.get("https://restcountries.eu/rest/v2/all").then(response => this.land = response.data[nbr]);
    
    
  },
  methods: {
    
  }
}
</script>
</script>