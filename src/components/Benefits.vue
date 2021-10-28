<template>
    <div id="benefits">
        <div>
        <div class="benefits-title">
            <h3 class="benefits-title-text">¿Qué incluye?</h3>
            <hr class="benefits-title-line"/>
        </div>
        <div class="benefits-list">
            <p v-html="benefits"></p>
        </div>
        <p class="benefits-description">{{description}}</p> 
        </div>

         <div id="reglas">
        <h3 class="reglas-title">
        <font-awesome-icon class="reglas-title-icon" :icon="icon" /> 
        Reglas:</h3>
        <p class="reglas-text">{{small_print}}</p>
    </div>

    </div>
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faFileAlt } from '@fortawesome/free-solid-svg-icons'
export default {
    name: 'Benefits',
    components: {FontAwesomeIcon},
      props: {
        benefits: String,
        description: String,
        small_print: String
    },
     data () {
    return {
      icon: faFileAlt
    }
  }
}
</script>