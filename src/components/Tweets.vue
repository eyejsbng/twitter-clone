<template>
	<ion-row class="wrapper">
		<ion-col size="2">
		<ion-avatar>
      <ion-img :src="tweet.img"></ion-img>
    </ion-avatar>
		</ion-col>
		<ion-col size="10">
			<ion-row class="tweet-info">
      <ion-col size="12">
        <span class="name">{{ tweet.username }}</span>
        <span class="handle">@{{ tweet.handle }}</span>
        <span class="handle">- {{ formatDate(tweet.date*1000) }}</span>
      </ion-col>
    </ion-row>
		<ion-row>
		<ion-col size="12">
      <div>{{ parseTweet(tweet.text) }}</div>
        <img class="preview-img" :src="tweet.attachment" v-if="tweet.attachment">
      </ion-col>
		</ion-row>
		<ion-row class="ion-justify-content-start">
      <ion-col>
        <ion-button fill="clear" color="medium" size="small">
          <ion-icon :icon="chatbubbleOutline" slot="start"></ion-icon>
          {{ tweet.response }}
        </ion-button>
      </ion-col>
      <ion-col>
        <ion-button  fill="clear" :color="tweet.retweet ? 'primary' : 'medium'" size="small">
          <ion-icon :icon="repeatOutline" slot="start"></ion-icon>
          {{ tweet.retweets }}
        </ion-button>
      </ion-col>
      <ion-col>
        <ion-button fill="clear" :color="tweet.liked ? 'primary' : 'medium'" size="small">
          <ion-icon :icon="heartOutline" slot="start"></ion-icon>
          {{ tweet.like }}
        </ion-button>
      </ion-col>
      <ion-col>
        <ion-button fill="clear" color="medium" size="small">
          <ion-icon name="share-outline" slot="start"></ion-icon>
        </ion-button>
      </ion-col>
    </ion-row>
		</ion-col>
	</ion-row>
</template>
<script>
	import {
		chatbubbleOutline,
		repeatOutline,
		heartOutline,
		shareOutline
	} from 'ionicons/icons';
	import moment from 'moment'
export default {
	props: ['tweet'],
	setup() {
		
		function parseTweet(val) {
		
			var tweet =	val.replace(/(<([^>]+)>)/gi, "");
			tweet.replace(/@\w+/g,"<span class='highlight'>$&</span>")
			tweet.replace(/#\w+/g,"Gago")
			return tweet
		}
		function formatDate(val) {
			return moment(val).format('MM/DD/YY')
		}
		return {
			parseTweet,
			formatDate,
			chatbubbleOutline,
			repeatOutline,
			heartOutline,
			shareOutline
		}
	},

	methods: {
		
	}
}
</script>
<style scoped>
.tweet-info {
    font-size: 0.9em;
}
 
.name {
    font-weight: 600;
}
 
.handle {
    padding-left: 4px;
    color: var(--ion-color-medium);
}
 
.wrapper {
    border-bottom: 1px solid var(--ion-color-light);
}
 
.highlight {
    color: var(--ion-color-primary);
}
 
.preview-img {
    border: 1px solid var(--ion-color-light);
    border-radius: 10px;
}
</style>