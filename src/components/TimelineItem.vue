<script setup>
import { 
  isActivityValid, 
  isNull, 
  isTimelineItemValid , 
  validateActivities, 
  validateSelectOptions
} from '../validators';
import BaseSelect from './BaseSelect.vue'
import TimelineHour from './TimelineHour.vue'

const props = defineProps({
    timelineItem: {
      required: true,
      type: Object,
      validator: isTimelineItemValid
    },
    activities: {
      required: true,
      type: Array,
      validator: validateActivities
    },
    activitySelectOptions: {
      required: true,
      type: Array,
      validator: validateSelectOptions
    }

  })
const emit = defineEmits({
  selectActivity(activity){
   return isNull(activity) || isActivityValid(activity)
  } 
})  
function selectActivity(id){
  emit('selectActivity',
  props.activities.find((activity) => activity.id === id) || null)
}
</script>

<template>
  <li 
    class="relative flex flex-col gap-2 border-t border-gray-200 py-10 px-4"
    >
    <TimelineHour :hour="timelineItem.hour" />
  
    <BaseSelect 
      :selected="timelineItem.activityId" 
      :options="activitySelectOptions" 
      placeholder="Rest"
      @select="selectActivity"  
    />
</li>
</template>