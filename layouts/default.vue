<script setup lang="ts"></script>
<template>
	<section class="grid grid-cols-[1fr_6fr] min-h-screen">
		<LayoutSidebar class="px-5 py-8 bg-[#1d252b] h-full relative w-full" />
		<div>
			<slot />
		</div>
	</section>
</template>

<style scoped></style>
