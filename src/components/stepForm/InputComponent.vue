<template>
  <div class="input-ctn">
    <div
      v-if="
        inputItem.type === 'text' ||
        inputItem.type === 'email' ||
        inputItem.type === 'number'
      "
    >
      <input
        :type="inputItem.type"
        class="input-item"
        :placeholder="inputItem.label"
        :value="inputItem.value"
        @input="changeInput($event, inputItem)"
      />
    </div>
    <div>
      <div v-if="inputItem.type === 'select'">
        <select id="cars" class="input-select" v-model="inputForm">
          <option value="volvo">Volvo</option>
          <option value="saab">Saab</option>
          <option value="vw">VW</option>
          <option value="audi" selected>Audi</option>
        </select>
      </div>
      <div v-if="inputItem.type === 'checkbox'">
        <input type="checkbox" />
        <label>{{ inputItem.title }}</label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "InputComponent",
  props: {
    inputItem: {
      type: Object,
    },
    name: {
      type: String,
    },
  },
  data() {
    return {};
  },
  methods: {
    changeInput(event, name) {
      this.$emit("changeInput", {
        value: (name.value = event.target.value),
        name: name,
      });
    },
  },
  computed: {
    valueInput: {
      setValue(value) {
        return this.$emit("changeInput", { name: this.name, value });
      },
    },
  },
};
</script>

<style scoped>
.input-item {
  color: #586068;
  font-size: 16px;
  width: 95%;
  padding: 8px 16px;
  border-radius: 4px;
  border: 1px solid #ccc;
  outline: 3px solid transparent;
}
.input-select {
  width: 100%;
  padding: 15px;
  border-radius: 6px;
  text-align: center;
  cursor: pointer;
}
</style>
