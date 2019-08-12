<template>
  <section class="hero">
    <div class="hero-body">
      <div class="container">
        <div class="content splash">
          <div class="gradient"></div>
          <div v-if="$root.storage && $root.storage.announcement">
            <h1 v-html="$root.storage.announcement.title"></h1>
            <p v-html="$root.storage.announcement.message"></p>
            <div class="columns is-vcentered has-text-centered">
              <div class="column">
                <router-link class="button is-success is-large" to="/turno">
                  <span>Solicitar Turno</span>
                </router-link>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>  
  </section>
</template>

<script>
import { snackbar } from '@/components/Snackbar';

export default {
  name: 'TurnosCigue',
  data () {
    return {
      _gtag: gtag
    }
  },                 
  mounted: function() {
    this.loading = false
  }
}
</script>

<style type="text/css">
  .splash {
    padding-bottom: 5rem;
    min-height: 70vh;
    background-image: url('/static/img/atencion.svg');
    background-position: center 150px;
    background-repeat: no-repeat;
    background-size: contain;
  }
  .gradient {
    position: absolute;
    top: 0;
    left:0;
    right: 0;
    bottom: 0;
background: rgb(255,255,255);
background: linear-gradient(180deg, rgba(255,255,255,0) 0%, rgba(255,255,255,0) 50%, rgba(255,255,255,1) 100%);
  }
</style>