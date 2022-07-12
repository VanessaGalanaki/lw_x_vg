<template>
  <div
    class="trigger-checkbox-main"
    :key="trigger.id"
    v-for="trigger in triggers"
  >
    <input
      :value="trigger.type"
      type="checkbox"
      v-model="selectedTypes"
      v-on:change="check($event, trigger)"
    />
    <label>{{ trigger.descr }}</label>
    <Dropdown_element
      v-show="trigger.has_values === true"      
      :multiple_values="trigger.multiple_values"
      :trigger="trigger"
      :disabled="!trigger.isChecked"
      @clicked="onSelectOccurrence"
    />
  </div>
  
    <Popup_element @interface="getChildInterface"></Popup_element>
 
</template>

<script>
import Dropdown_element from "./Dropdown.vue";
import Popup_element from "./Popup.vue";

export default {
  name: "Checkbox_element",
  components: {
    Dropdown_element,
    Popup_element,
  },
  childInterface: {
    activatePopupEngines: (trigger) => {
      trigger;
    },
  },
  props: {
    triggers: Array,
  },
  data() {
    return {
      selectedTypes: [],
      key: "",
    };
  },
  methods: {
    getChildInterface(childInterface) {
      this.$options.childInterface = childInterface;
    },
    activatePopupEngines(trigger) {
      this.$options.childInterface.activatePopupEngines(trigger);
    },
    onSelectOccurrence(value, trg) {
      this.$options.childInterface.activatePopupEngines(trg, value);
    },
    check(event, trg) {
      trg.isChecked =
        event.target.value === trg.type &&
        this.selectedTypes.includes(trg.type);
      if (trg.multiple_values.length === 0) {
             this.$options.childInterface.activatePopupEngines(trg, 0);

      }
    },
  },
};
</script>

<style src="../../assets/css/elements/trigger_checkbox.css"></style>


