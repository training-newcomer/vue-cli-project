<template>
  <div id="app">
    <TheHeader text="My counter" />
    <div v-if="!validationMessageList.length">{{ count }}</div>
    <div v-else v-for="message in validationMessageList" :key="message">
      {{ message }}
    </div>

    <div class="btnContainer">
      <BaseButton :disabled="hasMaxCount" @onClick="plusOne">+</BaseButton>
      <BaseButton :disabled="hasMinCount" @onClick="minusOne">-</BaseButton>
      <NumberInput v-model.number="inputCount" max="9999" min="0" />
      <BaseButton @onClick="insertCount">insert</BaseButton>
    </div>
  </div>
</template>

<script>
import TheHeader from "./components/TheHeader.vue";
import BaseButton from "./components/BaseButton.vue";
import NumberInput from "./components/NumberInput.vue";

export default {
  name: "App",
  components: {
    TheHeader,
    BaseButton,
    NumberInput,
  },
  data() {
    return {
      count: 0,
      inputCount: 0,
      isEditing: false,
    };
  },
  watch: {
    inputCount() {
      this.isEditing = true;
    },
  },
  computed: {
    hasMaxCount() {
      return this.count >= 9999;
    },
    hasMinCount() {
      return this.count <= 0;
    },
    hasMaxInputCount() {
      return this.inputCount > 9999;
    },
    hasMinInputCount() {
      return this.inputCount < 0;
    },
    validationMessageList() {
      const validationList = [];

      if (this.isEditing) {
        validationList.push("editing...");
      }

      if (this.hasMaxInputCount) {
        validationList.push("9999以上は入力できません");
      }

      if (this.hasMinInputCount) {
        validationList.push("0以下は入力できません");
      }

      return validationList;
    },
  },
  methods: {
    plusOne() {
      this.count++;
    },
    minusOne() {
      this.count--;
    },
    insertCount() {
      if (this.hasMaxInputCount || this.hasMinInputCount) {
        return;
      }
      this.count = this.inputCount;
      this.isEditing = false;
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.btnContainer {
  margin: 12px auto 0;
}
</style>
