<template>
    <ion-header>
        <ion-toolbar>
            <ion-title>{{ title }}</ion-title>
        </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
        {{ content }}
    </ion-content>
</template>

<script>
    import { IonContent, IonHeader, IonTitle, IonToolbar } from '@ionic/vue';
    import { defineComponent } from 'vue';
    import { InAppBrowser } from '@ionic-native/in-app-browser';

    export default defineComponent({
        name: 'Modal',
        props: {
            title: { type: String, default: 'Super Modal' },
        },
        data() {
            return {
                content: 'Content Modal here!!',
            }
        },
        ionViewWillEnter() {
            console.log('Home page did leave');
            InAppBrowser.create('https://ionicframework.com/docs/vue/lifecycle', '_blank');
        },
        components: { IonContent, IonHeader, IonTitle, IonToolbar }
    });
</script>
