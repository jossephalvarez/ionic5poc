<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Home</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-item>
        <ion-avatar slot="start">
          <img src="https://gravatar.com/avatar/dba6bae8c566f9d4041fb9cd9ada7741?d=identicon&f=y">
        </ion-avatar>
        <ion-label>Item Avatar</ion-label>
      </ion-item>
      <ion-item>
        <ion-button color="secondary" expand="full" @click="openWebView()">Webview</ion-button>
        <ion-button color="success" expand="full">Biometric</ion-button>
        <ion-button color="secondary" expand="full" @click="openModal()">Open Modal</ion-button>
        </ion-item>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonItem, IonLabel, IonAvatar, IonButton , modalController } from '@ionic/vue';
import Modal from '../components/Modal';
import { InAppBrowser } from '@ionic-native/in-app-browser';

import { defineComponent } from "vue";

export default defineComponent({
  name: 'Tab1',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonAvatar, IonItem, IonLabel, IonButton },
  setup() {
    const openModal = async () => {
      // Otherwise, make the call:
      try {
        const modal = await modalController
                .create({
                  component: Modal,
                  cssClass: 'my-custom-class',
                  componentProps: {
                    title: 'Modal'
                  },
                })
        return modal.present();
      } catch (e) {
        console.log("error", e);
      }
    };
    const openWebView =() =>{
      InAppBrowser.create('https://ionicframework.com/','_blank', 'location=yes');
    }
    return {
      openModal,
      openWebView
    };
  },

})
</script>
