<template>
  <div
    :style="{
      width:
        (state.currentStep / Object.keys(state.formStep).length) * 100 + '%',
    }"
    class="progressbar"
  ></div>
</template>

<script>
export default {
  name: "ProgressBar",
  props: {
    state: {
      type: Object,
    },
  },
};
</script>

<style scoped>
.progressbar {
  background-color: #437fe8;
  border-radius: 12px;
  transition: width 0.5s ease;
  height: 18px;
  margin: 20px 0px;
}
</style>
