<template>
  <div class="application-form">
    <!-- Modal Container for the Form -->
    <div class="form-container">
      <!-- Circle elements -->
      <div class="circle circle-top"></div>
      <div class="circle circle-bottom"></div>
      <div class="circle circle-bottom-right"></div>

      <!-- Cancel Button to Close Form -->
      <button class="btn-cancel-top-right" @click="cancelApplication">X</button>

      <h2 class="form-title">Apply Now and Shine!</h2>

      <!-- Application Form -->
      <form @submit.prevent="submitForm">
        <!-- Name Input Field -->
        <div class="form-group">
          <label for="name">Full Name <span class="required">*</span></label>
          <input type="text" id="name" v-model="formData.name" required placeholder="Enter your full name" />
          <span v-if="nameError" class="error-message">{{ nameError }}</span>
        </div>

        <!-- Email Input Field -->
        <div class="form-group">
          <label for="email">Email <span class="required">*</span></label>
          <input type="email" id="email" v-model="formData.email" required placeholder="Enter your email address" />
          <span v-if="emailError" class="error-message">{{ emailError }}</span>
        </div>

        <!-- Resume Upload Input -->
        <div class="form-group">
          <label for="resume">Upload Resume <span class="required">*</span></label>
          <input type="file" id="resume" ref="resumeInput" @change="handleFileUpload" required />
          <span v-if="resumeError" class="error-message">{{ resumeError }}</span>
        </div>

        <!-- Submit and Clear Buttons -->
        <div class="form-action">
          <button class="btn-submit" type="submit">Submit Application</button>
          <button class="btn-clear" type="button" @click="clearForm">Clear</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        name: '',
        email: '',
        resume: null, // Store resume file here
      },
      nameError: '',
      emailError: '',
      resumeError: '',
    };
  },
  methods: {
    submitForm() {
      this.nameError = '';
      this.emailError = '';
      this.resumeError = '';

      let isValid = true;

      if (!this.formData.name || !/^[A-Za-z\s]+$/.test(this.formData.name)) {
        this.nameError = 'Please enter a valid name (only letters and spaces).';
        isValid = false;
      }

      if (!this.formData.email || !/\S+@\S+\.\S+/.test(this.formData.email)) {
        this.emailError = 'Please enter a valid email address.';
        isValid = false;
      }

      if (!this.formData.resume) {
        this.resumeError = 'Please upload your resume.';
        isValid = false;
      }

      if (isValid) {
        alert('Your application has been submitted!');
        this.formData.name = '';
        this.formData.email = '';
        this.formData.resume = null;
        this.$emit('close');
      }
    },
    cancelApplication() {
      this.$emit('close');
    },
    handleFileUpload(event) {
      this.formData.resume = event.target.files[0];
    },
    clearForm() {
      this.formData.name = '';
      this.formData.email = '';
      this.formData.resume = null;
      this.$refs.resumeInput.value = '';
      this.nameError = '';
      this.emailError = '';
      this.resumeError = '';
    },
  },
};
</script>

<style scoped>
.application-form {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 40px;
  background: rgba(0, 0, 0, 0.6);
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1000;
  backdrop-filter: blur(8px);
}

.form-container {
  position: relative;
  background: linear-gradient(135deg, #ffffff, #f5f5f5);
  padding: 40px;
  width: 500px;
  max-width: 90%;
  border-radius: 15px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
  text-align: center;
  animation: fadeIn 0.5s ease-out;
  overflow: hidden;
}

/* Circle Styling */
.circle {
  position: absolute;
  width: 150px;
  height: 150px;
  border-radius: 50%;
  z-index: 0;
  opacity: 0.2;
}

.circle-top {
  background: radial-gradient(circle, #ff9a9e, #fad0c4);
  top: -50px;
  right: -50px;
}

.circle-bottom {
  background: radial-gradient(circle, #a18cd1, #fbc2eb);
  bottom: -50px;
  left: -50px;
}

.circle-bottom-right {
  background: radial-gradient(circle, #6dd5ed, #2193b0);
  bottom: -80px;
  right: -60px;
}

/* Fade-in animation for form */
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Cancel button style */
.btn-cancel-top-right {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  font-size: 1.5rem;
  color: #e74c3c;
  cursor: pointer;
  transition: transform 0.3s ease, color 0.3s ease;
}

/* Cancel button hover effect */
.btn-cancel-top-right:hover {
  transform: scale(1.2);
  color: #c0392b;
}

/* Form title styling */
/* Form title styling */
.form-title {
  font-size: 2rem; /* Larger size */
  font-weight: 800; /* Bolder font weight */
  color: transparent;
  background: linear-gradient(45deg, #f39c12, #e74c3c, #8e44ad);
  -webkit-background-clip: text; /* Clip background to text */
  background-clip: text;
  margin-bottom: 25px;
  text-transform: uppercase;
  letter-spacing: 2px; /* Slightly increased letter spacing */
  animation: fadeInText 1s ease-out; /* Text fade-in animation */
  text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.2); /* Subtle text shadow */
}

/* Text fade-in animation */
@keyframes fadeInText {
  0% {
    opacity: 0;
    transform: translateY(-10px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}


/* Style for input fields */
.form-group {
  margin-bottom: 20px;
  text-align: left;
  display: flex;
  flex-direction: column;
}

/* Label styling */
.form-group label {
  font-size: 1.1rem;
  color: #333;
  margin-bottom: 8px;
}

/* Asterisk for required fields */
.required {
  color: red;
}

/* Input field styling */
.form-group input {
  padding: 12px;
  font-size: 1rem;
  border: 1px solid #ddd;
  border-radius: 10px;
  outline: none;
  transition: all 0.3s ease;
  background: #f9f9f9;
  color: #333;
}

/* Input field focus effect */
.form-group input:focus {
  border-color: #3498db;
  box-shadow: 0 0 10px rgba(52, 152, 219, 0.6);
}

/* Submit button styling */
.form-action {
  display: flex;
  justify-content: center;
  margin-top: 30px;
}

/* Submit button style */
.btn-submit {
  background: linear-gradient(135deg, #f39c12, #e74c3c);
  color: white;
  padding: 12px 30px;
  border: none;
  border-radius: 25px;
  font-size: 1.1rem;
  font-weight: bold;
  cursor: pointer;
  transition: transform 0.2s ease, box-shadow 0.3s ease;
  text-transform: uppercase;
}

/* Submit button hover effect */
.btn-submit:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(255, 87, 34, 0.5);
}

/* Clear button style */
.btn-clear {
  background: linear-gradient(135deg, #8e44ad, #3498db);
  color: white;
  padding: 12px 30px;
  border: none;
  border-radius: 25px;
  font-size: 1.1rem;
  font-weight: bold;
  cursor: pointer;
  transition: transform 0.2s ease, box-shadow 0.3s ease;
  margin-left: 10px;
  text-transform: uppercase;
}

/* Clear button hover effect */
.btn-clear:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(255, 87, 34, 0.5);
}

/* Clear button active effect */
.btn-clear:active {
  transform: translateY(0);
  box-shadow: none;
}

/* Error message styling */
.error-message {
  color: red;
  font-size: 0.9rem;
  margin-top: 5px;
}
</style>
