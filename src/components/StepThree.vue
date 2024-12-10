<script setup>
import { ref, defineEmits } from 'vue';

const addOns = [
    { name: 'Online Services', price: '$1/mo', description: 'Access to multiplayer' },
    { name: 'Extra Large Storage', price: '$2/mo', description: 'Extra 1TB of cloud save' },
    { name: 'Customizable Profile', price: '$3/mo', description: 'Custom theme on your profile' },
];

const emit = defineEmits(['update-addons']);

const selectedAddOns = ref([]);

const toggleAddOn = (addOn) => {
    const index = selectedAddOns.value.indexOf(addOn);
    if (index > -1) {
        selectedAddOns.value.splice(index, 1); // Remove add-on
    } else {
        selectedAddOns.value.push(addOn); // Add add-on
    }
    emit('update-addons', selectedAddOns.value); // Emit selected add-ons to parent
};
</script>

<template>
    <div class="px-12 md:px-48 py-10 md:py-20">
        <div class="mb-9">
            <h1 class="text-2xl md:text-3xl font-bold font-ubuntu text-marine-blue">Pick add-ons</h1>
            <p class="text-cool-gray font-ubuntu text-sm md:text-base">
                Add-ons help enhance your gaming experience.
            </p>
        </div>

        <div class="flex flex-col gap-4">
            <div v-for="addOn in addOns" :key="addOn.name"
                class="flex items-center justify-between border border-light-gray rounded-md p-4 hover:border-purplish-blue transition">
                <label class="flex items-center gap-4 cursor-pointer">
                    <input type="checkbox" :id="addOn.name" class="form-checkbox text-purplish-blue h-5 w-5"
                        @change="toggleAddOn(addOn)" />
                    <div>
                        <h2 class="font-bold font-ubuntu text-marine-blue">{{ addOn.name }}</h2>
                        <p class="text-sm text-cool-gray">{{ addOn.description }}</p>
                    </div>
                </label>
                <div class="text-right">
                    <p class="text-purplish-blue font-medium">{{ addOn.price }}</p>
                </div>
            </div>
        </div>
    </div>
</template>
