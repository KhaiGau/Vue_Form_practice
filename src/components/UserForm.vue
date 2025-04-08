<script setup>
import { ref, computed } from 'vue';

const formData = ref({
  name: '',
  email: '',
  gender: '',
  hobbies: [],
  note: '',
  agreePolicy: false,
});

const showResult = ref(false);

const nameError = computed(() => {
  if (!formData.value.name) return '';
  return formData.value.name.length < 3
    ? 'Name must be at least 3 characters'
    : '';
});

const emailError = computed(() => {
  if (!formData.value.email) return '';
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return !emailRegex.test(formData.value.email)
    ? 'Please enter a valid email'
    : '';
});

const isFormValid = computed(() => {
  return (
    formData.value.name.length >= 3 &&
    /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formData.value.email) &&
    formData.value.gender &&
    formData.value.agreePolicy
  );
});

const hobbyOptions = [
  'Reading',
  'Gaming',
  'Cooking',
  'Sports',
  'Music',
  'Travel',
  'Art',
  'Photography',
];

const resetForm = () => {
  formData.value = {
    name: '',
    email: '',
    gender: '',
    hobbies: [],
    note: '',
    agreePolicy: false,
  };
};

const handleSubmit = () => {
  if (isFormValid.value) {
    showResult.value = true;
  }
};
</script>

<template>
  <div class="container mt-5">
    <div v-if="!showResult" class="card">
      <div class="card-body">
        <div class="card-title">
          <mb-4>User Registration Form</mb-4>
        </div>


        <form @submit.prevent="handleSubmit" class="needs-validation">
          <!-- Name Input -->
          <div class="mb-3">
            <label for="name" class="form-label">Name *</label>
            <input
              type="text"
              class="form-control"
              :class="{ 'is-invalid': nameError }"
              id="name"
              v-model="formData.name"
              required
            />
            <div class="invalid-feedback" v-if="nameError">
              {{ nameError }}
            </div>
          </div>

          <!-- Email Input -->
          <div class="mb-3">
            <label for="email" class="form-label">Email *</label>
            <input
              type="email"
              class="form-control"
              :class="{ 'is-invalid': emailError }"
              id="email"
              v-model="formData.email"
              required
            />
            <div class="invalid-feedback" v-if="emailError">
              {{ emailError }}
            </div>
          </div>

          <!-- Gender Radio -->
          <div class="mb-3">
            <label class="form-label">Gender *</label>
            <div class="form-check">
              <input
                class="form-check-input"
                type="radio"
                id="male"
                value="male"
                v-model="formData.gender"
                required
              />
              <label class="form-check-label" for="male">Male</label>
            </div>
            <div class="form-check">
              <input
                class="form-check-input"
                type="radio"
                id="female"
                value="female"
                v-model="formData.gender"
              />
              <label class="form-check-label" for="female">Female</label>
            </div>
          </div>

          <!-- Hobbies Multiple Select -->
          <div class="mb-3">
            <label for="hobbies" class="form-label">Hobbies</label>
            <select
              multiple
              class="form-select"
              id="hobbies"
              v-model="formData.hobbies"
            >
              <option v-for="hobby in hobbyOptions" :key="hobby" :value="hobby">
                {{ hobby }}
              </option>
            </select>
          </div>

          <!-- Note Textarea -->
          <div class="mb-3">
            <label for="note" class="form-label">Note</label>
            <textarea
              class="form-control"
              id="note"
              rows="3"
              v-model="formData.note"
            ></textarea>
          </div>

          <!-- Policy Checkbox -->
          <div class="mb-3 form-check">
            <input
              type="checkbox"
              class="form-check-input"
              id="policy"
              v-model="formData.agreePolicy"
              required
            />
            <label class="form-check-label" for="policy">
              I agree to the terms and conditions *
            </label>
          </div>

          <div class="d-flex align-items-center gap-3">
            <button
              type="submit"
              class="btn btn-primary"
              :disabled="!isFormValid"
            >
              Submit
            </button>
            <button
              type="button"
              @click="resetForm"
              class="btn btn-sm btn-outline-secondary"
              title="Reset form"
            >
              ↺
            </button>
          </div>
        </form>
      </div>
    </div>

    <!-- Result Screen -->
    <div v-else class="card">
      <div class="card-body">
        <h2 class="card-title mb-4">Registration Information</h2>
        <div class="mb-3"><strong>Name:</strong> {{ formData.name }}</div>
        <div class="mb-3"><strong>Email:</strong> {{ formData.email }}</div>
        <div class="mb-3"><strong>Gender:</strong> {{ formData.gender }}</div>
        <div class="mb-3">
          <strong>Hobbies:</strong> {{ formData.hobbies.join(', ') }}
        </div>
        <div class="mb-3"><strong>Note:</strong> {{ formData.note }}</div>
        <button class="btn btn-secondary" @click="showResult = false">
          Back to Form
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  max-width: 600px;
  margin: 0 auto;
}
.card-title mb-4 {
  color: red;
  background-color: blue;
  border: 5px solid yellow;
  padding: 5px;
}

</style>
