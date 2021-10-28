<template>
    <div id="actividad">
      <div class="actividad-arrow">
        <router-link to="/actividades">
        <font-awesome-icon :icon="arrow" />
        </router-link>
      </div>
        <ActividadInfo :image="activityDescription.image[0]" :title="activity.title" :text="activityDescription.description" :province="activityDescription.locations[0].province" :participants="activityDescription.participants" :points="activity.points" />
        <Benefits :description="activityDescription.description" :benefits="activityDescription.benefits" :small_print="activityDescription.small_print"/>
        <Similares :activity_type="activity.activity_type"/>
    </div>
</template>

<script>
import axios from 'axios';
import ActividadInfo from '../components/ActividadInfo'
import Benefits from '../components/Benefits'
import Similares from '../components/Similares'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faArrowLeft } from '@fortawesome/free-solid-svg-icons'

export default {
    name: 'Actividad',
    components: {
      ActividadInfo, 
      Benefits,
      Similares,
      FontAwesomeIcon
  },
    data(){
        return{
          activity: null,
          activityDescription: null, 
          id: this.$route.params.id,
          arrow: faArrowLeft
        }
    },
     methods: {
    getActivity(){
      axios
        .get(`https://json-biglifeapp.herokuapp.com/activity/${this.id}`)
          .then(res =>{
            this.activity = res.data;
            this.activityDescription = JSON.parse(this.activity.activity);
          })
          .catch(e => console.log(e))
    }
  },
  mounted(){
    this.getActivity()
  } 
}
</script>