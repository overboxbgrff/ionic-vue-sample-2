<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Kripto</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Kripto</ion-title>
        </ion-toolbar>
      </ion-header>

      <div id="container">
        <ion-button expand="block" class="ion-margin" @click="getData">Refresh</ion-button>
        
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButton, IonList,
  IonItem, IonLabel, IonGrid, IonRow, IonCol, } from '@ionic/vue';
import axios from 'axios';

export default{
  name: "HomePage",
  components: {IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButton, IonList,
      IonItem, IonLabel, IonGrid, IonRow, IonCol,
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

        this.cryptoData = response.data.data.filter((crypto) =>
          ["BTC", "ETH", "USDT", "BNB"].includes(crypto.symbol)
        );
      } catch (error) {
        console.error("Error fetching data: ", error);
      }
  },
};

</script>

<style scoped>
#container {
  text-align: center;
  
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  
  color: #8c8c8c;
  
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>
