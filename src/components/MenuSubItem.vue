<template>
  <li class="submenu-item"
      @mouseenter="openDropdown"
      @mouseleave="closeDropdown">

    <button :popovertarget="`${section.id}-${subcategory.id}`"
            :style="`anchor-name: --${section.id}-${subcategory.id}`">
      {{ subcategory.title }}
    </button>

    <div :id="`${section.id}-${subcategory.id}`"
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

const dropdownStyles = computed(() => {
  const id = `${props.section.id}-${props.subcategory.id}`
  return {
    positionAnchor: `--${id}`,
    left: `calc(20px + anchor(--${id} left))`,
    right: `calc(20px + anchor(--${id} right))`,
    top: `anchor(--${id} top)`
  }
})

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
  transition: all 0.25s;
  padding: 30px;
  left: v-bind(dropdownStyles.right);
  top: v-bind(dropdownStyles.top);
  position-try-options: --submenu-right;
  border-radius: 15px;
  border: none;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
}


@position-try --submenu-right {
  left: auto;
  right: v-bind(dropdownStyles.left);
  top: v-bind(dropdownStyles.top);
}
</style>