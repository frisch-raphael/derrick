<script lang="ts" setup>
import { DataTest } from 'src/enums/enums';
import { useSlots } from 'vue';
const slots = useSlots();
interface Props {
  title: string;
  actionsAlign?: 'center' | 'left' | 'right' | 'between' | 'around' | 'evenly' | 'stretch' | undefined;
}
const props = withDefaults(defineProps<Props>(), { actionsAlign: 'center' });
</script>

<template>
  <q-dialog :data-cy="DataTest.DialogBase">
    <q-card :data-cy="DataTest.DialogBaseCard" style="width: 800px; max-width: 100vw">
      <q-linear-progress></q-linear-progress>
      <q-card-section>
        <div class="text-h6 row">
          {{ title }}
          <q-space></q-space>
          <q-btn
            v-close-popup
            :data-cy="DataTest.DialogBaseClose"
            icon="mdi-close-circle"
            color="red-10"
            flat
          >
          </q-btn>
        </div>
      </q-card-section>

      <q-card-section class="q-pt-none">
        <slot></slot>
      </q-card-section>
      <q-card-actions v-if="slots.actions" :align="props.actionsAlign">
        <slot name="actions"></slot>
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>
