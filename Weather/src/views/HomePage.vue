<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Weather Jakarta</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Weather in Jakarata</ion-title>
        </ion-toolbar>
      </ion-header>


<ion-content :fullscreen="true">
  <ion-header collapse="condense">
    <ion-toolbar>
      <ion-title size="large">Weather in Jakarta</ion-title>
    </ion-toolbar>
  </ion-header>

  <div class="card-container">
    <ion-card v-for="(time, index) in weatherTimes" :key="index">
      <ion-card-header>
        <ion-card-title>{{ time }}</ion-card-title>
      </ion-card-header>
      <ion-card-content>
        Temperature: {{ weatherTemps[index] }} °C
      </ion-card-content>
    </ion-card>
  </div>
</ion-content>


    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonList, IonItem, IonLabel } from '@ionic/vue';

interface WeatherData {
  hourly: {
    time: string[];
    temperature_2m: number[];
  };
}

const weatherTimes = ref<string[]>([]);
const weatherTemps = ref<number[]>([]);

const fetchWeather = async () => {
  try {
    const res = await fetch('https://api.open-meteo.com/v1/forecast?latitude=-6.2&longitude=106.8&hourly=temperature_2m');
    const data: WeatherData = await res.json();

    weatherTimes.value = data.hourly.time;
    weatherTemps.value = data.hourly.temperature_2m;
  } catch (error) {
    console.error('Failed to fetch weather:', error);
  }
};

onMounted(() => {
  fetchWeather();
});
</script>


