<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <IonButtons>
          <ion-back-button />
        </IonButtons>
        <ion-title>Geolocation Page</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true" class="ion-padding">
      <h2>Welcome To Geolocation Page</h2>
      <ion-item v-if="location">
        <ion-avatar slot="start">
          <img src="https://mobilemarketingwatch.com/wp-content/uploads/2016/09/location-icon.png">
        </ion-avatar>
        <ion-label>{{location.coords.latitude}} : {{location.coords.longitude}}</ion-label>
      </ion-item>
      <ion-button @click="getLocation">Get Current Location</ion-button>
    </ion-content>
  </ion-page>
</template>

<script>
  import {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonButtons,
    IonButton,
    IonBackButton,
  } from "@ionic/vue";
  import { defineComponent, ref } from "vue";
  import { Plugins } from "@capacitor/core";
  const { Geolocation } = Plugins;

  export default defineComponent({
    name: "Geolocation",
    components: {
      IonContent,
      IonHeader,
      IonPage,
      IonTitle,
      IonToolbar,
      IonButtons,
      IonBackButton,
      IonButton,
    },
    setup() {
      const location = ref(null);
      const getLocation = async () => {
        console.log("got getLocation event");
        location.value = await Geolocation.getCurrentPosition({
          enableHighAccuracy: true,
          timeout: 30000,
        });
        console.log("location", location.value.coords);
      };

      return {
        location,
        getLocation,
      };
    },
  });
</script>

<style scoped>
</style>
