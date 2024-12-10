<script setup>
import { computed } from 'vue';
import plansData from '@/assets/data/plans.json';

const props = defineProps({
    planData: Object,
    selectedAddOns: Array,
});

const plans = plansData.plans;

const selectedPlanData = computed(() => {
    const selected = plans.find(plan => plan.name === props.planData.plan);
    return selected;
});

const totalAmount = computed(() => {
    const selectedPlan = selectedPlanData.value;

    if (!selectedPlan) {
        return 0;
    }

    const basePrice = props.planData.billing === 'Monthly'
        ? parseFloat(selectedPlan.monthlyPrice.replace('$', '').replace('/mo', '') || '0')
        : parseFloat(selectedPlan.yearlyPrice.replace('$', '').replace('/yr', '') || '0') / 12;

    const addOnTotal = props.selectedAddOns.reduce((acc, addOn) => {
        const price = parseFloat(addOn.price?.replace('$', '').replace('/mo', '') || '0');
        return acc + price;
    }, 0);

    return basePrice + addOnTotal;
});
</script>

<template>
    <div class="px-12 md:px-48 py-10 md:py-20">
        <div class="mb-9">
            <h1 class="text-2xl md:text-3xl font-bold font-ubuntu text-marine-blue">Finishing up</h1>
            <p class="text-cool-gray font-ubuntu text-sm md:text-base">
                Double-check everything looks OK before confirming.
            </p>
        </div>

        <div v-if="selectedPlanData" class="bg-white p-6 rounded-md mb-6">
            <div class="flex justify-between items-center">
                <div class="flex items-center">
                    <p class="text-lg font-semibold text-marine-blue">{{ props.planData.plan }}</p>
                    <p class="text-lg font-semibold text-marine-blue">({{ props.planData.billing }})</p>
                </div>

                <p class="text-lg font-bold text-marine-blue ms-auto">
                    {{ props.planData.planPrice }}
                </p>
            </div>
            <div>
                <a href="#" @click="changePlan" class="text-purplish-blue text-sm hover:underline">
                    Change
                </a>
            </div>
        </div>
        <div v-else>
            <p class="text-red-500">Plan data is missing or incorrect.</p>
        </div>

        <div v-if="props.selectedAddOns.length > 0" class="bg-white p-6 rounded-md mb-6">
            <h3 class="text-lg font-bold text-marine-blue">Add-ons</h3>
            <div v-for="addOn in props.selectedAddOns" :key="addOn.name" class="flex justify-between items-center py-3">
                <p class="text-sm text-cool-gray">{{ addOn.name }}</p>
                <p class="text-sm text-gray-800">+{{ addOn.price }}</p>
            </div>
        </div>
        <div v-else>
            <p class="text-red-500">No add-ons selected.</p>
        </div>

        <div v-if="totalAmount > 0" class="bg-white p-6 rounded-md">
            <div class="flex justify-between items-center">
                <p class="text-sm text-cool-gray">Total (per month)</p>
                <p class="text-xl text-purplish-blue font-semibold">+{{ totalAmount.toFixed(2) }}$/mo</p>
            </div>
        </div>
        <div v-else>
            <p class="text-red-500">Total amount calculation failed.</p>
        </div>
    </div>
</template>
