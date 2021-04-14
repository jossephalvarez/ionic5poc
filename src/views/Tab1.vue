<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Home</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
<!--      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 1</ion-title>
        </ion-toolbar>
      </ion-header>
      <ExploreContainer name="Home Screen Tab" />

      <ion-button color="primary" expand="full">Cam</ion-button>
      <ion-button color="secondary" expand="full">Webview</ion-button>
      <ion-button color="tertiary" expand="full">Location</ion-button>
      <ion-button color="success" expand="full">Biometric</ion-button>-->
      <ion-item>
        <ion-avatar slot="start">
          <img src="https://gravatar.com/avatar/dba6bae8c566f9d4041fb9cd9ada7741?d=identicon&f=y">
        </ion-avatar>
        <ion-label>Item Avatar</ion-label>
      </ion-item>
      <ion-item>
            <ion-button color="secondary" expand="full">Webview</ion-button>
            <ion-button color="success" expand="full">Biometric</ion-button>
        </ion-item>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonItem, IonLabel, IonAvatar } from '@ionic/vue';
// import ExploreContainer from '@/components/ExploreContainer.vue';

export default  {
  name: 'Tab1',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonAvatar, IonItem, IonLabel }
}
</script>
