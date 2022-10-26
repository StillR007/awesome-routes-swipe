<template>
  <div class="about">
    <h1>This is an about page</h1>
    <HelloWorld msg="This is an about page" />
  </div>
</template>

<script>
import HelloWorld from "@/components/HelloWorld.vue";
import Hammer from "hammerjs";

export default {
  name: "AboutView",
  components: {
    HelloWorld,
  },
  data: () => ({
    routeIndex: 1,
  }),
  created() {
    const body = document.querySelector("body");
    const manager = new Hammer.Manager(body);
    const Swipe = new Hammer.Swipe({ threshold: 5, velocity: 0.3 });
    manager.add(Swipe);

    manager.on("swipe", (e) => {
      let direction = e.offsetDirection;

      if (direction === 2) {
        try {
          const { routes } = this.$router.options;
          this.$router.push(routes[this.routeIndex + 1]);
        } catch (e) {
          console.error(e);
        }
      }
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
