<template>
     <div id="card">
        <div class="card-img">
            <img :src=image />
        </div>
        <div class="card-header">
            <h3 class="card-header-title">{{title}}</h3>
            <font-awesome-icon class="card-header-icon" :icon=icon /> 
        </div>
        <div class="card-location">
            <h4 class="card-location-info">
                <font-awesome-icon class="card-location-icon" :icon="locationIcon" /> 
                {{address}}, {{province}}</h4>
        </div>
        <div class="card-description">
            <p class="card-description-text">{{description}}</p>
        </div>
        <div class="card-points">
            <p class="card-points-text">{{points}} puntos</p>
        </div> 
    </div>
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faMapMarkerAlt } from '@fortawesome/free-solid-svg-icons'

export default {
    name: 'ActividadCard',
    components: {FontAwesomeIcon},
    props: {
        image: String,
        title: String,
        icon: Object,
        address: String,
        province: String ,
        description: String, 
        points: Number
    },
  data () {
    return {
      locationIcon: faMapMarkerAlt
    }
  }
}
</script>