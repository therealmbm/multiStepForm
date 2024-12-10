<script setup>
import { ref } from 'vue';
import StepsCounter from '@/components/StepsCounter.vue';
import StepOne from '@/components/StepOne.vue';
import StepTwo from './components/StepTwo.vue';
import StepThree from './components/StepThree.vue';
import StepFour from './components/StepFour.vue';
import StepFive from './components/StepFive.vue';

const currentStep = ref(1);
const totalSteps = 5;

const PersonalData = ref({
  name: '',
  email: '',
  phone: '',
});

const inputErrors = ref({
  name: '',
  email: '',
  phone: '',
});

const planData = ref({
  plan: 'Arcade',
  billing: 'Monthly',
  planPrice: '',
});

const selectedAddOns = ref([]);

// Function to update selected plan in StepTwo
function updateSelectedPlan(updatedPlan) {
  planData.value = { ...updatedPlan };
}

const nextStep = () => {
  inputErrors.value = { name: '', email: '', phone: '' };
  let isValid = true;

  for (const [key, value] of Object.entries(PersonalData.value)) {
    if (value.trim(value) === '') {
      inputErrors.value[key] = 'This field is required';
      isValid = false;
    }
  }
  if (isValid && currentStep.value < totalSteps) {
    currentStep.value++;
  }
};

const prevStep = () => {
  if (currentStep.value > 1) {
    currentStep.value--;
  }
};

function updatePersonalData(updatedInputs) {
  PersonalData.value = { ...PersonalData.value, ...updatedInputs };
}

const updateSelectedAddOns = (addOnsData) => {
  selectedAddOns.value = addOnsData;
};
</script>

<template>
  <div class="py-12 md:py-28 px-6 md:px-72 bg-slate-200 min-h-screen">
    <div class="grid grid-cols-1 md:grid-cols-[1fr_3fr] bg-white rounded-xl p-4 min-h-[650px]">
      <StepsCounter :currentStep="currentStep" />
      <div>
        <StepOne v-if="currentStep === 1" :errors="inputErrors" @update-inputs="updatePersonalData" />
        <StepTwo v-if="currentStep === 2" @update-plan="updateSelectedPlan" />
        <StepThree v-if="currentStep === 3" @update-addons="updateSelectedAddOns" />
        <StepFour v-if="currentStep === 4" :planData="planData" :selectedAddOns="selectedAddOns" />
        <StepFive v-if="currentStep === 5" />
        <div class="flex justify-between items-center px-6 md:px-24 mb-10">
          <a href="#" v-if="currentStep > 1 && currentStep < totalSteps" @click="prevStep"
            class="text-lg font-ubuntu text-cool-gray hover:text-purplish-blue focus:text-purplish-blue focus:outline-none active:text-marine-blue transition">
            Go Back
          </a>
          <button type="button" v-if="currentStep < totalSteps" @click="nextStep"
            class="bg-marine-blue px-6 py-3 md:px-8 md:py-4 ms-auto rounded-md text-white font-medium hover:bg-purplish-blue transition">
            Next Step
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
