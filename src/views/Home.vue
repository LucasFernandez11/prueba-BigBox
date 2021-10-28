<template>
    <div id="home">
      <Actividades :page="page"/>
        <nav class="pagination" role="navigation" aria-label="pagination">
          <back-to-top class="pagination-btt pagination-arrow">
            <a class="pagination-arrow" v-on:click="changePage(page-1)">
              <font-awesome-icon :icon="previous" />
            </a>
          </back-to-top>
            <ul class="pagination-list">
              <back-to-top class="pagination-btt">
                <li>
                    <a v-bind:class="page == 1?'pagination-link-active':'pagination-link'" v-on:click="changePage(page=1)">1</a>
                    <a v-bind:class="page >1?'pagination-link-active':'pagination-link-not'" >{{page}}</a>
                    <a class="pagination-link"  v-on:click="changePage(page+1)">{{page+1}}</a>
                    <a class="pagination-link" v-on:click="changePage(page+2)" >{{page +2}}</a>
                    <a class="pagination-link" v-on:click="changePage(page+3)" >{{page +3}}</a>
                    <a class="pagination-link" v-on:click="changePage(page+4)" >{{page +4}}</a>
                    <a class="pagination-link" v-on:click="changePage(page+5)" >{{page +5}}</a>
                    <a class="pagination-link-text">...</a>
                    <a class="pagination-link" v-on:click="changePage(pages)">{{pages}}</a>
                </li>
              </back-to-top>
            </ul>

            <back-to-top class="pagination-btt pagination-arrow">
              <a class="pagination-arrow" v-on:click="changePage(page+1)">
              <font-awesome-icon :icon="next" />
              </a>
            </back-to-top>

        </nav>
    </div>
</template>

<script>
import axios from 'axios';
import Actividades from '../components/Actividades'
import BackToTop from 'vue-backtotop';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faChevronCircleRight, faChevronCircleLeft } from '@fortawesome/free-solid-svg-icons'

export default {
  components: { 
    Actividades, 
    FontAwesomeIcon,
    BackToTop
   },
    name: 'Home',
    data(){
        return{
            activities: [],
            page: 1,
            pages: Number,
            previous: faChevronCircleLeft,
            next: faChevronCircleRight
        }
    },
  methods: {
    changePage(page){
    this.page = page <= 0 || page > this.pages ? this.page : page;
    console.log(page)
  }, 
    getActivities(){
      const params = {
        page: this.page
      }
      axios
        .get(`https://json-biglifeapp.herokuapp.com/activity`, {params})
          .then(res =>{
            this.activities = res.data;
            this.pages = parseInt(this.activities.length / 9);
          })
          .catch(e => console.log(e))
    }
  },
  mounted(){
    this.getActivities()
  }
}
</script>
<style lang="scss">
@import '../assets/scss/main.scss';
</style>