<template>
	<v-app style="background: #f9f9f9">
		<v-container>
			<v-card>
				<v-card-title :style="{ color: this.$vuetify.theme.themes.light.primary }">1. Add Vehicles</v-card-title>
				<v-tabs grow>
					<v-tab>Single Vin</v-tab>
					<v-tab>Bulk Vin</v-tab>
					<v-tab>Manual Entry</v-tab>
				</v-tabs>
			</v-card>
		</v-container>
	</v-app>
</template>

<script lang="ts">
	import Vue from 'vue';

	export default Vue.extend({
		name: 'App',
		components: {},
		data: () => ({
			//
		}),
	});
</script>
