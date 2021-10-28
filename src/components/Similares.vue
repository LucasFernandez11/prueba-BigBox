<template>
    <div id="similares">
        <h3 class="similares-title">Otras actividades similares:</h3>
        <div class="similares-cards" >
         <div v-for="(similar, index) in similares" :key="similar.id">
        <router-link v-bind:to="'/actividades/'+similar.id">
       <ActividadCard :image="similaresDescription[index].image[0]" :title="similar.title" :address="similaresDescription[index].locations[0].address" :province="similaresDescription[index].locations[0].province" :description="similaresDescription[index].description" :points="similar.points" v-if="similaresDescription[index].participants != 1" :icon="iconUserFriends"/>
        </router-link>
        <router-link v-bind:to="'/actividades/'+similar.id">
       <ActividadCard :image="similaresDescription[index].image[0]" :title="similar.title" :address="similaresDescription[index].locations[0].address" :province="similaresDescription[index].locations[0].province" :description="similaresDescription[index].description" :points="similar.points" v-if="similaresDescription[index].participants == 1" :icon="iconUser"/>
        </router-link>
      </div>
      </div>
    </div>
</template>

<script>
import axios from 'axios';
import ActividadCard from './ActividadCard';
import { faUser, faUserFriends } from '@fortawesome/free-solid-svg-icons'

export default {
    name: 'Similares',
    components: {
    ActividadCard
  },
  props:{
    activity_type: String

  },
  data(){
    return{
      activities: [],
      similares: [],
      similaresDescription: [],
      iconUser: faUser,
      iconUserFriends: faUserFriends
    }
  },
  methods: {
    getActivities(){
      axios
        .get("https://json-biglifeapp.herokuapp.com/activity?_page=1&_limit=50")
          .then(res =>{
            this.activities = res.data;
            this.similares = this.activities.filter(a => a.activity_type == this.activity_type)
            this.similares = this.similares.slice(0, 3);
            this.similares.forEach(s => {
            this.similaresDescription.push(JSON.parse(s.activity));
            })
            console.log(this.similares)
            console.log(this.similaresDescription)
          })
          .catch(e => console.log(e))
    }
    },
  mounted(){
    this.getActivities()
  }
}

</script>