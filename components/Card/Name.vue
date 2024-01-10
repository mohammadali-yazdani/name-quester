<script lang="ts" setup>
interface NameProps {
  name: string;
  index: number;
}

const props = defineProps<NameProps>();

const emit = defineEmits(["remove"]);

const removeName = () => {
  emit("remove", props.index);
};
</script>

<template>
  <div class="cards-box">
    {{ name }}
    <p @click="removeName">×</p>
  </div>
</template>

<style scoped>
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
