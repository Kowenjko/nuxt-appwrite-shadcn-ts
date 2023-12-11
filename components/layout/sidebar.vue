<script setup lang="ts"></script>
<template>
	<div>
		<nuxt-link class="mb-10 block" to="/">
			<nuxt-img class="mx-auto" src="/logo.svg" width="100px" />
		</nuxt-link>
		<LayoutMenu />
		<button
			class="absolute top-2 right-3 transition-colors hover:text-purple-400"
			@click=""
		>
			<Icon name="line-md:logout" />
		</button>
	</div>
</template>

<style scoped></style>
