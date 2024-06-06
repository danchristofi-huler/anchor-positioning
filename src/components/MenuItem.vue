<template>
  <div class="menu-item"
       @mouseenter="openDropdown"
       @mouseleave="closeDropdown"
       @click.prevent>

    <button :style="`anchor-name: --${section.id}`">
      {{ section.title }}
    </button>

    <div popover class="menu-item-dropdown" ref="menuEl" :style="`position-anchor: --${props.section.id}`">
      <span>{{ section.title }}</span>
      <ul v-if="section.subcategories">
        <MenuSubItem v-for="subcategory in section.subcategories" :section="section" :subcategory="subcategory" />
      </ul>
    </div>

  </div>
</template>

<script setup>
import {computed, ref} from "vue";
import MenuSubItem from "./MenuSubItem.vue";

const props = defineProps({
  section: Object
})

const menuEl = ref(null)

const openDropdown = () => {
  menuEl.value.showPopover()
}

const closeDropdown = () => {
  // menuEl.value.hidePopover()
}

</script>

<style scoped>

.menu-item {
  > button {
    height: 100%;
    padding: 0 50px;
    position: relative;
  }
}

.menu-item-dropdown {
  position: absolute;
  margin: 0;
  width: 600px;
  inset-area: bottom span-right;
  position-try-options: flip-block, flip-inline, flip-block flip-inline;
  padding: 30px;
  border-radius: 15px;
  border: none;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
  transition:
      opacity .2s ease-in,
      display .2s ease-in;
  transition-behavior: allow-discrete;

  &:not(:popover-open) {
    opacity: 0;
  }

  @starting-style {
    opacity: 0;
  }

  &:has(ul) {
    width: 260px;
  }

  ul {
    list-style: none;
    padding: 0;
    margin: 40px 0 0;
  }
}


</style>