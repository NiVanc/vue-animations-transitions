<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <h1>Animations</h1>
        <hr />
        <select v-model="animationStyle" class="form-control">
          <option value="fade">Fade</option>
          <option value="slide">Slide</option>
        </select>
        <br />
        <button class="btn btn-primary" @click="show = !show">Show alert</button>
        <br />
        <br />
        <transition :name="animationStyle">
          <div class="alert alert-info" v-if="show">This is a info alert, check it out!</div>
        </transition>
        <transition name="slide" type="animation">
          <div class="alert alert-info" v-if="show">This is a info alert, check it out!</div>
        </transition>
        <transition appear enter-active-class="animated bounce" leave-active-class="animated shake">
          <div class="alert alert-info" v-if="show">This is a info alert, check it out!</div>
        </transition>
        <hr />
        <transition :name="animationStyle" mode="out-in">
          <div class="alert alert-info" v-if="show">This is a info alert, check it out!</div>
          <div class="alert alert-warning" v-else>This is a warning alert, check it out!</div>
        </transition>
        <hr />
        <button class="btn btn-primary" @click="load = !load">Load or remove element</button>
        <br />
        <br />
        <transition
          @before-enter="beforeEnter"
          @enter="enter"
          @after-enter="afterEnter"
          @enter-cancelled="enterCancelled"
          @before-leave="beforeLeave"
          @leave="leave"
          @after-leave="afterLeave"
          @leave-cancelled="leaveCancelled"
        >
          <div
            style="width: 100px; height: 100px; background: lightgreen; border: 1px solid green"
            v-if="load"
          ></div>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      show: false,
      load: true,
      animationStyle: "fade"
    };
  },
  methods: {
    beforeEnter(el) {
      console.log("beforeEnter");
    },
    enter(el, done) {
      console.log("Enter");
      done();
    },
    afterEnter(el) {
      console.log("afterEnter");
    },
    enterCancelled(el) {
      console.log("enterCancelled");
    },
    beforeLeave(el) {
      console.log("beforeLeave");
    },
    leave(el, done) {
      console.log("Leave");
      done();
    },
    afterLeave(el) {
      console.log("afterLeave");
    },
    leaveCancelled(el) {
      console.log("leaveCancelled");
    }
  }
};
</script>

<style>
.fade-enter {
  opacity: 0;
}

.fade-enter-active {
  transition: opacity 1s;
}

.fade-leave {
}

.fade-leave-active {
  transition: opacity 1s;
  opacity: 0;
}

.slide-enter {
  opacity: 0;
}

.slide-enter-active {
  animation: slide-in 1s ease-out forwards;
  transition: opacity 1s;
}

.slide-leave {
}

.slide-leave-active {
  animation: slide-out 1s ease-out forwards;
  transition: 1s ease-out forwards;
}

@keyframes slide-in {
  from {
    transform: translateY(20px);
  }
  to {
    transform: translateY(0px);
  }
}

@keyframes slide-out {
  from {
    transform: translateY(0);
  }
  to {
    transform: translateY(20px);
  }
}
</style>
