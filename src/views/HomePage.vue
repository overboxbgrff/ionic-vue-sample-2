<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Blank</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-button expand="block" class="ion-margin" @click="getData">Refresh</ion-button>

      <ion-list>
        <ion-item v-for="crypto in cryptoData" :key="crypto.id">
          <ion-label>
            <ion-grid>
              <ion-row>

                <ion-col size="4">
                  <p>Rank</p>
                  {{ crypto.rank }}
                </ion-col>

                <ion-col size="4">
                  {{ crypto.name }}<br />
                  {{ crypto.symbol }}
                </ion-col>

                <ion-col size="4">
                  <p>USD</p>
                  {{ crypto.price_usd }}
                </ion-col>

              </ion-row>
            </ion-grid>
          </ion-label>
        </ion-item>
      </ion-list>

    </ion-content>
  </ion-page>
</template>

<script>
import {
  IonContent,IonHeader,IonPage,IonTitle,IonToolbar,IonButton,IonList,IonItem,IonLabel,IonGrid,IonRow,IonCol,} from "@ionic/vue";
import axios from "axios";

export default {
  name: "HomePage",
  components: {
    IonContent,IonHeader,IonPage,IonTitle,IonToolbar,IonButton,IonList,IonItem,IonLabel,IonGrid,IonRow,IonCol,
  },
  data() {
    return {
      cryptoData: [],
    };
  },
  methods: {
    async getData() {
      try {
        const response = await axios.get(
          "https://api.coinlore.net/api/tickers/"
        );

        this.cryptoData = response.data.data.slice(0,7);
      } catch (error) {
        console.error("Error fetching data: ", error);
      }
    },
  },
  beforeMount(){
    this.getData();
  },
};
</script>