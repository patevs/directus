<script setup lang="ts">
import { useI18n } from 'vue-i18n';

defineProps<{
	readme: string | null;
}>();

const { t } = useI18n();
</script>

<template>
	<v-notice v-if="!readme" class="notice">{{ t('extension_readme_missing') }}</v-notice>
	<div v-else v-md="{ value: readme, target: '_blank' }" class="readme" />
</template>

<style scoped lang="scss">
@use '@/styles/mixins';

.readme {
	:deep(*) {
		-webkit-user-select: text;
		user-select: text;
	}

	:deep() {
		@include mixins.markdown;
	}

	:deep(* + *) {
		margin-block-start: 1rem;
	}

	:deep(img) {
		border: var(--theme--border-width) solid var(--theme--border-color-subdued);
	}
}

.notice {
	align-self: flex-start;
	margin-block-start: 4px;
}
</style>
