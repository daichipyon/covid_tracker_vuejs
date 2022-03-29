<template>
<main v-if="!loading">
  <div class="text-center.text-3xl">Now loading</div>
</main>
<main v-else>
  <Datatitle/>
  <Datablock :stats="stats"></Datablock>
  <CountrySelect :countries='countries' @get-country="update_stats"/>
</main>
</template>

<script>
import { reactive, computed, onMounted, ref, toRefs  } from "vue";
import Datatitle from '@/components/Datatitle.vue'
import Datablock from '@/components/Datablock.vue'
import CountrySelect from '../components/CountrySelect.vue'

export default {
  name: 'HomeView',
  components: {
    Datatitle,
    Datablock,
    CountrySelect,
  },

  setup(){
    const loading = ref(false)
    const selected_country_id = ref(0)
    const countries = reactive({})

    const fetch_info = async () => {

      const res = await fetch('https://api.covid19api.com/summary',{
        mode:'cors'
      })
      const data = await res.json()
      return data
    }

     onMounted(async () => {
      try{
        const data = await fetch_info()

        const tmp_countries = await data.Countries
        const global = await data.Global
        global['ID'] = "Global_ID"
        countries['Global_ID'] = global


        tmp_countries.forEach((country)=>{
          const country_id = country.ID
          countries[country_id] = country
        })


        selected_country_id.value = 'Global_ID'
        loading.value = true
        
      }catch(e){
        console.log(e)
      }
    })

    const stats = computed(()=> {
      return countries[selected_country_id.value]
    })
    
    const update_stats = (country_id) => {
      console.log(country_id)
      selected_country_id.value = country_id
    }
    return {stats, loading,countries,selected_country_id,update_stats}
  }

}
</script>
<style>
body { 
  background-color: rgb(238, 242, 255); 
} 
</style>
