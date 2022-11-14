<template>
	<v-card flat>
		<v-card-text>
			<VinForm :loading="isFetching" @handleSubmit="handleFormSubmission"></VinForm>
			<ActiveVehicles :data="vehicleData"></ActiveVehicles>
		</v-card-text>
	</v-card>
</template>

<script lang="ts">
	import Vue from 'vue';
	import ActiveVehicles from '@/components/ActiveVehicles.vue';
	import VinForm, { FormType } from '@/components/VinForm.vue';

	interface DecodeVinResult {
		Value: string;
		ValueId: string;
		Variable: string;
		VariableId: number;
	}

	interface DecodeVinResponse {
		Count: number;
		Message: string;
		Results: DecodeVinResult[];
		SearchCriteria: string;
	}

	interface DataType {
		isFetching: boolean;
		vehicleData: VehicleData;
	}

	export type VehicleData = null | Record<string | 'Model' | 'Model Year' | 'Make' | 'vin', string>;

	export default Vue.extend({
		components: { ActiveVehicles, VinForm },
		data: (): DataType => ({
			isFetching: false,
			vehicleData: null,
		}),
		methods: {
			async handleFormSubmission({ vin }: FormType) {
				this.isFetching = true;
				const res = await fetch(`${process.env.VUE_APP_VIN_API}/decodevin/${vin}?format=json`, { method: 'GET' });
				const { Results } = await res.json() as DecodeVinResponse;

				const data = Results.reduce((result, current) => {
					return {
						...result,
						[current.Variable]: current.Value,
					};
				}, {});

				this.isFetching = false;
				this.vehicleData = { ...data, vin };
			},
		},
	});
</script>
