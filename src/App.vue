<template>
  <div id="app">

    <!-- navbar -->
    <nav class="navbar is-transparent" v-show="$root.ready">
      <div class="container">
        <div v-if="$root.storage" class="navbar-brand">
          <router-link v-if="$root.storage.header" class="navbar-item" to="/">
            <img :src="$root.storage.header.logo">
            <span class="is-size-5 has-text-weight-bold" v-html="$root.storage.header.text"></span> <span class="is-size-6 is-slogan is-capitalize" v-html="$root.storage.header.subtext"></span>
          </router-link>
          <div class="navbar-burger burger" data-target="navMenu">
            <span></span>
            <span></span>
            <span></span>
          </div>
        </div>
        <div id="navMenu" class="navbar-menu" v-if="$root.storage">
          <div class="navbar-start">
            <router-link v-for="item in $root.storage.header.options" :key="item.link" class="navbar-item" :to="item.link" v-html="item.text"></router-link>
          </div>
        </div>
      </div>
    </nav>    

    <!-- template -->
    <keep-alive>
      <transition
        name="fade"
        mode="out-in"
        @beforeLeave="beforeLeave"
        @enter="enter"
        @afterEnter="afterEnter">
        <router-view/>
      </transition>
    </keep-alive>    

    <!-- footer -->
    <div class="footer" v-if="$root.storage" v-show="$root.ready">
      <div class="container" v-if="$root.storage.footer">  
        <div class="columns">
          <div v-for="group in $root.storage.footer.options" :key="group.text" class="column has-text-left">
            <strong v-html="group.text"></strong>
            <p v-for="item in group.options">
              <router-link v-if="!item.is_blank && !item.target" :to="item.link">
                <span v-show="item.faicon" :class="'fa fa-' + item.faicon"></span>
                <span :title="item.title" v-html="item.text"></span>
              </router-link>
              <a v-if="item.is_blank" :href="item.link">
                <span v-show="item.faicon" :class="'fa fa-' + item.faicon"></span>
                <span :title="item.title" v-html="item.text"></span>
              </a>
              <a v-if="item.target" href="#" :data-target="item.target" class="modal-button">
                <span v-show="item.faicon" :class="'fa fa-' + item.faicon"></span>
                <span :title="item.title" v-html="item.text"></span>
              </a>
            </p>
          </div>
        </div>
        <div class="has-text-center is-size-6" v-if="$root.storage">
          <strong v-html="$root.storage.footer.text"></strong> <span v-html="$root.storage.footer.subtext"></span>
        </div>
      </div>
    </div>

    <div class="d-hotline animated zoomIn">
      <a class="is-hidden-tablet" href="whatsapp://send?phone=+54 9 11 5718-2736&amp;text=Hola, estoy interesado en obtener un turno en Cigue">
        <div class="chat-content">
          <i class="fa fa-whatsapp"></i>
        </div>
      </a>
      <a class="is-hidden-mobile" href="https://web.whatsapp.com/send?phone=5491157182736&amp;text=Hola, estoy interesado en obtener un turno en Cigue">
        <div class="chat-content">
          <i class="fa fa-whatsapp"></i>
        </div>
      </a>
    </div>   

    <!-- modals -->
    <div id="modal-terminos" class="modal">
      <div class="modal-background"></div>
      <button aria-label="close" class="delete is-large"></button>
      <div class="modal-content has-background-white">
        <div class="section animated zoomIn">
          <div class="has-text-centered">
            <h1 class="is-size-4 has-text-weight-semibold">Cigue</h1>
            <h1 class="is-size-5 has-text-weight-semibold">Cigliutti Guerini</h1>
            <h4 class="is-size-6">Términos y Condiciones</h4></div>
          <div class="has-text-left">
            <h1 class="garantia--h">Términos y Condiciones de uso</h1>
            <h5 class="titlesection"></h5>
            <p>La plataforma web de turnos online de Cigue Concesionario Oficial Mercedes-Benz www.TurnosCigue.com.ar, a partir de ahora "La plataforma" es de uso exclusivo para clientes Mercedes-Benz de la república Argentina.</p>
            <p>La plataforma es de uso estrictamente de contacto para establecer un vínculo directo con el asesor comercial que lo contactará a la brevedad para confirmar el turno y el horario deseado, no generando un compromiso ni obligación de turno por la selección realizada hasta en tanto el asesor comercial no se contacte de manera directa. </p>
            <p>Ante cualquier consulta, necesidad o sugerencia puede contactarnos de forma directa a <a href="mailto:mercedesbenz@atencionweb.com">MercedesBenz@atencionweb.com</a> o por telefóno al número <a href="tel:+54 11 5718 2736">+54 11 5718 2736</a></p>
            <p></p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'app',
  data() {
    return {
      prevHeight: 0,
    };
  },
  methods: {
    beforeLeave(element) {
      this.prevHeight = getComputedStyle(element).height;
    },
    enter(element) {
      const { height } = getComputedStyle(element);

      element.style.height = this.prevHeight;

      setTimeout(() => {
        element.style.height = height;
      });
    },
    afterEnter(element) {
      element.style.height = 'auto';
    }
  }
}

</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.fade-enter-active,
.fade-leave-active {
  transition-property: opacity;
  transition-duration: 0.3s;
  transition-property: height, opacity;
  transition-timing-function: ease;
  overflow: hidden;
}

.fade-enter,
.fade-leave-active {
  opacity: 0
}

.slide-left-enter-active,
.slide-left-leave-active,
.slide-right-enter-active,
.slide-right-leave-active {
  transition-duration: 0.5s;
  transition-property: height, opacity, transform;
  transition-timing-function: cubic-bezier(0.55, 0, 0.1, 1);
  overflow: hidden;
}

.slide-left-enter,
.slide-right-leave-active {
  opacity: 0;
  transform: translate(2em, 0);
}

.slide-left-leave-active,
.slide-right-enter {
  opacity: 0;
  transform: translate(-2em, 0);
}

.zoom-enter-active,
.zoom-leave-active {
  animation-duration: 0.5s;
  animation-fill-mode: both;
  animation-name: zoom;
}

.zoom-leave-active {
  animation-direction: reverse;
}

@keyframes zoom {
  from {
    opacity: 0;
    transform: scale3d(0.3, 0.3, 0.3);
  }

  100% {
    opacity: 1;
  }
}

</style>
