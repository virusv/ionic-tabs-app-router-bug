<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-buttons slot="start">
          <slot name="start">
            <ion-back-button />
          </slot>
        </ion-buttons>
        
        <ion-title>{{ title }}</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <h1 class="title-tab-page">{{ title }}</h1>
      <div class="btn-wrap-tab-page ion-padding" slot="fixed">
        <ion-button size="large" @click="next" expand="block">NEXT</ion-button>
      </div>
      
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonButton, IonButtons, IonBackButton } from '@ionic/vue';
import { useRoute, useRouter } from 'vue-router';
import { computed } from 'vue';

export default  {
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonButton, IonButtons, IonBackButton },
  setup() {
    const router = useRouter();
    const route = useRoute();

    const { a, n } = route.params;

    const title = computed(() => {
      return [a, n || '0'].join('.');
    });

    function next() {
      router.push({
        name: 'tab-page',
        params: {
          a: a,
          n: Number(n || 0) + 1,
        },
      });
    }

    return {
      title,
      next,
    };
  }
}
</script>

<style>
.title-tab-page {
  padding-top: 40px;
  padding-bottom: 20px;
  text-align: center;
}

.btn-wrap-tab-page {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  width: 100%;
}
</style>