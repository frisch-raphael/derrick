<script lang="ts" src="./TheDrawer.ts"></script>

<template>
  <q-scroll-area class="fit">
    <q-list class="q-my-md">
      <q-item v-if="isUserAdmin()">
        <q-btn-group rounded class="absolute-center q-ma-xs">
          <q-btn
            :color="storedcontext === 'engagement' ? 'primary' : undefined"
            :data-cy="DataTest.DrawerReportBtn"
            rounded
            icon="mdi-file-outline"
            @click="switchDrawerContext('engagement')"
          >
            Report
          </q-btn>
          <q-btn
            :data-cy="DataTest.DrawerAdminBtn"
            :color="storedcontext === 'admin' ? 'primary' : undefined"
            rounded
            icon="mdi-shield-crown-outline"
            @click="switchDrawerContext('admin')"
            >Admin</q-btn
          >
        </q-btn-group>
      </q-item>
      <q-separator v-if="isUserAdmin()" class="q-my-md"></q-separator>
      <template v-for="(menuItem, index) in currentMenu" :key="index">
        <q-item
          v-if="menuItem.name"
          v-ripple
          clickable
          transition-hide="slide-left"
          :active="menuItem.name === 'Outbox'"
        >
          <q-item-section v-if="menuItem.icon" avatar>
            <q-icon color="secondary" :name="menuItem.icon" />
          </q-item-section>
          <q-item-section
            v-if="menuItem.name"
            :data-cy="menuItem.name"
            :class="getDrawerTitleClasses(menuItem.isTitle)"
          >
            <router-link
              v-if="menuItem.goto"
              style="text-decoration: none; color: inherit"
              :to="{ name: menuItem.goto }"
            >
              {{ menuItem.name }}
            </router-link>
            <span v-else>{{ menuItem.name }}</span>
          </q-item-section>
        </q-item>
        <q-separator v-if="menuItem.isSeparator" :key="'sep' + index" />
      </template>
    </q-list>
  </q-scroll-area>
</template>

<style>
.fade-in-enter-active {
  transition: all 0.5s ease;
}

.fade-in-leave-active {
  transition: all 0.5s ease;
}

.fade-in-enter,
.fade-in-leave-to {
  position: absolute; /* add for smooth transition between elements */
  opacity: 0;
}
</style>
