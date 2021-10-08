<script lang="ts">
import { defineComponent } from 'vue';
// Uncomment import and local "components" registration if library is not registered globally.
// import { GravityComponentsSample } from '@/entry.esm';

export default defineComponent({
  name: 'ServeDev',
  // components: {
  //  GravityComponentsSample,
  // }
});
</script>

<template>
  <div id="app">
    <gravity-components-sample />
  </div>
</template>
