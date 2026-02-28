<!-- eslint-disable vue/no-template-shadow -->
<template v-if="!showCheckboxes">
  <div class="checkbox-label">
    {{ displayName }}
  </div>
</template>

<script setup lang="ts">
import { getBrowseFolderName, parseBool } from "@/helpers/utils";
import {
  MediaType,
  type BrowseFolder,
  type MediaItemType,
} from "@/plugins/api/interfaces";

// properties
export interface Props {
  displayName: string;
}

const compProps = withDefaults(defineProps<Props>(), {
  displayName: "",
});
</script>

<style scoped>
.checkbox {
  position: relative;
  height: 1em;
  margin-top: 1.5em;
  align-content: center;
}

.checkbox-label {
  font-weight: 500;
}

.unavailable {
  opacity: 0.3;
}

.dimmed {
  opacity: 0.3;
}

.hidden {
  opacity: 0;
}

.hiresicon {
  margin-top: 5px;
  margin-right: 15px;
  margin-left: 15px;
  filter: invert(100%);
}

.hiresicondark {
  margin-top: 5px;
  margin-right: 15px;
  margin-left: 15px;
}
</style>
