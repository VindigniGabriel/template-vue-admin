<template>
  <v-main>
    <transition name="ggsac">
      <router-view />
    </transition>
    <dashboard-core-footer />
  </v-main>
</template>

<script>
export default {
  name: "DashboardCoreView",

  components: {
    DashboardCoreFooter: () => import("./Footer")
  }
};
</script>

<style>
* base */ .ggsac {
  backface-visibility: hidden;
  z-index: 1;
}

/* moving */
.ggsac-move {
  transition: all 600ms ease-in-out 50ms;
}

/* appearing */
.ggsac-enter-active {
  transition: all 400ms ease-out;
}

/* disappearing */
.ggsac-leave-active {
  transition: all 200ms ease-in;
  position: absolute;
  z-index: 0;
}

/* appear at / disappear to */
.ggsac-enter,
.ggsac-leave-to {
  opacity: 0;
}
</style>