<template>
  <section :class="cn(props.class)">
    <div class="mockup-code space-y-6">
      <div>
        <pre
          data-prefix=">"
          class="mb-4"
          v-text="'Page meta'"
        />

        <pre
          :data-prefix="index + 1"
          v-for="([key, value], index) in metaStruct"
          :key="key"
          class="whitespace-nowrap grid grid-cols-[calc(2rem+2ch)_200px_auto]"
        >
          <code class="text-success" v-text="key"/>         
          <code class="text-warning" v-text="mapRouteConfigValueDisplay(value)" />
        </pre>
      </div>
      <div>
        <pre
          data-prefix=">"
          v-text="'Page route name'"
        />
        <pre
          data-prefix=">"
          class="text-success"
          v-text="route.name"
        />
      </div>
      <div>
        <pre
          data-prefix=">"
          v-text="'Page route path'"
        />
        <pre
          data-prefix=">"
          class="whitespace-nowrap text-success"
          v-text="route.path"
        />
      </div>
      <div>
        <pre
          data-prefix=">"
          class="mb-4"
          v-text="'Page params'"
        />

        <pre
          :data-prefix="index + 1"
          v-for="([key, value], index) in paramsStruct"
          :key="key"
          class="whitespace-nowrap grid grid-cols-[calc(2rem+2ch)_100px_auto]"
        >
          <code class="text-success" v-text="key"/>         
          <code class="text-warning" v-text="mapRouteConfigValueDisplay(value)" />
        </pre>
      </div>
      <div>
        <pre
          data-prefix=">"
          class="mb-4"
          v-text="'Page query'"
        />

        <pre
          :data-prefix="index + 1"
          v-for="([key, value], index) in queryStruct"
          :key="key"
          class="whitespace-nowrap grid grid-cols-[calc(2rem+2ch)_100px_auto]"
        >
          <code class="text-success" v-text="key"/>         
          <code class="text-warning" v-text="mapRouteConfigValueDisplay(value)" />
        </pre>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { type HTMLAttributes, computed } from 'vue'
import { cn } from '@/libs/class-name'
import { useRoute } from 'vue-router'

const props = defineProps<{
  class?: HTMLAttributes['class']
}>()

const route = useRoute()

const metaStruct = computed(() => Object.entries(route.meta))
const paramsStruct = computed(() => Object.entries(route.params))
const queryStruct = computed(() => Object.entries(route.query))

const mapRouteConfigValueDisplay = (value: unknown) => {
  if (typeof value === 'string') {
    return `"${value}"`
  }

  return value
}
</script>
