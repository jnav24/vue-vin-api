<template>
	<v-app style="background: #f9f9f9">
		<v-container>
			<v-card>
				<v-card-title
					:style="{ color: $vuetify.theme.themes.light.primary }"
				>
					1. Add Vehicles
				</v-card-title>
				<v-tabs grow v-model="currentTab">
					<v-tab
						:disabled="setValue(tab) !== currentTab"
						:href="'#' + setValue(tab)"
						:key="tab"
						v-for="tab in tabs"
					>
						{{ tab }}
					</v-tab>
				</v-tabs>
				<v-tabs-items v-model="currentTab">
					<v-tab-item value="single-vin"><SingleVin></SingleVin></v-tab-item>
				</v-tabs-items>
			</v-card>
		</v-container>
	</v-app>
</template>

<script lang="ts">
	import Vue from 'vue';
	import SingleVin from '@/components/SingleVin.vue';

	export default Vue.extend({
		name: 'App',
		components: { SingleVin },
		data: () => ({
			currentTab: 'single-vin',
			tabs: ['Single Vin', 'Bulk Vin', 'Manual Entry'],
		}),
		methods: {
			setValue(tab: string) {
				return tab.toLowerCase().replace(/\s+/, '-');
			},
		},
	});
</script>
