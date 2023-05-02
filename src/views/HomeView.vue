<template>
  <!-- <date-picker/> -->
  <html-2-pdf-card/>
  <!-- <deneme/> -->
</template>

<script lang="ts">
  import Vue from 'vue'
 import DatePicker from '@/components/DatePicker.vue';
 import Html2PdfCard from '@/components/Html2PdfCard.vue';
//  import deneme from '@/components/deneme.vue';

  export default Vue.extend({
    name: 'Home',

    components: {
      DatePicker,
      Html2PdfCard,
      // deneme
    },
  })
</script>
