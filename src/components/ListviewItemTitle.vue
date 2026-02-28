<!-- eslint-disable vue/no-template-shadow -->
<template v-if="!showCheckboxes">
  <span v-if="item.media_type == MediaType.FOLDER">
    <span>{{ getBrowseFolderName(item as BrowseFolder, t) }}</span>
  </span>
  <div class="checkbox-label">
    {{ displayName }}
    <span v-if="'version' in item && item.version"> ({{ item.version }}) </span>
    <span
      v-if="item.media_type == MediaType.TRACK && item.metadata?.release_date"
    >
      ({{ new Date(item.metadata.release_date).getFullYear() }})</span
    >
  </div>
  <!-- explicit icon -->
  <v-tooltip v-if="item && item.metadata" location="bottom">
    <template #activator="{ props }">
      <v-icon
        v-if="parseBool(item.metadata.explicit || false)"
        v-bind="props"
        icon="mdi-alpha-e-box"
        width="35"
      />
    </template>
    <span>{{ $t("tooltip.explicit") }}</span>
  </v-tooltip>
</template>

<script setup lang="ts">
import { getBrowseFolderName, parseBool } from "@/helpers/utils";
import {
  MediaType,
  type BrowseFolder,
  type MediaItemType,
} from "@/plugins/api/interfaces";
import { useI18n } from "vue-i18n";

// properties
export interface Props {
  displayName: string;
  item: MediaItemType;
}

// global refs
const { t } = useI18n();

const compProps = withDefaults(defineProps<Props>(), {
  displayName: "",
});
</script>

<style scoped>
.checkbox-label {
  font-weight: 500;
}
</style>
