<template>
  <div class="relative inline-flex" v-click-outside="() => {dropdownOpen = false}">
    <button
      ref="trigger"
      class="w-8 h-8 flex items-center justify-center bg-gray-100 hover:bg-gray-200 transition duration-150 rounded-full"
      :class="{ 'bg-gray-200': dropdownOpen }"
      aria-haspopup="true"
      @click.prevent="dropdownOpen = !dropdownOpen"
      :aria-expanded="dropdownOpen"
    >
      <span class="sr-only">Notifications</span>
      <svg class="w-4 h-4" viewBox="0 0 16 16" xmlns="http://www.w3.org/2000/svg">
        <path class="fill-current text-gray-500" d="M6.5 0C2.91 0 0 2.462 0 5.5c0 1.075.37 2.074 1 2.922V12l2.699-1.542A7.454 7.454 0 006.5 11c3.59 0 6.5-2.462 6.5-5.5S10.09 0 6.5 0z" />
        <path class="fill-current text-gray-400" d="M16 9.5c0-.987-.429-1.897-1.147-2.639C14.124 10.348 10.66 13 6.5 13c-.103 0-.202-.018-.305-.021C7.231 13.617 8.556 14 10 14c.449 0 .886-.04 1.307-.11L15 16v-4h-.012C15.627 11.285 16 10.425 16 9.5z" />
      </svg>
      <div v-if="notifications.length" class="absolute top-0 right-0 w-2.5 h-2.5 bg-red-500 border-2 border-white rounded-full" />
    </button>
    <transition
      enter-active-class="transition ease-out duration-200 transform"
      enter-from-class="opacity-0 -translate-y-2"
      enter-to-class="opacity-100 translate-y-0"
      leave-active-class="transition ease-out duration-200"
      leave-from-class="opacity-100"
      leave-to-class="opacity-0"
    >
      <div v-show="dropdownOpen" class="origin-top-right z-10 absolute top-full -mr-48 sm:mr-0 min-w-80 bg-white border border-gray-200 py-1.5 rounded shadow-lg overflow-hidden mt-1" :class="align === 'right' ? 'right-0' : 'left-0'">
        <div class="text-xs font-semibold text-gray-400 uppercase pt-1.5 pb-2 px-4">Уведомления</div>
        <ul
          ref="dropdown"
          @focusin="dropdownOpen = true"
          @focusout="dropdownOpen = false"
        >
<!--          <li class="border-b border-gray-200 last:border-0">
            <router-link class="block py-2 px-4 hover:bg-gray-50" to="#0" @click="dropdownOpen = false">
              <span class="block text-sm mb-2">📣 <span class="font-medium text-gray-800">Новое уведомление</span> Сегодня 8 именинников.</span>
              <span class="block text-xs font-medium text-gray-400">20 июня 2022</span>
            </router-link>
          </li>-->
          <li class="border-b border-gray-200 last:border-0" v-if="!notifications.length">
            <div class="block py-2 px-4" @click="dropdownOpen = false">
              <span class="block text-sm mb-2 text-center">
                <span class="text-gray-800">Нет уведомлений</span>
              </span>
            </div>
          </li>
        </ul>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: 'DropdownNotifications',
  props: ['align'],
  data: () => ({
    dropdownOpen: false,
    notifications: [],
  }),
}
</script>
