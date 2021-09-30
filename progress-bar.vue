<!--
VUE Progress Bar (Not Animated)

Just a lovely, plain progress bar. You can give it whatever colors you want.

The 'min' and 'max' props are optional and will default to 0 and 100 respectively.

The 'progress' prop would be the current value of whatever item the bar signifies.

The 'showPercentage' prop can be set to 'true' to show the percentage value of progress
rounded to two decimal places.
-->

<template>
  <div class="w-full h-4 rounded-full bg-gray-500 relative">
    <div
      class="
        p-2
        h-full
        rounded-md
        bg-gradient-to-r
        from-yellow-300
        via-yellow-500
        to-red-500
      "
      :style="`width: ${((progress - min) * 100) / (max - min)}%`"
    />
    <div
      class="
        absolute
        text-white text-xs
        font-bold
        top-0
        text-center
        w-full
        flex
        items-center
      "
    >
      <span class="mx-auto">{{
        `${Math.round((((progress - min) * 100) / (max - min)) * 100) / 100}%`
      }}</span>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    min: {
      type: Number,
      default() {
        return 0
      },
    },
    max: {
      type: Number,
      default() {
        return 100
      },
    },
    progress: {
      type: Number,
      default() {
        return 1
      },
    },
    showPercentage: {
      type: Boolean,
      default() {
        return false
      },
    },
  },
}
</script>
