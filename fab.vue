<!-- 
- Just a copypaste of something I made for a project. 
- Uses tailwindcss and nuxtjs. 
- Should work for vanilla vue too with some tweaks.

You can also use svg icons instead of the unicode + and ×.

The prop 'nav' should be an array of objects with 'name' as text, 
'route' as a url, 'key' as text (replace 'navItem.key' in this 
file with 'navItem.name' or 'navItem.route' if you wish to use 
them instead) and 'routeIcon' as text (you can use svg icons with
v-html tho unicode is preferable).
-->

<!--
The IDs 'fabButton' and 'fabItems' do nothing and you are free to remove them.
-->

<template>
  <div>
    <div class="fixed p-4 bottom-0 right-0 flex flex-col items-center z-40">
      <div
        id="fabItems"
        :class="`transform transition duration-500 ease-in-out ${
          toggleNav ? 'translate-y-0' : 'translate-y-100'
        }`"
      >
        <ul class="p-4 flex-col items-center space-y-10 w-full mx-auto">
          <div v-for="navItem in Navigation" :key="navItem.key">
            <a
              v-tooltip="{
                placement: 'left',
                content: navItem.name,
                trigger: 'hover',
                classes: 'text-white font-bold text-md',
                html: false,
              }"
              :href="navItem.route"
              class="relative p-2 group flex items-center"
            >
              <li
                class="
                  rounded-full
                  flex
                  items-center
                  p-4
                  w-16
                  h-16
                  bg-red-600
                "
              >
                <div class="px-auto flex items-center mx-auto">
                  {{ navItem.routeIcon }}
                </div>
              </li>
            </a>
          </div>
        </ul>
      </div>

      <div
        id="fabButton"
        class="
          rounded-full
          bg-red-500
          flex
          items-center
          w-16
          h-16
          z-50
          bg-opacity-50
          hover:bg-opacity-100
        "
      >
        <button
          :class="`p-4 transform transition duration-500 ease-in-out mx-auto block ${
            toggleNav ? 'rotate-90' : ''
          }`"
          @click="toggleBoth"
        >
          <span v-if="toggleNav">×<span/>
          <span v-else>+<span/>
        </button>
      </div>
    </div>
    <div
      :class="`inset-0 w-full fixed h-full z-30 block bg-gray-800 bg-opacity-30 ${
        toggleNav ? 'visible' : 'invisible'
      }`"
      @click="toggleOff"
    ></div>
  </div>
</template>

<script>
export default {
  props: {
    nav: {
      type: Array,
      default: null,
    },
    FabType: {
      type: String,
      default() {
        return 'main'
      },
    },
  },
  data() {
    return {
      toggleNav: false,
      Navigation: this.nav,
    }
  },
  methods: {
    toggleOff() {
      this.toggleNav = false
    },
    toggleBoth() {
      this.toggleNav = !this.toggleNav
    },
    toggleOn() {
      this.toggleNav = true
    },
  },
}
</script>
