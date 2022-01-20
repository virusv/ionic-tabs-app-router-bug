<template>
  <ion-page>
    <ion-tabs :class="{
      [className]: true,
    }">
      <ion-router-outlet></ion-router-outlet>
      <ion-tab-bar slot="bottom">
        <ion-tab-button tab="tabA" href="/tabs/a">
          <ion-icon :icon="triangle" />
          <ion-label>Tab 1</ion-label>
        </ion-tab-button>
          
        <ion-tab-button tab="tabB" href="/tabs/b">
          <ion-icon :icon="ellipse" />
          <ion-label>Tab 2</ion-label>
        </ion-tab-button>
        
        <ion-tab-button tab="tabC" href="/tabs/c">
          <ion-icon :icon="square" />
          <ion-label>Tab 3</ion-label>
        </ion-tab-button>
      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script lang="ts">
import { IonTabBar, IonTabButton, IonTabs, IonLabel, IonIcon, IonPage, IonRouterOutlet } from '@ionic/vue';
import { ellipse, square, triangle } from 'ionicons/icons';
import { ref, onBeforeUnmount } from 'vue';
import { useRouter } from 'vue-router';

export default {
  components: { IonLabel, IonTabs, IonTabBar, IonTabButton, IonIcon, IonPage, IonRouterOutlet },
  setup() {
    const router = useRouter();
    const className = ref('class-name-0');

    onBeforeUnmount(router.beforeEach((to, from, next) => {
      className.value = 'class-name-' + Math.round(Math.random() * 10000);
      next();
    }));

    return {
      ellipse, 
      square, 
      triangle,
      className,
    }
  }
}
</script>