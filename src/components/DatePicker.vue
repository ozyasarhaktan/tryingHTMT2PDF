<template>
  <v-row>
    <v-col cols="12" sm="6" md="4">
      <v-menu v-model="menu" :close-on-content-click="false" :return-value.sync="deneme" transition="scale-transition"
        offset-y min-width="290px">
        <template v-slot:activator="{ on, attrs }">
          <v-text-field v-model="deneme" label="Tarih Aralığı seç" prepend-icon="mdi-calendar" readonly v-bind="attrs"
            v-on="on"></v-text-field>
        </template>

        <v-container cols="12" min-width="600px" max-width="600px" min-height="400px" max-height="400px">
          <div class="d-flex flex-column float-left me-2">
            <v-btn @click="today" depressed block class="mb-2">
              Bugün
            </v-btn>
            <v-btn @click="yesterday" depressed block class="mb-2">
              Dün
            </v-btn>
            <v-btn @click="last7Days" depressed block class="mb-2">
              Son 7 Gün
            </v-btn>
            <v-btn @click="last30Days" depressed block class="mb-2">
              Son 30 Gün
            </v-btn>
            <v-btn @click="thisMonth" depressed block>
              Bu Ay
            </v-btn>

            <div class="mt-2">
              <v-btn @click="tamamla" color="success me-1">Başvur</v-btn>
              <v-btn @click="iptal" dark color="red">İptal</v-btn>
            </div>
          </div>

          <div class="d-flex flex-row float-right">
            <div>
              <v-text-field readonly solo outlined label="Başlangıç Tarihi" v-model="dateFormatted"
                prepend-inner-icon="mdi-calendar"></v-text-field>
              <v-date-picker v-model="baslangicDate" range no-title scrollable></v-date-picker>
            </div>
          </div>

        </v-container>

      </v-menu>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data: () => ({
    baslangicDate: [new Date().toISOString().substr(0, 10), new Date().toISOString().substr(0, 10)],
    tarih: new Date(),
    deneme: "",
    menu: false

  }),
  methods: {
    tamamla() {
      if (this.baslangicDate.length != 2) {
        alert("İlk tarih veya ikinci tarih boş olamaz")
      }
      else {
        alert("islem tamam")
        setTimeout(() => {
          this.menu = false;
        }, 500);
      }
      setTimeout(() => {
        this.deneme = this.dateFormatted.toString();
      }, 501);

    },
    iptal() {
      this.baslangicDate = null;
    },
    today() {
      const [yil, ay, gun] = [this.tarih.getFullYear(), this.tarih.getMonth(), this.tarih.getDate()];
      this.baslangicDate = [`${yil}-${ay.toString().padStart(2, '0')}-${gun.toString().padStart(2, '0')}`, `${yil}-${ay.toString().padStart(2, '0')}-${gun.toString().padStart(2, '0')}`];
    },
    yesterday() {
      const [yil, ay, gun] = [this.tarih.getFullYear(), this.tarih.getMonth(), this.tarih.getDate()];
      this.baslangicDate = [`${yil}-${ay.toString().padStart(2, '0')}-${(new Date().getDate() - 1).toString().padStart(2, '0')}`, `${yil}-${ay.toString().padStart(2, '0')}-${gun.toString().padStart(2, '0')}`];
    },
    last7Days() {
      const [yil, ay, gun] = [this.tarih.getFullYear(), this.tarih.getMonth(), this.tarih.getDate()];
      this.baslangicDate = [`${yil}-${(new Date().getMonth()).toString().padStart(2, '0')}-${(new Date().getDate() - 7).toString().padStart(2, '0')}`, `${yil}-${ay.toString().padStart(2, '0')}-${gun.toString().padStart(2, '0')}`];
    },
    last30Days() {
      const [yil, ay, gun] = [this.tarih.getFullYear(), this.tarih.getMonth(), this.tarih.getDate()];
      this.baslangicDate = [`${yil}-${(new Date().getMonth() - 1).toString().padStart(2, '0')}-${new Date().getDate(new Date().setDate(this.tarih.getDate() - 30)).toString().padStart(2, '0')}`, `${yil}-${ay.toString().padStart(2, '0')}-${gun.toString().padStart(2, '0')}`];
    },
    thisMonth() {
      const [yil, ay, gun] = [this.tarih.getFullYear(), this.tarih.getMonth(), this.tarih.getDate()];
      this.baslangicDate = [`${yil}-${ay.toString().padStart(2, '0')}-${'1'.padStart(2, '0')}`, `${yil}-${(ay).toString().padStart(2, '0')}-${new Date(new Date().getFullYear(), ay, 0).getDate()}`];
    }
  },

  computed: {
    dateFormatted() {
      if (this.baslangicDate) {
        const [yil, ay, gun] = this.baslangicDate[0].split('-');
        if (this.baslangicDate.length == 2) {
          const [yil2, ay2, gun2] = this.baslangicDate[1].split('-');

          if (this.baslangicDate[1] < this.baslangicDate[0]) {
            alert("Seçilen ilk tarih ikinci tarihten küçük olamaz!");
            this.baslangicDate = null;
          }
          else {
            return `${gun}.${ay}.${yil} - ${gun2}.${ay2}.${yil2}`;
          }
        }
      }
    },


  }
};
</script>
