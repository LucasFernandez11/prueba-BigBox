<template>
    <div id="actividad-info">
        <div class="actividad-header">
                <img class="actividad-header-image" :src=image />
            <div class="actividad-header-info">
                <h2 class="actividad-header-info-title">{{title}}</h2>
                <p class="actividad-header-info-text">{{text}}</p>
                <div class="actividad-header-info-participants">
                    <i/>
                    <p class="actividad-header-info-participants-text">Para {{participants}} personas</p>
                </div>
                <p class="actividad-header-info-location">
                    <font-awesome-icon class="actividad-header-info-location-icon" :icon="locationIcon" />
                 {{province}}</p>
                <p class="actividad-header-info-points">{{points}} puntos</p>
            </div>
        </div>
    </div>    
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faMapMarkerAlt } from '@fortawesome/free-solid-svg-icons'

export default {
    name: 'ActividadInfo',
    components: {
        
        FontAwesomeIcon
        },
    props: {
        image: String,
        title: String,
        text: String,
        participants: Number,
        province: String ,
        points: Number,
        benefits: String,
        description: String 
    },
    data () {
    return {
      locationIcon: faMapMarkerAlt
    }
  }
}
</script>