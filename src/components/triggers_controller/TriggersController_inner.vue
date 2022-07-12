<template>
  <div class="trigger-controller-inner-container">
    <label
      @click="activatePopupEngines(trigger)"
      class="aqua-color bold trigger-controller-inner-main-label"
      >Automatically show</label
    >
    <div class="triggers-table">
      <Checkbox_element :triggers="triggers" />
    </div>
  </div>
</template>




<script>
import Checkbox_element from "../elements/Checkbox.vue";

export default {
  name: "TriggersController_inner",
  components: {
    Checkbox_element,
  },
  data() {
    return {
      triggers: [],
    };
  },
  created() {
    this.triggers = [
      {
        id: 1,
        descr: "Show on timer",
        type: "timer",
        isChecked: false,
        has_values: true,
        multiple_values: [
          {
            id: "tr_timer1",
            value: 3000,
            descr: "After 0.5 minutes",
          },
          {
            id: "tr_timer2",
            value: 6000,
            descr: "After 1 minutes",
          },
          {
            id: "tr_timer3",
            value: 90000,
            descr: "After 1.5 minutes",
          },
        ],
      },
      {
        id: 2,
        descr: "Show after scrolling",
        type: "scroll",
        isChecked: false,
        has_values: true,
        multiple_values: [
          {
            id: "tr_scroll1",
            value: 20,
            descr: "25% of page",
          },
          {
            id: "tr_scroll2",
            value: 45,
            descr: "50% of page",
          },
          {
            id: "tr_scroll3",
            value: 98,
            descr: "100% of page",
          },
        ],
      },
      {
        id: 3,
        descr: "Show on exit intent",
        type: "exit",
        isChecked: false,
        has_values: false,
        multiple_values: [],
      },
    ];
  },
};
</script>
<style src="../../assets/css/triggers_controller/triggers_inner.css"></style>
