<template>
  <button @click="$emit('open')" class="add-btn">
    <span class="add-btn-span">+</span>
    Новий контакт
  </button>
</template>

<script>
export default {
  name: "AddContactItem",
};
</script>

<style lang="css" scoped>
.add-btn {
  display: flex;
  align-items: center;
  gap: 10px;
  color: green;
  background: none;
  border: none;
  cursor: pointer;
  font-weight: 700;
  font-size: 18px;
  margin-left: -5px;
}
.add-btn-span {
  padding: 10px 15px;
  border-radius: 50%;
  border: 1px dashed green;
}
</style>