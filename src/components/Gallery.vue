<template>
<div class="gallery">
  <Card>
    <img src="@/assets/gto.jpg" />
    <h2>{{$store.state.car_info.brand}} {{$store.state.car_info.model}}</h2>
  </Card>
</div>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>

</style>
