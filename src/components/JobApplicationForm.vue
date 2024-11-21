<template>
  <div class="application-form">
    <!-- Background Moving Circles -->
    <div class="animated-background-circle circle-1"></div>
    <div class="animated-background-circle circle-2"></div>
    <div class="animated-background-circle circle-3"></div>
    <div class="animated-background-circle circle-4"></div>

    <!-- New Small Circles -->
    <div class="animated-background-circle circle-5"></div>
    <div class="animated-background-circle circle-6"></div>

    <!-- Modal Container for the Form -->
    <div class="form-container">
      <!-- Cancel Button to Close Form -->
      <button class="btn-cancel-top-right" @click="cancelApplication">X</button>

      <h2 class="form-title">Apply Now and Shine!</h2>

      <!-- Application Form -->
      <form @submit.prevent="submitForm">
        <!-- Name Input Field -->
        <div class="form-group">
          <label for="name">Full Name</label>
          <input type="text" id="name" v-model="formData.name" required placeholder="Enter your full name" />
        </div>

        <!-- Email Input Field -->
        <div class="form-group">
          <label for="email">Email</label>
          <input type="email" id="email" v-model="formData.email" required placeholder="Enter your email address" />
        </div>

        <!-- Resume Upload Input -->
        <div class="form-group">
          <label for="resume">Upload Resume</label>
          <input type="file" id="resume" @change="handleFileUpload" />
        </div>

        <!-- Submit Button -->
        <div class="form-action">
          <button class="btn-submit" type="submit">Submit Application</button>
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
    };
  },
  methods: {
    // This function runs when the form is submitted
    submitForm() {
      alert('Your application has been submitted!'); // Show a success message
      this.formData.name = ''; // Reset the name field
      this.formData.email = ''; // Reset the email field
      this.formData.resume = null; // Clear the resume file
      this.$emit('close'); // Close the form/modal
    },
    // This function is triggered when the cancel button is clicked
    cancelApplication() {
      this.$emit('close'); // Close the form/modal
    },
    // This function handles file upload and stores the selected file
    handleFileUpload(event) {
      this.formData.resume = event.target.files[0]; // Store the selected resume file
    },
  },
};
</script>

<style scoped>
/* Main overlay container to center the form */
.application-form {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 40px;
  background: rgba(0, 0, 0, 0.5); /* Dark background overlay */
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1000;
  backdrop-filter: blur(8px); /* Blur the background */
}

/* Container for the form itself with a colorful gradient background */
.form-container {
  position: relative;
  background: linear-gradient(135deg, #3498db, #9b59b6, #e74c3c);
  padding: 40px;
  width: 500px;
  max-width: 90%;
  border-radius: 20px;
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.2);
  text-align: center;
  animation: gradientAnimation 6s ease infinite, slide-up 0.5s ease-out;
  overflow: hidden;
}

/* Keyframe animation to make the background gradient move */
@keyframes gradientAnimation {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

/* Slide-up animation for form when it appears */
@keyframes slide-up {
  from {
    transform: translateY(30px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

/* Style for background circles that move */
.animated-background-circle {
  position: absolute;
  border-radius: 50%;
  opacity: 0.4; /* Make circles a little transparent */
  animation: moveCircle 12s infinite ease-in-out alternate;
}

/* Positioning and styling for the large background circles */
.circle-1 {
  width: 350px;
  height: 350px;
  background: radial-gradient(circle, #ff9a9e, #fad0c4);
  top: -20%;
  left: -20%;
  animation-delay: 0s;
}

.circle-2 {
  width: 400px;
  height: 400px;
  background: radial-gradient(circle, #a18cd1, #fbc2eb);
  bottom: -20%;
  right: -10%;
  animation-delay: 2s;
}

.circle-3 {
  width: 300px;
  height: 300px;
  background: radial-gradient(circle, #9b59b6, #e74c3c);
  bottom: 70%;
  right: -0.5%;
  animation-delay: 4s;
}

.circle-4 {
  width: 280px;
  height: 280px;
  background: radial-gradient(circle, #f39c12, #e67e22);
  top: 70%;
  left: -0.5%;
  animation-delay: 6s;
}

/* Styling for smaller background circles */
.circle-5 {
  width: 60px;
  height: 60px;
  background: radial-gradient(circle, #ff9a9e, #fad0c4);
  top: 50%;
  right: 20%;
  animation: moveSmallCircle 11s infinite ease-in-out alternate;
}

.circle-6 {
  width: 60px;
  height: 60px;
  background: radial-gradient(circle, #9b59b6, #e74c3c);
  top: 50%;
  left: 20%;
  animation: moveSmallCircle 11s infinite ease-in-out alternate;
}

/* Circle movement animation */
@keyframes moveCircle {
  0% {
    transform: translate(0, 0) scale(1);
  }
  50% {
    transform: translate(30px, -30px) scale(1.3);
  }
  100% {
    transform: translate(-30px, 30px) scale(1);
  }
}

/* Small circle movement animation */
@keyframes moveSmallCircle {
  0% {
    transform: translateX(0);
  }
  50% {
    transform: translateX(200px);
  }
  100% {
    transform: translateX(0);
  }
}

/* Cancel button style to close the form */
.btn-cancel-top-right {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  font-size: 1.5rem;
  color: white;
  cursor: pointer;
  transition: transform 0.3s ease, color 0.3s ease;
  z-index: 2;
}

/* Cancel button hover effect */
.btn-cancel-top-right:hover {
  color: #e74c3c;
  transform: scale(1.2);
}

/* Form title styling */
.form-title {
  font-size: 2rem;
  font-weight: bold;
  color: white;
  margin-bottom: 30px;
  text-transform: uppercase;
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
  font-size: 1.2rem;
  color: white;
  margin-bottom: 8px;
}

/* Input field styling */
.form-group input {
  padding: 12px;
  font-size: 1rem;
  border: none;
  border-radius: 10px;
  outline: none;
  transition: all 0.3s ease;
  background: rgba(255, 255, 255, 0.8);
  color: #2c3e50;
}

/* Input field focus effect */
.form-group input:focus {
  box-shadow: 0 0 10px rgba(52, 152, 219, 0.8);
}

/* Submit button styling */
.form-action {
  display: flex;
  justify-content: center;
  margin-top: 30px;
}

.btn-submit {
  background: linear-gradient(135deg, #f39c12, #e74c3c);
  color: white;
  padding: 12px 30px;
  border: none;
  border-radius: 25px;
  font-size: 1.2rem;
  font-weight: bold;
  cursor: pointer;
  transition: transform 0.2s ease, box-shadow 0.3s ease;
}

/* Submit button hover effect */
.btn-submit:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(255, 87, 34, 0.5);
}

/* Submit button active effect */
.btn-submit:active {
  transform: translateY(0);
  box-shadow: none;
}
</style>
