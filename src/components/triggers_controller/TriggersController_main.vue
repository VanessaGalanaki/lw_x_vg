<template>
  <div class="trigger-controller-main-container">
    <div class="trigger-header">
      <h1>
        git commit -m "Philosophy triggers about learning VG"
      </h1>
    </div>

    <div class="trigger-inner">
      <div class="trigger-title">
        <h3>Popup triggers</h3>
      </div>
      <TriggersController_inner />
      <TriggersController_footer />
    </div>
  </div>
</template>

<script>
import TriggersController_inner from "./TriggersController_inner.vue";
import TriggersController_footer from "./TriggersController_footer.vue";

export default {
  name: "TriggersController_main",
  components: {
    TriggersController_inner,
    TriggersController_footer,
  },
};
</script>

<style src="../../assets/css/triggers_controller/triggers_main.css"></style>
