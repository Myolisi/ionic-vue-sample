<template>
  <div class="home">
    <ion-header>
      <ion-toolbar>
        <ion-title>Gigle-dee</ion-title>
        <ion-icon slot="end" name="hammer"></ion-icon>
      </ion-toolbar>
    </ion-header>
    <ion-grid fixed>
      <ion-row></ion-row>
      <ion-row class="ion-padding-bottom">
        <ion-col size="12">Just hit the button and have fun</ion-col>
      </ion-row>
      <ion-row>
        <ion-col size="12">
          <ion-button expand="block" v-on:click="generateJoke()" fill="solid">Get Joke</ion-button>
        </ion-col>
      </ion-row>
    </ion-grid>
    <!-- Card results -->
    <ion-progress-bar v-if="doSearch" type="indeterminate"></ion-progress-bar>
    <ion-card v-if="jokes && !doSearch">
      <ion-card-header>
        <ion-card-title>{{jokes['setup']}}</ion-card-title>
      </ion-card-header>
      <ion-card-content>{{jokes['punchline']}}</ion-card-content>
    </ion-card>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "home",
  data() {
    return {
      doSearch: false,
      jokes: ""
    };
  },
  methods: {
    generateJoke() {
      this.doSearch = true;
      axios
        .get("https://official-joke-api.appspot.com/random_joke")
        .then(res => {
          this.doSearch = false;
          this.jokes = res.data;
          console.log(this.jokes);
        })
        .catch(err => {
          console.log(err);
        });
    }
  },
  mounted() {}
};
</script>
