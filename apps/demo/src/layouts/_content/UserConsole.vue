<template>
  <div :class="cn(hideSidebar ? '' : 'grid grid-cols-[300px_auto]')">
    <aside
      v-if="!hideSidebar"
      class="border-r border-gray-200 p-6"
    >
      <ul class="flex flex-col gap-4">
        <router-link
          v-for="item in sidebarItems"
          :key="item.name"
          v-slot="{ isActive }"
          :to="{ name: item.name }"
        >
          <button :class="cn('btn', isActive ? 'btn-primary' : 'btn-ghost')">
            {{ item.label }}
          </button>
        </router-link>
      </ul>
    </aside>
    <main class="p-6">
      <section>
        <div class="breadcrumbs text-sm">
          <ul>
            <li>
              <router-link :to="{ name: '/(home)/' }">Home</router-link>
            </li>
            <li v-if="currentRoute">
              <router-link :to="{ name: currentRoute.name }">
                {{ currentRoute.label }}
              </router-link>
            </li>
          </ul>
        </div>
      </section>
      <slot />
    </main>
  </div>
</template>
<script lang="ts" setup>
import { computed } from 'vue'
import type { RouteRecordName } from 'vue-router'
import { useRoute } from 'vue-router'

import { cn } from '@libs/helpers/className'

const sidebarItems: Array<{ label: string; name: RouteRecordName }> = [
  { name: '/user-console/resource-overview/', label: 'Resource Overview' },
  { name: '/user-console/bare-metal/', label: 'Bare metal' },
  { name: '/user-console/template/', label: 'Template' },
]

const route = useRoute()

const hideSidebar = computed(() => Boolean(route.meta.hideSidebar))

const currentRoute = computed(() =>
  sidebarItems.find(item => route.name.includes(item.name))
)
</script>
