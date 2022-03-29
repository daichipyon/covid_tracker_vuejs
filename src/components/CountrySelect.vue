<template>
<div class="inline-block relative w-64 pt-10">
    <select class="block appearance-none w-full bg-white border border-gray-400 hover:border-gray-500 px-4 py-2 pr-8 rounded shadow leading-tight focus:outline-none focus:shadow-outline" v-model='selected_update' @change="change_country">
      <option value="0">Select Country</option>
      <option v-for="country in countries" :value="country.ID" :key="country.ID">
          {{country.Country}}
      </option>
    </select>
</div>
  <button
    class="ml-5 bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600"
    @click="reset_country">
    Reset
  </button>

</template>


<script>
  import { ref} from "vue";

  export default {
    name: 'CountrySelect',
    props: ['countries'],
    emits:['reset_country'],
    setup ({countries},context) {
        const selected_update = ref(0)
        const change_country = () => {
            context.emit('get-country', selected_update.value)
        }
        const reset_country = () => {
            selected_update.value = 0
            context.emit('get-country','Global_ID')
        }

      return {change_country,selected_update,reset_country};
    }
  }
</script>