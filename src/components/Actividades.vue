<template>
  <div id="actividades">
    <div v-for="(activity, index) in activities" :key="activity.id">
      <router-link v-bind:to="'/actividades/'+activity.id">
        <ActividadCard :image="activitiesDescription[index].image[0]" :title="activity.title"
          :address="activitiesDescription[index].locations[0].address"
          :province="activitiesDescription[index].locations[0].province"
          :description="activitiesDescription[index].description" :points="activity.points"
          v-if="activitiesDescription[index].participants != 1" :icon="iconUserFriends" />
      </router-link>
      <router-link v-bind:to="'/actividades/'+activity.id">
        <ActividadCard :image="activitiesDescription[index].image[0]" :title="activity.title"
          :address="activitiesDescription[index].locations[0].address"
          :province="activitiesDescription[index].locations[0].province"
          :description="activitiesDescription[index].description" :points="activity.points"
          v-if="activitiesDescription[index].participants == 1" :icon="iconUser" />
      </router-link>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  import ActividadCard from './/ActividadCard';
  import {
    faUser,
    faUserFriends
  } from '@fortawesome/free-solid-svg-icons'


  export default {
    name: 'Actividades',
    components: {
      ActividadCard
    },
    props: {
      page: Number

    },
    data() {
      return {
        activities: [],
        activitiesDescription: [],
        iconUser: faUser,
        iconUserFriends: faUserFriends
      }
    },
    methods: {
      getActivities(page) {
        axios
          .get("https://json-biglifeapp.herokuapp.com/activity?_page=" + page + "&_limit=9")
          .then(res => {
            this.activities = res.data;
            this.activitiesDescription.length = 0;
            this.activities.forEach(a => {
              this.activitiesDescription.push(JSON.parse(a.activity));
            })
          })
          .catch(e => console.log(e))
      }
    },
    watch: {
      page: function () {
        this.getActivities(this.page)
      }
    },
    mounted() {
      this.getActivities()
    }
  }
</script>