<template>
      <v-row>
        <v-col cols="12" sm="6" md="4">
          <v-menu
            ref="menu"
            v-model="menu"
            :close-on-content-click="false"
            :return-value.sync="date"
            transition="scale-transition"
            offset-y
            min-width="290px"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-text-field
                :value.sync="dates"
                label="Picker in menu"
                prepend-icon="mdi-calendar"
                readonly
                v-bind="attrs"
                v-on="on"
              ></v-text-field>
            </template>
    
            <v-container cols="12" min-width="600px" max-width="600px" min-height="400px" max-height="400px" >
              <div class="d-flex flex-column float-left ">
                <v-btn depressed block class="mb-2">
                Bugün
              </v-btn>
              <v-btn depressed block class="mb-2">
                Dün
              </v-btn>
              <v-btn depressed block class="mb-2">
                Son 7 Gün
              </v-btn>
              <v-btn depressed block class="mb-2">
                Son 30 Gün
              </v-btn>
              <v-btn depressed block>
                Bu Ay
              </v-btn>
    
              <div class="mt-2">
                <v-btn color="success me-1">Başvur</v-btn>
                <v-btn dark color="red">İptal</v-btn>
              </div>
              </div>
    
              <div class="d-flex flex-row float-right">
                <div>
                  <v-text-field
                  readonly
                  solo
                  outlined
                  label="Başlangıç Tarihi"
                  v-model="dateFormattedStart"
                  prepend-inner-icon="mdi-calendar"
                  v-bind="attrs"
                  @blur="date = parseDate(dateFormatted)"
                  v-on="on"
                ></v-text-field>
                <v-date-picker v-model="baslangincDate"  no-title scrollable></v-date-picker>
                </div>
                <div>
                  <v-text-field 
                  readonly
                  solo 
                  outlined
                  label="Bitiş Tarihi"
                  v-model="dateFormattedEnd"
                  prepend-inner-icon="mdi-calendar"
                  v-bind="attrs"
                  @blur="date = parseDate(dateFormatted)"
                  v-on="on"
                ></v-text-field>
                  <v-date-picker v-model="bitisDate"  no-title scrollable></v-date-picker>
                </div>
              </div>
                    
            </v-container>
    
          </v-menu>
        </v-col>
      </v-row>
    </template>
    
    <script>
    export default {
      props: {
        value: {
          type: Array,
          required: true,
        },
      },
      data: () => ({
        date: new Date().toISOString().substr(0, 10),
        baslangincDate: null,
        bitisDate: null,
      }),
    
      methods: {
    
      },
    
      computed:{
        dateFormattedStart(){
          if (this.baslangincDate && this.bitisDate) {
              const options = {
                  year: 'numeric',
                  month: 'long',
                  day: 'numeric'
              };
              return this.baslangincDate;
          } else{
            return '';
          }
        },
        dateFormattedEnd(){
          if (this.bitisDate) {
              const options = {
                  year: 'numeric',
                  month: 'long',
                  day: 'numeric'
              };
              return this.bitisDate;
          } else{
            return '';
          }
        },
    
    
      }
    };
    </script>
    