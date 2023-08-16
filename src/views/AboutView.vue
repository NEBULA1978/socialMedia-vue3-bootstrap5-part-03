<template>
	<div class="about">
		<h1>This is the About View</h1>
		<CenaVisigodo />
	</div>
</template>

<script>
import CenaVisigodo from '@/components/CenaVisigodo.vue';

export default {
	name: 'AboutView',
	components: {
		CenaVisigodo,
	},
};
</script>


<style scoped>
	.about {
		min-height: 60vh;
		max-width: 895px;
		margin: auto;
	}
</style>
