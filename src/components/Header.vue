<template>
  <header>
    <h2 class="title">{{ wordValue ? wordValue : "Word Hunt" }}</h2>
    <div class="input-wrap">
      <input type="text" placeholder="Search a Word" v-model="wordValue" @input="debouncedHandleInput" />
    </div>
  </header>
</template>

<script setup lang="ts">
import { ref, defineEmits } from "vue";

// 防抖函数定义
function debounce<T extends (...args: any[]) => any>(func: T, wait: number): T {
  let timeoutId: ReturnType<typeof setTimeout>;
  return ((...args: Parameters<T>) => {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => func(...args), wait);
  }) as T;
}

const emit = defineEmits(['update:modelValue']);
const wordValue = ref<HTMLInputElement | null>(null);

// 处理 input 事件的方法
const handleInput = (event: Event) => {
  const value = (event.target as HTMLInputElement).value;
  emit('update:modelValue', value);
};

// 使用防抖函数
const debouncedHandleInput = debounce(handleInput, 500);

</script>

<style lang="less" scoped>
@media (max-width: 1000px) {
  h2 {
    font-size: 11vw;
  }
}

header {
  height: 30vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
  position: sticky;

  h2 {
    font-size: 7vw;
    font-weight: 100;
    margin: 0;
  }

  .input-wrap {
    input {
      width: 50vw;
      border: none;
      background-color: #282c34;
      border-bottom: 1px solid rgba(197, 188, 188, 1);
      padding: 5px;
      color: white;
      font-size: 18px;

      &:focus {
        outline: none;
        border-bottom: 1px solid white;
      }

      &::placeholder {
        color: rgba(255, 255, 255, 0.6);
      }
    }
  }
}
</style>