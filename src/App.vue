<template>
  <div class="flex justify-center">
    <div class="flex flex-col">
      <input
        type="number"
        v-model="num1"
        placeholder="Enter a number"
        class="border rounded mb-2 px-2 py-1 outline-none"
      />
      <input
        type="number"
        v-model="num2"
        placeholder="Enter a number"
        class="border rounded px-2 py-1 outline-none"
      />
      <div class="mt-4 flex items-center justify-between">
        <h4 class="mr-2">Sum: {{ sum }}</h4>
        <button
          class="rounded bg-blue-500 hover:bg-blue-700 py-1 px-4 text-white"
          @click="handleClick()"
        >
          Sum
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, ref } from "vue";
import { useStore } from "vuex";
import { key } from "./store";

export default defineComponent({
  name: "App",
  setup() {
    const store = useStore(key);
    const num1 = ref<number>();
    const num2 = ref<number>();

    const sum = computed(() => store.getters.sumNum);

    function handleClick() {
      store.commit("sumNumbers", { num1, num2 });
    }
    return { sum, num1, num2, handleClick };
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
