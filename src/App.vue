<template>
  <div class="layout">
    <aside></aside>
    <nav>
      <MenuItem v-for="section in menuSections" :section="section" />
    </nav>
    <main>
      <Tooltip v-for="index in 300"/>
    </main>
  </div>
</template>

<script setup>
import MenuItem from "./components/MenuItem.vue";
import Tooltip from "./components/Tooltip.vue";

const menuSections = [
  {
    id: 'dashboard-menu',
    title: 'Dashboard'
  },
  {
    id: 'spaces-menu',
    title: 'Spaces'
  },
  {
    id: 'tiles-menu',
    title: 'Tiles'
  },
  {
    id: 'collections-menu',
    title: 'Collections'
  },
  {
    id: 'users-menu',
    title: 'Users'
  },
  {
    id: 'audiences-menu',
    title: 'Audiences'
  },
  {
    id: 'comms-menu',
    title: 'Comms'
  },
  {
    id: 'reports-menu',
    title: 'Reports'
  },
  {
    id: 'more-menu',
    title: 'More',
    subcategories: [
      {
        id: 'menu-1',
        title: 'Settings'
      },
      {
        id: 'menu-2',
        title: 'Organisations'
      },
      {
        id: 'menu-3',
        title: 'More 3'
      }
    ]
  }
]
</script>

<style scoped>
.layout {
  display: grid;
  width: 100%;
  min-height: 100vh;
  grid-template-columns: 200px 1fr;
  grid-template-rows: 100px 1fr;
  grid-template-areas:
    "aside nav"
    "aside main";


  > aside {
    background: #8e8e8e;
    grid-area: aside;
  }

  > nav {
    background: #181818;
    grid-area: nav;
    display: flex;
  }

  > main {
    background: #484848;
    grid-area: main;
    color: #FFF;
    padding: 50px;
    display: flex;
    gap: 80px;
    flex-wrap: wrap;
    justify-content: start;
    align-content: flex-start;
  }

}


</style>
