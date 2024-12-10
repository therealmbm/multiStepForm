<script setup>
import { defineProps } from 'vue';
defineProps({
    currentStep: Number // Accept currentStep as a prop
});
</script>

<template>
    <div
        class="bg-[url('@/assets/images/bg-sidebar-desktop.svg')] bg-cover bg-center w-full rounded-md text-white p-10">
        <ul>
            <li class="py-7">
                <div class="flex gap-5">
                    <p :class="[
                        'font-bold w-fit py-2 px-4 rounded-full',
                        currentStep === 1 ? 'bg-pastel-blue text-marine-blue' : 'border border-pastel-blue text-white'
                    ]">1</p>
                    <div class="items-center leading-3">
                        <p class="font-extralight">STEP 1</p>
                        <h3 class="text-lg font-semibold tracking-widest">YOUR INFO</h3>
                    </div>
                </div>
            </li>
            <li class="py-7">
                <div class="flex gap-5">
                    <p :class="[
                        'font-bold w-fit py-2 px-4 rounded-full',
                        currentStep === 2 ? 'bg-pastel-blue text-marine-blue' : 'border border-pastel-blue text-white'
                    ]">2</p>
                    <div class="items-center leading-3">
                        <p class="font-extralight">STEP 2</p>
                        <h3 class="text-lg font-semibold tracking-widest">SELECT PLAN</h3>
                    </div>
                </div>
            </li>
            <li class="py-7">
                <div class="flex gap-5">
                    <p :class="[
                        'font-bold w-fit py-2 px-4 rounded-full',
                        currentStep === 3 ? 'bg-pastel-blue text-marine-blue' : 'border border-pastel-blue text-white'
                    ]">3</p>
                    <div class="items-center leading-3">
                        <p class="font-extralight">STEP 3</p>
                        <h3 class="text-lg font-semibold tracking-widest">ADD ONS</h3>
                    </div>
                </div>
            </li>
            <li class="py-7">
                <div class="flex gap-5">
                    <p :class="[
                        'font-bold w-fit py-2 px-4 rounded-full',
                        currentStep === 4 ? 'bg-pastel-blue text-marine-blue' : 'border border-pastel-blue text-white'
                    ]">4</p>
                    <div class="items-center leading-3">
                        <p class="font-extralight">STEP 4</p>
                        <h3 class="text-lg font-semibold tracking-widest">SUMMARY</h3>
                    </div>
                </div>
            </li>
            <li class="py-7">
                <div class="flex gap-5">
                    <p :class="[
                        'font-bold w-fit py-2 px-4 rounded-full',
                        currentStep === 5 ? 'bg-pastel-blue text-marine-blue' : 'border border-pastel-blue text-white'
                    ]">5</p>
                    <div class="items-center leading-3">
                        <p class="font-extralight">STEP 5</p>
                        <h3 class="text-lg font-semibold tracking-widest">FINISH</h3>
                    </div>
                </div>
            </li>
        </ul>
    </div>
</template>
