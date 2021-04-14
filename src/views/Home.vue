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
          <img src="https://avatars.githubusercontent.com/u/17790050?v=4">
        </ion-avatar>
        <ion-label>Josseph Alvarez</ion-label>
      </ion-item>
      <ion-item>
        <ion-button color="primary" expand="full" @click="openWebView()">Webview</ion-button>
        <ion-button color="tertiary" expand="full" @click="openBiometric()">Biometric</ion-button>
        <ion-button color="secondary" expand="full" @click="openModal()">Open Modal</ion-button>
        </ion-item>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonItem, IonLabel, IonAvatar, IonButton , modalController } from '@ionic/vue';
import Modal from '../components/Modal';
import { InAppBrowser } from '@ionic-native/in-app-browser';
import { AndroidFingerprintAuth } from '@ionic-native/android-fingerprint-auth';

import { defineComponent } from "vue";

export default defineComponent({
  name: 'Tab1',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonAvatar, IonItem, IonLabel, IonButton },
  setup() {
    const openModal = async (title) => {
      // Otherwise, make the call:
      try {
        const modal = await modalController
                .create({
                  component: Modal,
                  cssClass: 'my-custom-class',
                  componentProps: {
                    title: title || 'Modal'
                  },
                })
        return modal.present();
      } catch (e) {
        console.log("error", e);
      }
    };
    const openWebView =() =>{
      InAppBrowser.create('https://ionicframework.com/','_blank', 'location=yes');
    };
    const openBiometric = () => {
      AndroidFingerprintAuth.isAvailable()
              .then((result)=> {
                if(result.isAvailable){
                  // it is available
                  AndroidFingerprintAuth.encrypt({ clientId: 'myAppName', username: 'myUsername', password: 'myPassword' })
                      .then(result => {
                            if (result.withFingerprint) {
                              console.log('Successfully encrypted credentials.');
                              console.log('Encrypted credentials: ' + result.token);
                              openModal('Open Modal WITH FINGER PRINT');
                            } else if (result.withBackup) {
                              console.log('Successfully authenticated with backup password!');
                              openModal('Open Modal WITH BACKUP');
                            } else console.log('Didn\'t authenticate!');
                          })
                      .catch(error => {
                            if (error === AndroidFingerprintAuth.ERRORS.FINGERPRINT_CANCELLED) {
                              console.log('Fingerprint authentication cancelled');
                            } else console.error(error)
                          });

                } else {
                  // fingerprint auth isn't available
                }
              })
              .catch(error => console.error(error));
    }
    return {
      openModal,
      openWebView,
      openBiometric
    };
  },

})
</script>
