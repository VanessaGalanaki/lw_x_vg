
<template>
  <select  ref="mValue.value" v-if="multiple_values.length > 0" v-model="selectValue" @change="onSelectValue(selectValue, trigger)">
    <option disabled value="">Please select one</option>
    <option
      :key="mValue.id"
      v-for="mValue in multiple_values"
      :value="mValue.value"
     
      
    >
      {{ mValue.descr }}
    </option>
  </select>
</template>


<script>
export default {
  name: "Dropdown_element",
  props: {
    multiple_values: Array,
    trigger: Object
  },
  data() {
    return {
      selectValue: "",
    };
  },
   methods: {
    onSelectValue (selectValue, trg) {
      this.$emit('clicked', selectValue , trg)
      this.$emit('input',selectValue);
    }
  }
};
</script>

<style src="../../assets/css/elements/trigger_dropdown.css"></style>