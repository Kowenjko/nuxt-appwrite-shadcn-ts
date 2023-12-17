<script setup lang="ts">
import { cn } from '@/lib/utils'

const props = defineProps({
	class: {
		type: String,
		default: '',
	},
})
</script>

<template>
	<div
		:class="
			cn('rounded-lg  bg-[#273445] text-card-foreground shadow', props.class)
		"
	>
		<slot />
	</div>
</template>
