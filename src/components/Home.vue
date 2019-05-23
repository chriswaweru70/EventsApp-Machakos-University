<template>
  <v-container>
    <v-layout row wrap>
      <v-flex xs12 sm6 class="text-xs-center text-sm-right">
        <v-btn large router to="/meetups" class="secondary radius">Explore Events</v-btn>
      </v-flex>
      <v-flex xs12 sm6 class="text-xs-center text-sm-left">
        <v-btn large router to="/meetup/new" class="secondary radius">Organize Event</v-btn>
      </v-flex>
    </v-layout>
    <v-layout>
      <v-flex xs12 class="text-xs-center">
        <v-progress-circular
          indeterminate
          class="primary--text"
          :width="7"
          :size="70"
          v-if="loading"></v-progress-circular>
      </v-flex>
    </v-layout>
    <v-layout row wrap class="mt-2" v-if="!loading">
      <v-flex xs12>
        <v-carousel style="cursor: pointer;">
          <v-carousel-item
            v-for="meetup in meetups"
            :src="meetup.imageUrl"
            :key="meetup.id"
            @click="onLoadMeetup(meetup.id)">
            <div class="title">
              {{ meetup.title }}
            </div>
          </v-carousel-item>
        </v-carousel>
      </v-flex>
    </v-layout>
    <v-layout row wrap  class="mt-2">
      <v-flex xs12 class="text-xs-center">
       <p class="bolder2">Join our awesome Events!</p>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    computed: {
      meetups () {
        return this.$store.getters.featuredMeetups
      },
      loading () {
        return this.$store.getters.loading
      }
    },
    methods: {
      onLoadMeetup (id) {
        this.$router.push('/meetups/' + id)
      }
    }
  }
</script>

<style scoped>
 .title {
   position: static;
   text-align: center;
   bottom: 50px;
   background-color: rgb(75, 49, 123, 0.8);
   color: white;
   box-sizing: border-box;
   font-size: 2em;
   padding: 10px;
}

.radius {
    border-radius: 100px;
    margin-bottom: 30px;

    
    animation-name: moveInTop;
    animation-duration: 5s;
    animation-fill-mode: backwards; 
    animation-play-state: running;
    animation-timing-function: ease-out;
}



@keyframes moveInTop {
    0% {
     opacity: 0;
     transform: translateY(-30px);
    }

     100% {
     opacity: 1;
     transform: translate(0);
    }
}

.position {
    margin-right: 300px !important;
    margin-left: 300px!important;
}

.bolder2 {
    font-size: 30px;
    font-weight: bolder;
   

    animation-name: moveInBottom;
    animation-duration: 5s;
    animation-fill-mode: backwards; 
    animation-play-state: running;
    animation-timing-function: ease-out
}



@keyframes moveInBottom {
    0% {
     opacity: 0;
     transform: translateY(30px);
    }

     100% {
     opacity: 1;
     transform: translate(0);
    }
}
</style>
