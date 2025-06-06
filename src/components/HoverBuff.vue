<script setup lang="ts">
import type { ImageMetadata } from 'astro'
import type { HTMLAttributes } from 'vue'

import type { VariantType } from '@/lib/variant'

import Buff from '@/components/Buff.vue'
import { HoverCard, HoverCardContent, HoverCardTrigger } from '@/components/shadcn-vue/hover-card'
import Span from '@/components/Span.vue'

const props = defineProps<{
  icon: ImageMetadata
  name: string
  nameVariant: VariantType
  description: string
  tag?: string
  class?: HTMLAttributes['class']
}>()
</script>

<template>
  <HoverCard>
    <HoverCardTrigger as-child>
      <Buff :icon="icon" :name="name" :description="description" :tag="tag" :class="props.class">
        <slot name="icon">
          <img :src="icon.src" :alt="description">
        </slot>
      </Buff>
    </HoverCardTrigger>
    <HoverCardContent class="w-auto max-w-150">
      <div class="space-y-2">
        <h4 class="flex items-center gap-2 text-lg font-semibold">
          <Buff :icon="icon" :name="name" :description="description">
            <slot name="icon">
              <img :src="icon.src" :alt="description">
            </slot>
          </Buff>
          <Span :variant="nameVariant">{{ name }}</Span>
        </h4>
        <slot>
          <p>
            {{ description }}
          </p>
        </slot>
      </div>
    </HoverCardContent>
  </HoverCard>
</template>
