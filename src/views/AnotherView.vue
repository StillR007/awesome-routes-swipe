<template>
  <div class="another">
    <h1>This is an another page</h1>
    <HelloWorld msg="Another page" />
  </div>
</template>

<script>
import HelloWorld from "@/components/HelloWorld.vue";
import Hammer from "hammerjs";

export default {
  name: "AnotherView",
  components: {
    HelloWorld,
  },
  data: () => ({
    routeIndex: 2,
  }),
  created() {
    const body = document.querySelector("body");
    const manager = new Hammer.Manager(body);
    const Swipe = new Hammer.Swipe({ threshold: 5, velocity: 0.3 });
    manager.add(Swipe);

    manager.on("swipe", (e) => {
      let direction = e.offsetDirection;

      if (direction === 4) {
        try {
          const { routes } = this.$router.options;
          this.$router.push(routes[this.routeIndex - 1]);
        } catch (e) {
          console.error(e);
        }
      }
    });
  },
};
</script>
