<template>
  <div>
    <div class="step-input">
      <div v-for="inputItem in inputItems" :key="inputItem">
        <div class="step-title">{{ inputItem.label }}</div>
        <input-component
          :inputItem="inputItem"
          @changeInput="changeInput"
          :name="changeInput.label"
        ></input-component>
        <p class="message">{{ inputItem.message }}</p>
      </div>
    </div>
    <div class="btn-ctn">
      <div
        v-if="
          state.currentStep > 0 && state.currentStep < state.formStep.length
        "
      >
        <button @click="handlePrevious" class="btn-previous">PREVIOUS</button>
        <button @click="handleNext" class="btn-next">NEXT</button>
      </div>
      <div v-else>
        <button @click="handleRest" class="btn-previous">Reset</button>
        <button @click="handleNext" class="btn-next">NEXT</button>
      </div>
    </div>
  </div>
</template>
<script>
import InputComponent from "./InputComponent.vue";
export default {
  name: "FormValidation",
  components: {
    InputComponent,
  },
  props: {
    state: {
      type: Object,
    },
  },
  computed: {
    inputItems() {
      return this.state.formStep[this.state.currentStep - 1].listField;
    },
  },
  methods: {
    changeInput(e) {
      this.$emit("changeInput", e);
    },

    handleNext() {
      this.$emit("handleNext");
    },
    handlePrevious() {
      this.$emit("handlePrevious");
    },
    handleRest() {
      this.$emit("handleRest");
    },
  },
};
</script>

<style scoped>
.step-input {
  text-align: left;
  border-radius: 12px;
  background-color: #fff;
  box-shadow: 0 4px 10px rgb(0 0 0 / 20%), 6px 12px 20px rgb(0 0 0 / 10%);
  margin-top: 15px;
  padding: 20px;
}
.step-title {
  margin: 10px 0px;
}
.btn-ctn {
  margin-top: 50px;
}
.btn-previous {
  background-color: #72e6b1;
  border: unset;
  font-size: 16px;
  font-weight: 600;
  text-transform: uppercase;
  color: #fff;
  padding: 8px 42px;
  border-radius: 12px;
  cursor: pointer;
  box-shadow: 1px 1px 10px rgb(0 0 0 / 40%);
  transition: box-shadow 0.35s ease-out;
  margin-right: 20px;
}
.btn-next {
  background-color: #1e68cf;
  border: unset;
  font-size: 16px;
  font-weight: 600;
  text-transform: uppercase;
  color: #fff;
  padding: 8px 42px;
  border-radius: 12px;
  cursor: pointer;
  box-shadow: 1px 1px 10px rgb(0 0 0 / 40%);
  transition: box-shadow 0.35s ease-out;
}
.message {
  color: red;
}
</style>
