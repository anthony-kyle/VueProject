<template>
<div class="history">
  <Gallery />
  <div class="content">{{$store.state.car_info.history}}</div>
</div>
</template>

<script>
// @ is an alias to /src
import Gallery from '@/components/Gallery.vue';

export default {
  name: 'Home',
  components: {
    Gallery
  }
}
</script>
