<template>

  <div :v-if="countries" >
    
      <div class="container">

        <div class="row">
          <div class="col-5" style="max-height: 90vh; overflow: scroll">
            <div class="list-group">
              <router-link v-for="(country) in countries" :key="country.name" class="list-group-item list-group-item-action d-flex flex-column justify-content-center align-items-center" :to="`/list/${country.alpha3Code}`">
                <img :src="`https://flagpedia.net/data/flags/icon/72x54/${country.alpha2Code.toLowerCase()}.png`"  />
                <p>{{country.name.common}}</p>
              </router-link>

            </div>
          </div>
          <div class="col-7">
            <router-view />
          </div>
        </div>
    </div>
  </div>
</template>
  
<script>
export default {
  data(){
    return {
      countries: []
    }
  },
  async created(){
    const response = await fetch('https://ih-countries-api.herokuapp.com/countries')
    this.countries = await response.json()
  }
}
  
</script>