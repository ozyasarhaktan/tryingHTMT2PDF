<template>
  <date-picker/>
</template>

<script lang="ts">
  import Vue from 'vue'
 import DatePicker from '@/components/DatePicker.vue';
//  import AlternativeDatePicker from '@/components/AlternativeDatePicker.vue';

  export default Vue.extend({
    name: 'Home',

    components: {
      DatePicker
    },
  })
</script>
