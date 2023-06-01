<script setup>
import { PlusIcon } from '@heroicons/vue/24/outline';
import BaseButton from './BaseButton.vue';
import { isActivityValid } from '../validators';
import { nextTick, ref } from 'vue';

const emit = defineEmits({
  submit: isActivityValid,
  
})

const activity = ref('')

async function submit(){
  emit('submit', activity.value)
  activity.value = ''

  //return promise, all function inside will work after update DOM
  await nextTick()
    window.scrollTo(0, document.body.scrollHeight)

} 
</script>

<template>     
    <form 
      @submit.prevent="submit"
      class="sticky bottom-[57px] flex gap-2 border-t bg-white p-4">
      <input 
        type="text" 
        placeholder="activity name"
        v-model="activity"
        class="w-full rounded border px-4 text-xl"
        >
      <BaseButton :disabled="activity.trim() === ''">
        <PlusIcon class="h-8"/>
      </BaseButton>
    </form>
</template>