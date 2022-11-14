<template>
	<div>
		<p>Enter a VIN and we'll use our data partner to search for you vehicle.</p>
		<v-form @submit.prevent="handleSubmit">
			<v-row>
				<v-col>
					<v-text-field
						:error-messages="isError ? 'VIN is required' : ''"
						v-model="vin"
						label="Enter VIN"
					></v-text-field>
				</v-col>
				<v-col></v-col>
			</v-row>
			<v-row>
				<v-col></v-col>
				<v-col></v-col>
				<v-col>
					<v-layout justify-center>
						<v-btn
							color="primary"
							:disabled="loading"
							type="submit"
							:loading="loading"
						>
							Lookup Vehicle
						</v-btn>
					</v-layout>
				</v-col>
			</v-row>
		</v-form>
	</div>
</template>

<script lang="ts">
import Vue from 'vue';

export interface FormType {
	vin: string;
}

export default Vue.extend({
	props: {
		loading: Boolean,
	},
	data: () => ({
		isError: false,
		vin: '',
	}),
	methods: {
		handleSubmit() {
			if (this.vin.trim()) {
				this.isError = false;
				this.$emit('handleSubmit', { vin: this.vin });
				this.vin = '';
				return;
			}

			this.isError = true;
		},
	},
});
</script>
