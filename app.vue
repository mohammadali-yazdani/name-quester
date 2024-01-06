<script lang="ts" setup>
import { Gender, Length, names, Popularity } from "~/data";

interface OptionsState {
  gender: Gender;
  popularity: Popularity;
  length: Length;
}

const options = reactive<OptionsState>({
  gender: Gender.GIRL,
  length: Length.ALL,
  popularity: Popularity.TRENDY,
});

const computeSelectedNames = () => {
  const filteredNames = names
    .filter((name) => name.gender === options.gender)
    .filter((name) => name.popularity === options.popularity)
    .filter((name) => {
      if (options.length === Length.ALL) return true; // For All
      else return name.length === options.length;
    });

  selectedNames.value = filteredNames.map((name) => name.name);
};

const selectedNames = ref<string[]>([]);
</script>

<template>
  <div class="container">
    <h1>Name Generator</h1>
    <p>Choose your options and click the "Find Names" button below</p>
    <div class="options">
      <div class="options-box">
        <h4>1) Choose a gender</h4>
        <div class="options-box--buttons">
          <button
            :class="options.gender === Gender.BOY && 'active'"
            @click="options.gender = Gender.BOY"
          >
            Boy
          </button>
          <button
            :class="options.gender === Gender.UNISEX && 'active'"
            @click="options.gender = Gender.UNISEX"
          >
            Unisex
          </button>
          <button
            :class="options.gender === Gender.GIRL && 'active'"
            @click="options.gender = Gender.GIRL"
          >
            Girl
          </button>
        </div>
      </div>
      <div class="options-box">
        <h4>2) Choose the name's popularity</h4>
        <div class="options-box--buttons">
          <button
            :class="options.popularity === Popularity.TRENDY && 'active'"
            @click="options.popularity = Popularity.TRENDY"
          >
            Trendy
          </button>
          <button
            :class="options.popularity === Popularity.UNIQUE && 'active'"
            @click="options.popularity = Popularity.UNIQUE"
          >
            Unique
          </button>
        </div>
      </div>
      <div class="options-box">
        <h4>3) Choose name's length</h4>
        <div class="options-box--buttons">
          <button
            :class="options.length === Length.LONG && 'active'"
            @click="options.length = Length.LONG"
          >
            Long
          </button>
          <button
            :class="options.length === Length.ALL && 'active'"
            @click="options.length = Length.ALL"
          >
            All
          </button>
          <button
            :class="options.length === Length.SHORT && 'active'"
            @click="options.length = Length.SHORT"
          >
            Short
          </button>
        </div>
      </div>

      <button class="primary" @click="computeSelectedNames">Find Names</button>
    </div>

    <div class="cards">
      <div v-for="name in selectedNames" :key="name" class="cards-box">
        {{ name }}
        <p>×</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
}

h1 {
  font-size: 3rem;
}

.options {
  background-color: rgb(255, 238, 236);
  border-radius: 2rem;
  padding: 1rem;
  width: 95%;
  margin: 0 auto;
  margin-top: 4rem;
  position: relative;
}

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

.options button.primary {
  background-color: rgb(249, 87, 89);
  color: white;
  border-radius: 6.5rem;
  border: none;
  padding: 0.7rem 4rem;
  font-size: 1rem;
  margin-top: 1rem;
  cursor: pointer;
}

.cards {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  margin-top: 3rem;
}

.cards-box {
  position: relative;
  background-color: rgb(27, 61, 138);
  color: white;
  border-radius: 1rem;
  padding: 1rem;
  margin-right: 0.5rem;
  margin-bottom: 1rem;
}

.cards-box p {
  position: absolute;
  top: -30%;
  left: 92.5%;
  cursor: pointer;
  color: rgba(255, 255, 255, 0.178);
}
</style>
