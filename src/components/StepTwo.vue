<script setup>
import { reactive, defineEmits } from 'vue';
import plansData from '@/assets/data/plans.json';
const emit = defineEmits(['update-plan']);

const selectedPlan = reactive({
    current: 'Arcade',
    billing: 'Monthly',
    planPrice: ''
});

const plans = plansData.plans;

// Map plan names to their respective images (static import)
const planIcons = {
    Arcade: require('@/assets/icons/arcade.svg'),
    Advanced: require('@/assets/icons/advanced.svg'),
    Pro: require('@/assets/icons/pro.svg')
};

const selectPlan = (planName) => {
    selectedPlan.current = planName;
    updatePlanPrice();
    emitUpdatedPlan();
};

const toggleBilling = () => {
    selectedPlan.billing = selectedPlan.billing === 'Monthly' ? 'Yearly' : 'Monthly';
    updatePlanPrice();
    emitUpdatedPlan();
};

const updatePlanPrice = () => {
    const selected = plans.find(plan => plan.name === selectedPlan.current);
    if (selected) {
        selectedPlan.planPrice = selectedPlan.billing === 'Monthly'
            ? selected.monthlyPrice
            : selected.yearlyPrice;
    }
};

const emitUpdatedPlan = () => {
    emit('update-plan', {
        plan: selectedPlan.current,
        billing: selectedPlan.billing,
        planPrice: selectedPlan.planPrice
    });
};

updatePlanPrice();
</script>

<template>
    <div class="px-12 md:px-48 py-10 md:py-20">
        <div class="mb-10">
            <h1 class="text-2xl md:text-3xl font-bold font-ubuntu text-marine-blue">Select your plan</h1>
            <p class="text-cool-gray font-ubuntu text-sm md:text-base">
                You have the option of monthly or yearly billing.
            </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
            <div v-for="plan in plans" :key="plan.name" @click="selectPlan(plan.name)" :class="[
                'border rounded-md px-4 py-6 cursor-pointer transition',
                selectedPlan.current === plan.name
                    ? 'border-purplish-blue'
                    : 'border-light-gray bg-white hover:border-purplish-blue'
            ]">
                <!-- Use statically imported icons -->
                <img :src="planIcons[plan.name]" :alt="plan.name" class="w-12 h-12 mb-4" />
                <h2 class="text-lg font-bold font-ubuntu text-marine-blue mt-8">{{ plan.name }}</h2>
                <p class="text-cool-gray text-sm mt-2">
                    {{ selectedPlan.billing === 'Monthly' ? plan.monthlyPrice : plan.yearlyPrice }}
                </p>
            </div>
        </div>

        <div class="flex justify-center items-center gap-4 my-6">
            <span :class="{ 'text-marine-blue': selectedPlan.billing === 'Monthly' }"
                class="text-sm font-ubuntu text-cool-gray">Monthly</span>
            <button @click="toggleBilling"
                class="relative w-12 h-6 bg-marine-blue rounded-full cursor-pointer transition">
                <span class="absolute top-0.5 left-1 w-5 h-5 bg-white rounded-full transition-transform"
                    :class="{ 'translate-x-6': selectedPlan.billing === 'Yearly' }"></span>
            </button>
            <span :class="{ 'text-marine-blue': selectedPlan.billing === 'Yearly' }"
                class="text-sm font-ubuntu text-cool-gray">Yearly</span>
        </div>
    </div>
</template>
