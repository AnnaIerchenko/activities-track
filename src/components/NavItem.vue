<script>
  export default {
    //attr inherit by tag <a></a>, not root one
    inheritAttrs: false
  }
</script>
<template>
  <li  class="flex-1" >
    <a v-bind="$attrs" class="flex items-center flex-col p-2 text-xs capitalize">
     <slot></slot>
      <!-- <ClockIcon v-if="page ==='timeline'" class="h-6 w-6"/>
      <ListBulletIcon v-else-if="page === 'activities'" class="h-6 w-6"/>
      <ChartBarIcon v-else class="h-6 w-6"/>{{ page }} -->
    </a>
  </li> 
</template>