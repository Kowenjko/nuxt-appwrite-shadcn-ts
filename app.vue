<script setup lang="ts">
const route = useRoute()

watch(
	() => route.name,
	(name) => useSeoMeta({ title: `CRM - ${name !== 'index' ? name : 'home'} ` })
)

useSeoMeta({ title: `CRM - home ` })
</script>
<template>
	<suspense>
		<nuxt-layout>
			<nuxt-page />
		</nuxt-layout>
	</suspense>
</template>
