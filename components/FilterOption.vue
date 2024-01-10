<script lang="ts" setup>
import { Gender, Length, Popularity } from "~/data";

interface OptionProps {
  option: {
    title: string;
    category: keyof {
      gender: Gender;
      popularity: Popularity;
      length: Length;
    };
    buttons: Gender[] | Popularity[] | Length[];
  };
  options: {
    gender: Gender;
    popularity: Popularity;
    length: Length;
  };
}

const props = defineProps<OptionProps>();
</script>

<template>
  <div class="options-box">
    <h4>{{ option.title }}</h4>
    <div class="options-box--buttons">
      <button
        v-for="value in option.buttons"
        :key="value"
        :class="options[option.category] === value && 'active'"
        @click="
          // @ts-ignore
          options[option.category] = value
        "
      >
        {{ value }}
      </button>
    </div>
  </div>
</template>

<style scoped>
.options-box {
  margin-bottom: 2rem;
}

.options-box--buttons button:first-child {
  border-radius: 1rem 0 0 1rem;
}

.options-box--buttons button:last-child {
  border-radius: 0 1rem 1rem 0;
}

.options-box--buttons button {
  background-color: white;
  outline: 0.15rem solid rgb(249, 87, 89);
  border: none;
  padding: 0.75rem;
  width: 12rem;
  font-size: 1rem;
  color: rgb(27, 60, 138);
  cursor: pointer;
  font-weight: 200;
}

.options-box--buttons button.active {
  background-color: rgb(249, 87, 89);
  color: white;
}
</style>
