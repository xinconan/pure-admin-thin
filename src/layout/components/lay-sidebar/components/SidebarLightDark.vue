<script setup lang="ts">
import { ref, watch } from "vue";
import DayIcon from "~icons/ri/sun-fill";
import DarkIcon from "~icons/ri/moon-fill";
import { useDark } from "@pureadmin/utils";
import { useDataThemeChange } from "@/layout/hooks/useDataThemeChange";

const screenIcon = ref();
const { isDark } = useDark();
const { dataThemeChange, overallStyle, dataTheme } = useDataThemeChange();

function toggle() {
  const mode = isDark.value ? "light" : "dark";
  dataTheme.value = !isDark.value;
  overallStyle.value = mode;
  dataThemeChange(mode);
}

watch(
  isDark,
  dark => {
    screenIcon.value = dark ? DayIcon : DarkIcon;
  },
  {
    immediate: true
  }
);
</script>

<template>
  <span class="fullscreen-icon navbar-bg-hover" @click="toggle">
    <IconifyIconOffline :icon="screenIcon" />
  </span>
</template>
