<script setup>
import { ref, defineProps, defineEmits } from 'vue';

const emit = defineEmits(['update-inputs']);
const props = defineProps({
    errors: {
        type: Object,
        required: true,
    }
});

const form = ref({
    name: '',
    email: '',
    phone: '',
});

function emitInputs() {
    emit('update-inputs', form.value);
}

</script>

<template>
    <div class="px-12 md:px-48 py-10 md:py-20">
        <div class="mb-9">
            <h1 class="text-2xl md:text-3xl font-bold font-ubuntu text-marine-blue">Personal info</h1>
            <p class="text-cool-gray font-ubuntu text-sm md:text-base">
                Please provide your name, email address, and phone number.
            </p>
        </div>
        <form @submit.prevent="validateForm" class="flex flex-col gap-6 md:gap-9">
            <div class="flex flex-col gap-1">
                <div class="flex justify-between items-center">
                    <label class="text-marine-blue text-sm md:text-base font-medium" for="name">Name</label>
                    <span v-if="errors.name" class="text-strawberry-red text-xs"> {{ errors.name }} </span>
                </div>
                <input v-model="form.name" @input="emitInputs" type="text" name="name" id="name"
                    placeholder="e.g. Stephen King" :class="[
                        'border p-2 rounded text-sm md:text-base focus:outline-none focus:ring-2',
                        errors.name ? 'border-strawberry-red focus:ring-strawberry-red' : 'border-light-gray focus:ring-purplish-blue'
                    ]" />
            </div>

            <div class="flex flex-col gap-1">
                <div class="flex justify-between items-center">
                    <label class="text-marine-blue text-sm md:text-base font-medium" for="email">Email Address</label>
                    <span v-if="errors.email" class="text-strawberry-red text-xs"> {{ errors.email }} </span>
                </div>
                <input v-model="form.email" @input="emitInputs" type="email" name="email" id="email"
                    placeholder="e.g. 0XZyH@example.com" :class="[
                        'border p-2 rounded text-sm md:text-base focus:outline-none focus:ring-2',
                        errors.email ? 'border-strawberry-red focus:ring-strawberry-red' : 'border-light-gray focus:ring-purplish-blue'
                    ]" />
            </div>

            <div class="flex flex-col gap-1">
                <div class="flex justify-between items-center">
                    <label class="text-marine-blue text-sm md:text-base font-medium" for="phone">Phone Number</label>
                    <span v-if="errors.phone" class="text-strawberry-red text-xs"> {{ errors.phone }} </span>
                </div>
                <input v-model="form.phone" @input="emitInputs" type="text" name="phone" id="phone"
                    placeholder="e.g. +1 234 567 890" :class="[
                        'border p-2 rounded text-sm md:text-base focus:outline-none focus:ring-2',
                        errors.phone ? 'border-strawberry-red focus:ring-strawberry-red' : 'border-light-gray focus:ring-purplish-blue'
                    ]" />
            </div>
        </form>
    </div>
</template>
