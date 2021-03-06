<template>
	<ion-page>
		<ion-header slot="header" v-if="showHeader == true">
			<ion-toolbar>
				<ion-buttons slot="start">
					<ion-button>
						<ion-icon slot="icon-only" name="menu-outline"></ion-icon>
					</ion-button>
				</ion-buttons>
				<ion-title>
					<ion-icon :icon="logoTwitter" color="primary" size="large" />
				</ion-title>
				<ion-buttons slot="end">
					<ion-button>
						<ion-icon slot="icon-only" :icon="pulseOutline" color="primary"></ion-icon>
					</ion-button>
				</ion-buttons>
			</ion-toolbar>
		</ion-header>

		<ion-content :fullscreen="true" :scroll-events="true">
				<ion-segment v-model="segment" mode="md">
				<ion-segment-button value="home">
					<ion-label>Home</ion-label>
				</ion-segment-button>
				<ion-segment-button value="content">
					<ion-label>cr-content-suggest</ion-label>
				</ion-segment-button>
			</ion-segment>
			<ion-slides v-if="segment == 'home'" :options="opts">
			<ion-slide v-for="tweet in tweets" :key="tweet.id">
				<ion-avatar>
					<img :src="tweet.img">
				</ion-avatar>
			</ion-slide>
		</ion-slides>
			<tweet v-for="tweet in tweets" :tweet="tweet" :key="tweet.username"/>
		</ion-content>
	</ion-page>
</template>

<script>
	import {
		IonIcon,
		IonButton,
		IonButtons,
		IonSegment,
		IonSegmentButton,
		IonLabel,
		IonPage,
		IonHeader,
		IonToolbar,
		IonTitle,
		IonContent
	} from '@ionic/vue';

	import {
		logoTwitter,
		pulseOutline
	} from 'ionicons/icons';
	import axios from 'axios'
	import Tweet from '../components/Tweets.vue'
	
	export default {
		name: 'Tab1',
		components: {
			IonButton,
			IonIcon,
			IonButtons,
			IonSegment,
			IonSegmentButton,
			IonLabel,
			IonHeader,
			IonToolbar,
			IonTitle,
			IonContent,
			IonPage,
			Tweet
		},
		setup() {

			return {
				logoTwitter,
				pulseOutline
			}
		},
		data() {
			return {
				tweets: [],
				segment: 'home',
				opts: {
					slidesPerView: 4.5,
					spaceBetween: 10,
					slideOffsetBefore: 0
				},
				showHeader: true,
				lastScrollPosition: 0,
			}
		},
		methods: {
			onScroll() {
				const currentScrollPosition = window.pageYOffset || document.documentElement.scrollTop
    // Because of momentum scrolling on mobiles, we shouldn't continue if it is less than zero
					if (currentScrollPosition < 0) {
						return
					}
					if (Math.abs(currentScrollPosition - this.lastScrollPosition) < 60) {
    return
  }
					// Here we determine whether we need to show or hide the navbar
					this.showNavbar = currentScrollPosition < this.lastScrollPosition
					// Set the current scroll position as the last scroll position
					this.lastScrollPosition = currentScrollPosition
			}
		},
		mounted() {
			window.addEventListener('scroll', this.onScroll)
		},
		beforeUnmount() {
			window.removeEventListener('scroll', this.onScroll)
		},
		created() {
			axios.get('https://devdactic.fra1.digitaloceanspaces.com/twitter-ui/tweets.json').then((data) => {
				this.tweets = data.data.tweets
			})
		},
	}
</script>
<style scoped>
ion-toolbar {
    --border-style: none;
}
 
ion-header {
    background: #fff;
}
 
ion-slides {
    padding-top: 8px;
    padding-bottom: 8px;
    border-bottom: 1px solid var(--ion-color-light);
}
 
ion-segment {
    z-index: 10;
    background: #fff;
}
 
ion-segment-button {
    text-transform: none;
}
 
ion-avatar {
    border: 2px solid var(--ion-color-primary);
    padding: 2px;
}
</style>