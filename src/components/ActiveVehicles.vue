<template>
	<div>
		<p>To make changes to the vehicles below, expand the row of the vehicle you wist to edit.</p>
		<p>ACTIVE VEHICLES: {{ form ? '1' : '0' }}</p>

		<v-expansion-panels v-if="form">
			<v-expansion-panel	>
				<v-expansion-panel-header>
					<v-layout align-center justify-space-between>
						1. {{ form.vin }}
						<v-btn color="primary" text @click.native.stop="handleDelete">Delete</v-btn>
					</v-layout>
				</v-expansion-panel-header>
				<v-expansion-panel-content color="#E3F2FD" style="padding-top: 1em">
					<v-form>
						<v-container>
							<v-row>
								<v-col>
									<v-text-field
										v-model="form.vin"
										label="VIN #"
									></v-text-field>
								</v-col>
								<v-col>
									<v-select
										v-model="form['Model Year']"
										:items="years"
										label="Year"
									></v-select>
								</v-col>
								<v-col>
									<v-text-field
										v-model="form['Make']"
										label="Make"
									></v-text-field>
								</v-col>
							</v-row>
							<v-row>
								<v-col>
									<v-text-field
										v-model="form['Model']"
										label="Model"
									></v-text-field>
								</v-col>
								<v-col></v-col>
								<v-col></v-col>
							</v-row>
							<v-row justify="end">
								<v-btn color="#969696" text>Cancel</v-btn>
								<v-btn color="primary" text>Save</v-btn>
							</v-row>
						</v-container>
					</v-form>
				</v-expansion-panel-content>
			</v-expansion-panel>
		</v-expansion-panels>
	</div>
</template>

<script lang="ts">
	import Vue from 'vue';
	import { VehicleData } from '@/components/SingleVin.vue';

	interface DataType {
		form: VehicleData;
		years: string[];
	}

	export default Vue.extend({
		props: {
			data: Object as () => VehicleData,
		},
		data: (): DataType => ({
			form: null,
			years: [],
		}),
		methods: {
			handleDelete() {
				alert('deleting...');
			},
		},
		mounted() {
			const currentYear = new Date().getFullYear();

			for (let year = currentYear; year > currentYear - 50; year--) {
				this.years.push(year.toString());
			}
		},
		watch: {
			data(nv: VehicleData) {
				this.form = nv;
			},
		},
	});
</script>
