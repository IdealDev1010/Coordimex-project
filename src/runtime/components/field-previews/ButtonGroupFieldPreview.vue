<template>
  <PruviousStringFieldPreview
    :canUpdate="canUpdate"
    :name="name"
    :options="options"
    :value="displayed"
    @refresh="$emit('refresh')"
  />
</template>

<script lang="ts" setup>
import { ref, watch, type PropType } from '#imports'
import type { FieldOptions } from '#pruvious'
import { __, loadTranslatableStrings } from '../../composables/translatable-strings'

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  value: {
    type: String,
  },
  options: {
    type: Object as PropType<FieldOptions['button-group']>,
    required: true,
  },
  canUpdate: {
    type: Boolean,
    default: false,
  },
  record: {
    type: Object as PropType<Record<string, any>>,
  },
  language: {
    type: String,
  },
})

defineEmits<{
  refresh: []
}>()

const displayed = ref('')

watch(
  () => props.value,
  () => {
    displayed.value = props.value ? __('pruvious-dashboard', props.options.choices[props.value] as any) : ''
  },
  { immediate: true },
)

await loadTranslatableStrings('pruvious-dashboard')
</script>
