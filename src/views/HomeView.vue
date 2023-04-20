<template>
  <date-picker/>
</template>

<script lang="ts">
  import Vue from 'vue'
 import DatePicker from '@/components/DatePicker.vue';

  export default Vue.extend({
    name: 'Home',

    components: {
      DatePicker
    },
  })
</script>
