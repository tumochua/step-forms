<template>
  <div class="header">
    <div v-for="header in state.formStep" :key="header">
      <div :class="{ active: header.stepId === state.currentStep }">
        <div class="header-item">
          <span class="header-number">{{ header.stepId }}</span>
          <span>{{ header.stepName }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeaderVue",
  props: {
    state: {
      type: Object,
    },
  },
  created() {},
};
</script>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
  border-radius: 12px;
  background-color: #fff;
  box-shadow: 0 4px 10px rgb(0 0 0 / 20%), 6px 12px 20px rgb(0 0 0 / 10%);
  margin-top: 15px;
  padding: 20px;
}
.active {
  border-radius: 12px;
  border: 2px solid #9fbcd7;
}
.header-item {
  padding: 8px 20px;
  border-radius: 12px;
  background-color: #f3f3f3;
}
.header-number {
  display: inline-block;
  font-size: 16px;
  width: 24px;
  height: 24px;
  line-height: 24px;
  border-radius: 50%;
  color: #f7f7f7;
  background-color: #969899;
  margin-right: 8px;
}
</style>
