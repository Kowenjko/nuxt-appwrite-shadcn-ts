<script lang="ts" setup>
import { MENU } from './menu.data'
const route = useRoute()
</script>

<template>
	<div class="space-y-3">
		<nuxt-link
			:class="[
				'flex items-center gap-3 py-1 px-2  rounded-lg w-full hover:bg-gray-700 hover:shadow transition-all',
				route.path === item.url && 'bg-gray-700 shadow',
			]"
			:to="item.url"
			v-for="item in MENU"
			:key="item.url"
		>
			<Icon :name="item.icon" class="mr-3" />
			<span>{{ item.name }}</span>
		</nuxt-link>
	</div>
</template>
