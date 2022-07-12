<template>
<div class="line-draw"></div>
  <div class="trigger-controller-footer-container">
    <label class="aqua-color bold">Trigger Automatically At Most</label>
    <div class="triggers-table">
      
        <Dropdown_element  :multiple_values="occurance" />

    </div>
  </div>
</template>




<script>
import Dropdown_element from "../elements/Dropdown.vue";

export default {
  name: "TriggersController_footer",
  components: {
    Dropdown_element
},
  data() {
    return {
      occurance: [],
    };
  },
  created() {
   this.occurance = [{
        descr:'Every week',
        value:7,
        id:'occ_1'
   },
   {
        descr:'Every 2 weeks',
        value:14,
        id:'occ_2'
   }]
  },
};
</script>
<style src="../../assets/css/triggers_controller/triggers_footer.css"></style>
