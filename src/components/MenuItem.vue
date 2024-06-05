<template>
  <div class="menu-item"
       @mouseenter="openDropdown"
       @mouseleave="closeDropdown"
       @click.prevent>

    <button :popovertarget="section.id"
            :style="`anchor-name: --${section.id}`">
      {{ section.title }}
    </button>

    <div :id="section.id" popover class="menu-item-dropdown" ref="menuEl">
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

const dropdownStyles = computed(() => {
  return {
    positionAnchor: `--${props.section.id}`,
    left: `anchor(--${props.section.id} left)`,
    right: `anchor(--${props.section.id} right)`,
    top: `anchor(--${props.section.id} top)`,
    bottom: `calc(10px + anchor(--${props.section.id} bottom))`
  }
})
</script>

<style scoped>

.menu-item {
  > button {
    height: 100%;
    padding: 0 50px;
    position: relative;

    &:has(+ :popover-open) {
      &:before {
        content: '';
        position: absolute;
        width: 0;
        height: 0;
        border-left: 15px solid transparent;
        border-right: 15px solid transparent;
        border-bottom: 15px solid white;
        top: 100%;
        left: 50%;
        transform: translateX(-50%);
      }
    }
  }
}

.menu-item-dropdown {
  position: absolute;
  margin: 0;
  width: 600px;
  left: v-bind(dropdownStyles.left);
  top: v-bind(dropdownStyles.bottom);
  position-try-options: --menu-right;
  transition: all 0.25s;
  padding: 30px;
  border-radius: 15px;
  border: none;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);

  &:has(ul) {
    width: 260px;
  }

  ul {
    list-style: none;
    padding: 0;
    margin: 40px 0 0;
  }
}

@position-try --menu-right {
  left: auto;
  right: v-bind(dropdownStyles.right);
  top: v-bind(dropdownStyles.bottom);
}

</style>