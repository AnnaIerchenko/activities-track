<script setup>
  import { computed, ref } from 'vue';
  import TheHeader from './components/TheHeader.vue'
  import TheNav from './components/TheNav.vue'
  import TheTimeline from './pages/TheTimeline.vue'
  import TheActivities from './pages/TheActivities.vue'
  import TheProgress from './pages/TheProgress.vue'
  import { PAGE_ACTIVITIES, PAGE_PROGRESS, PAGE_TIMELINE } from './constants'
  import {
    normalizePageHash, 
    generateTimelineItems, 
    generateActivitySelectOptions, 
    generateActivities
  } 
  from './functions'

const currentPage = ref(normalizePageHash())

const activities = ref(generateActivities())
//for generate options in drop-down list , after changing
const activitySelectOptions = computed(() => generateActivitySelectOptions(activities.value))

const timelineItems = ref(generateTimelineItems())
function goTo(page){
  currentPage.value = page
}

function createActivity(activity){
  activities.value.push(activity)
}

function deleteActivity(activity){
  timelineItems.value.forEach((timelineItem) => {
    if(timelineItem.activityId === activity.id){
      timelineItem.activityId = null
    }
  })
  activities.value.splice(activities.value.indexOf(activity), 1)
}

function setTimelineItemActivity({timelineItem, activity}){
  timelineItem.activityId = activity?.id || null
}
</script>

<template>
 <TheHeader @navigate="goTo($event)" />

  <main class="flex flex-grow flex-col">
  <TheTimeline 
    v-show="currentPage === PAGE_TIMELINE" 
    :timeline-items="timelineItems"
    :activities="activities"
    :activity-select-options="activitySelectOptions"
    @set-timeline-item-activity="setTimelineItemActivity"
    />
  <TheActivities 
    v-show="currentPage === PAGE_ACTIVITIES" 
    :activities="activities"
    @create-activity="createActivity"
    @delete-activity="deleteActivity"  
  />
  <TheProgress v-show="currentPage === PAGE_PROGRESS" />
  </main>

  <TheNav :current-page="currentPage" @navigate="goTo($event)" />
</template>

<style scoped>

</style>
