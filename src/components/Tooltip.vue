<template>
  <div class="tooltip">
    <button class="trigger"
            :style="`anchor-name: --${id}`"
            @mouseenter="openTooltip"
            @mouseleave="closeTooltip"
            @click.prevent>i</button>

    <div popover class="content" :style="`position-anchor: --${id}`" ref="contentEl">
     Lorem ipsum dolor sit amet, consectetur adipisicing elit. A adipisci aliquam asperiores at aut beatae corporis, cupiditate ea eaque error hic maxime.
    </div>
  </div>
</template>

<script setup>

import {computed, ref} from "vue";

const id = ref(`tooltip-${Math.random().toString(36).substring(7)}`)

const contentEl = ref(null)

const openTooltip = () => {
  contentEl.value.showPopover()
}

const closeTooltip = () => {
  contentEl.value.hidePopover()
}

</script>

<style scoped>

.trigger {
  width: 20px;
  height: 20px;
  background-color: white;
  border-radius: 100%;
  display: flex;
  color: #000;
  justify-content: center;
  align-items: center;
  margin: 0;
  padding: 0;
  border: none;
  cursor: pointer;

  &:has(+ :popover-open) {
    background-color: #000;
    color: #FFF;
  }
}

.content {
  position: absolute;
  padding: 15px;
  font-size: 14px;
  width: 220px;
  margin: 0;
  border-radius: 12px;
  transition: opacity 0.2s ease-in, display 0.2s ease-in;
  transition-behavior: allow-discrete;
  inset-area: right span-bottom;
  position-try-options: flip-block, flip-inline, flip-block flip-inline;

  &:not(:popover-open) {
    opacity: 0;
  }

  @starting-style {
    opacity: 0;
  }
}



</style>