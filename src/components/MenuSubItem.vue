<template>
  <li class="submenu-item"
      @mouseenter="openDropdown"
      @mouseleave="closeDropdown">

    <button :style="`anchor-name: --${section.id}-${subcategory.id}`">
      {{ subcategory.title }}
    </button>

    <div :style="`position-anchor: --${section.id}-${subcategory.id}`"
         popover
         class="submenu-item-dropdown"
         ref="submenuEl">
      <span>{{ subcategory.title }}</span>
    </div>
  </li>
</template>

<script setup>

import {computed, ref} from "vue";

const props = defineProps({
  section: Object,
  subcategory: Object
})

const submenuEl = ref(null)

const openDropdown = () => {
  submenuEl.value.showPopover()
}

const closeDropdown = () => {
  // submenuEl.value.hidePopover()
}

</script>

<style scoped>
li button {
  padding: 20px 0;
  width: 100%;
}

.submenu-item-dropdown {
  position: absolute;
  margin: 0;
  width: 300px;
  padding: 30px;
  inset-area: right span-bottom;
  position-try-options: flip-block, flip-inline, flip-block flip-inline;
  border-radius: 15px;
  border: none;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
}
</style>