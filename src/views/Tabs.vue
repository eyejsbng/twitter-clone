<template>
  <ion-page>
    <ion-tabs>
      <ion-tab-bar slot="bottom">
        <ion-tab-button tab="tab1" href="/tabs/tab1">
          <ion-icon :icon="homeOutline" />      
        </ion-tab-button>
          
        <ion-tab-button tab="tab2" href="/tabs/tab2">
          <ion-icon :icon="searchOutline" />      
        </ion-tab-button>

        <ion-tab-button tab="tab3" href="/tabs/tab3">
				<ion-badge color="primary">11</ion-badge>
          <ion-icon :icon="notificationsOutline" />       
        </ion-tab-button>

				<ion-tab-button tab="tab4" href="/tabs/tab4">
          <ion-icon :icon="mailOutline" />      
        </ion-tab-button>
				
      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script>
import { IonTabBar, IonTabButton, IonTabs, IonIcon, IonPage, IonBadge } from '@ionic/vue';
import { homeOutline, searchOutline, notificationsOutline, mailOutline } from 'ionicons/icons';

export default {
  name: 'Tabs',
  components: { IonTabs, IonTabBar, IonTabButton, IonIcon, IonPage,IonBadge },
  setup() {
    return {
      homeOutline, 
      searchOutline, 
      notificationsOutline,
			mailOutline
    }
  }
}
</script>