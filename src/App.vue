<template>
  <div class="app">
    <div class="form-container">
      <h1>Contact Information Form</h1>
      
      <form @submit.prevent="submitForm">
        <!-- First Name Field -->
        <cdx-field class="form-field">
          <cdx-text-input 
            v-model="formData.firstName"
            :status="validationStatus.firstName"
            @blur="validateField('firstName')"
            required
          />
          <template #label>First Name</template>
          <template #description>Enter your given name</template>
          <template #help-text v-if="validationStatus.firstName === 'error'">
            Please enter your first name
          </template>
        </cdx-field>

        <!-- Last Name Field -->
        <cdx-field class="form-field">
          <cdx-text-input 
            v-model="formData.lastName"
            :status="validationStatus.lastName"
            @blur="validateField('lastName')"
            required
          />
          <template #label>Last Name</template>
          <template #description>Enter your family name</template>
          <template #help-text v-if="validationStatus.lastName === 'error'">
            Please enter your last name
          </template>
        </cdx-field>

        <!-- Email Address Field -->
        <cdx-field class="form-field">
          <cdx-text-input 
            v-model="formData.email"
            input-type="email"
            :status="validationStatus.email"
            @blur="validateField('email')"
            required
          />
          <template #label>Email Address</template>
          <template #description>Enter a valid email address</template>
          <template #help-text v-if="validationStatus.email === 'error'">
            Please enter a valid email address
          </template>
        </cdx-field>

        <!-- Phone Number Field -->
        <cdx-field class="form-field">
          <cdx-text-input 
            v-model="formData.phone"
            input-type="tel"
            :status="validationStatus.phone"
            @blur="validateField('phone')"
            placeholder="e.g., +1-123-456-7890"
          />
          <template #label>Phone Number</template>
          <template #description>Enter your phone number (optional)</template>
          <template #help-text v-if="validationStatus.phone === 'error'">
            Please enter a valid phone number
          </template>
        </cdx-field>

        <!-- Description Field -->
        <cdx-field class="form-field">
          <cdx-text-area
            v-model="formData.description"
            :status="validationStatus.description"
            @blur="validateField('description')"
            placeholder="Tell us more about yourself..."
            :rows="5"
          />
          <template #label>Description</template>
          <template #description>Provide additional information (optional)</template>
        </cdx-field>

        <!-- Form Controls -->
        <div class="form-actions">
          <cdx-button
            action="destructive"
            type="button"
            @click="resetForm"
          >
            Reset
          </cdx-button>
          
          <cdx-button
            action="progressive"
            weight="primary"
            type="submit"
          >
            Submit
          </cdx-button>
        </div>
      </form>

      <!-- Success Message -->
      <cdx-message
        v-if="formSubmitted"
        type="success"
        class="form-message"
      >
        Form submitted successfully!
      </cdx-message>
    </div>
  </div>
</template>

<script>
import { defineComponent, ref, reactive } from 'vue';
import {
  CdxField,
  CdxButton,
  CdxTextInput,
  CdxTextArea,
  CdxMessage
} from '@wikimedia/codex';

export default defineComponent({
  name: 'App',
  components: {
    CdxField,
    CdxButton,
    CdxTextInput,
    CdxTextArea,
    CdxMessage
  },
  setup() {
    // Form data
    const formData = reactive({
      firstName: '',
      lastName: '',
      email: '',
      phone: '',
      description: ''
    });

    // Validation status for each field
    const validationStatus = reactive({
      firstName: 'default',
      lastName: 'default',
      email: 'default',
      phone: 'default',
      description: 'default'
    });

    // Form submission status
    const formSubmitted = ref(false);

    // Validate a specific field
    const validateField = (field) => {
      switch (field) {
        case 'firstName':
          validationStatus.firstName = formData.firstName.trim() === '' ? 'error' : 'default';
          break;
        case 'lastName':
          validationStatus.lastName = formData.lastName.trim() === '' ? 'error' : 'default';
          break;
        case 'email':
          const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
          validationStatus.email = !emailRegex.test(formData.email) ? 'error' : 'default';
          break;
        case 'phone':
          if (formData.phone.trim() === '') {
            validationStatus.phone = 'default';
          } else {
            const phoneRegex = /^[+]?[(]?[0-9]{1,4}[)]?[-\s.]?[0-9]{1,4}[-\s.]?[0-9]{1,9}$/;
            validationStatus.phone = !phoneRegex.test(formData.phone) ? 'error' : 'default';
          }
          break;
        default:
          break;
      }
    };

    // Validate all fields at once
    const validateAllFields = () => {
      validateField('firstName');
      validateField('lastName');
      validateField('email');
      validateField('phone');
      
      // Check if any field has an error
      return Object.values(validationStatus).every(status => status !== 'error');
    };

    // Submit form
    const submitForm = () => {
      if (validateAllFields()) {
        console.log('Form data submitted:', formData);
        formSubmitted.value = true;

        // Reset the form after 3 seconds
        setTimeout(() => {
          formSubmitted.value = false;
        }, 3000);
      }
    };

    // Reset form
    const resetForm = () => {
      // Reset form data
      Object.keys(formData).forEach(key => {
        formData[key] = '';
      });

      // Reset validation status
      Object.keys(validationStatus).forEach(key => {
        validationStatus[key] = 'default';
      });

      // Reset form submission status
      formSubmitted.value = false;
    };

    return {
      formData,
      validationStatus,
      formSubmitted,
      validateField,
      submitForm,
      resetForm
    };
  }
});
</script>

<style>
.app {
  font-family: Arial, sans-serif;
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.form-container {
  background-color: #f8f9fa;
  border-radius: 8px;
  padding: 24px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

h1 {
  color: #202122;
  margin-bottom: 24px;
  font-size: 24px;
}

.form-field {
  margin-bottom: 20px;
}

.form-actions {
  display: flex;
  justify-content: flex-end;
  gap: 12px;
  margin-top: 32px;
}

.form-message {
  margin-top: 24px;
}
</style>
