<template>
  <ion-page>
    <ion-content :fullscreen="true" color="light">
      <div>Click this ellipsis and click the "test" option</div>
      <ion-button @click="setOpen(true, $event)" shape="round" fill="clear" color="dark" size="small">
        <ion-icon :icon="ellipsisVertical"></ion-icon>
      </ion-button>
      <ion-popover :is-open="isOpen" :event="locationEvent" :dismissOnSelect="true" @didDismiss="setOpen(false)">
        <ion-item class="context-item" lines="full" @click="openModal">Test</ion-item>
      </ion-popover>
    </ion-content>
  </ion-page>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import { IonButton, IonPopover, IonIcon, IonPage, IonContent, modalController, IonItem } from '@ionic/vue';
import { ellipsisVertical } from 'ionicons/icons';
import ModalVue from './Modal.vue';

const isOpen = ref(false);
const locationEvent = ref<Event>();

function setOpen(state: boolean, event?: Event) {
  locationEvent.value = event;
  isOpen.value = state;
}

const openModal = async () => {
  const modal = await modalController
    .create({
      component: ModalVue
    })
  modal.present();
  await modal.onDidDismiss();
}
</script>