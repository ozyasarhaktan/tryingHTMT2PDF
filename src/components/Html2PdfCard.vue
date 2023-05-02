

<template>
      <div>
            <v-container >
                  <v-card ref="pdfContent" class="mx-auto align-items-center" min-width="800" max-width="800">

                        <v-container>
                              <v-row align="center" justify="center">
                                    <v-col>
                                          <v-text-field v-if="!gor" v-model="ad" class="ms-10" placeholder="Adınız"></v-text-field>
                                          <p v-if="gor">{{ ad }}</p>
                                    </v-col>
                                    <v-spacer></v-spacer>
                                    <v-col>
                                          <v-text-field class="me-10"  v-if="!gor" v-model="soyad" placeholder="Soyadınız"></v-text-field>
                                          <p v-if="gor">{{ soyad }}</p>
                                    </v-col>
                              </v-row>
                              <v-row>
                                    <v-col cols="12" lg="9" md="7" sm="6" xs="6">
                                          <div>
                                                <date-picker  v-if="!gor" v-on:baslangicDate="tarih" v-model="tarih"></date-picker>
                                                <p v-if="gor">{{ tarih }}</p>
                                          </div>
                                    </v-col>
                                    <v-spacer></v-spacer>
                                    <v-col cols="12" lg="3" md="5" sm="6" xs="6">
                                          <div>
                                                <v-text-field class="me-10" v-if="!gor" v-model="secKisiler" placeholder="Seçilen Kişiler"></v-text-field>
                                                <p v-if="gor">{{ secKisiler }}</p>
                                          </div>
                                    </v-col>
                              </v-row>
                              <v-row>
                                    <v-btn block white--text depressed color="error" v-html2pdf:pdfContent="'test.pdf'" class="my-5">PDF'e
                                          ÇEVİR</v-btn>
                              </v-row>
                        </v-container>

                  </v-card>
            </v-container>
      </div>
</template>

<script>
import DatePicker from '@/components/DatePicker.vue';
import VueHtml2pdf from '/node_modules/vue-html2pdf'
import jsPDF from '/node_modules/jspdf'

export default {
      directives: {
  html2pdf: VueHtml2pdf,
},
      data() {
            return {
                  ad: "",
                  soyad: "",
                  tarih: "",
                  secKisiler: "",
                  gor: false
            }
      },
//       mounted() {
//     this.$use(VueHtml2pdf)
//   },
      methods: {
            generatePdf() {
                  this.gor = true;
                  const pdf = new jsPDF();

                  pdf.html(this.$el.innerHTML, {
                        callback: () => {
                              pdf.save("test.pdf");
                        }
                  });
                  
            },

      },
      components: {
            DatePicker,
            VueHtml2pdf,

      },
}


</script>
