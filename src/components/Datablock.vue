<template>
<div class="grid md:grid-cols-2 gap-4 auto-cols-min">
    <div class="bg-indigo-200 shadow-md">
      <div class="text-center text-2xl p-3">New desease</div>
      <div class="text-center text-3xl pb-3"> <strong>{{stats.NewConfirmed}}</strong> cases</div>
    </div>
    <div class="bg-indigo-200 shadow-md">
      <div class="text-center text-2xl p-3">New deaths</div>
      <div class="text-center text-3xl pb-3"> <strong>{{stats.NewDeaths}}</strong> cases</div>
    </div>
</div>

</template>


<script>
export default {
  name: 'Datablock',
  props:['stats']
}
</script>