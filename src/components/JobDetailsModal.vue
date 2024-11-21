<template>
  <div class="modal">
    <!-- Modal content container -->
    <div class="modal-content">
      <!-- Close button to close the modal -->
      <button class="close-btn" @click="$emit('close')">&times;</button>
      
      <!-- Header section to display the job title -->
      <div class="header">
        <h2>{{ job.title }}</h2>
      </div>
      
      <!-- Details section to display job information -->
      <div class="details">
        <!-- Decorative circle at the top -->
        <div class="circle circle-top"></div>
        
        <!-- Job information such as company name and location -->
        <div class="info">
          <p><span class="label">Company:</span> {{ job.company }}</p>
          <p><span class="label">Location:</span> {{ job.location }}</p>
        </div>
        
        <!-- Decorative circle at the bottom -->
        <div class="circle circle-bottom"></div>
        
        <!-- Job description section -->
        <div class="description">
          <p>{{ job.description || "Description coming soon..." }}</p>
        </div>
      </div>
      
      <!-- Button to apply for the job -->
      <div class="action-buttons">
        <button class="btn-primary" @click="applyNow">Apply Now</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // Expects a `job` object as a prop
  props: {
    job: Object,
  },
  methods: {
    // Emits an event when the "Apply Now" button is clicked
    applyNow() {
      this.$emit("apply");
    },
  },
};
</script>

<style scoped>
/* Modal overlay for focus on the modal */
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7); 
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  animation: fade-in 0.4s ease-in-out;
}

/* Modal container with rounded corners and shadow */
.modal-content {
  background: linear-gradient(135deg, #ffffff, #f5f5f5);
  border-radius: 20px;
  padding: 40px;
  width: 600px;
  max-width: 90%;
  box-shadow: 0 15px 50px rgba(0, 0, 0, 0.2);
  position: relative;
  animation: slide-in 0.5s ease-out;
  overflow: hidden;
}

/* Decorative circle styling for modal */
.circle {
  position: absolute;
  width: 150px;
  height: 150px;
  border-radius: 50%;
  z-index: 0;
  opacity: 0.2;
}

/* Top decorative circle */
.circle-top {
  background: radial-gradient(circle, #ff9a9e, #fad0c4);
  top: -50px;
  right: -50px;
}

/* Bottom decorative circle */
.circle-bottom {
  background: radial-gradient(circle, #a18cd1, #fbc2eb);
  bottom: -50px;
  left: -50px;
}

/* Text container for job details */
.details {
  position: relative;
  z-index: 1;
  margin-bottom: 30px;
}

/* Job information paragraphs */
.info p {
  font-size: 1.2rem;
  margin: 12px 0;
  color: #7f8c8d;
}

/* Labels for company and location */
.label {
  font-weight: bold;
  color: #2980b9;
}

/* Description box styling */
.description p {
  font-size: 1.1rem;
  line-height: 1.6;
  text-align: justify;
  background: #ecf0f1;
  padding: 15px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

/* Close button for modal */
.close-btn {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  font-size: 2rem;
  cursor: pointer;
  transition: transform 0.3s ease, color 0.3s ease;
  z-index: 2;
}

/* Close button hover effects */
.close-btn:hover {
  color: #e74c3c;
  transform: rotate(90deg);
}

/* Header styling for the job title */
.header {
  text-align: center;
  padding: 15px 20px;
  margin-bottom: 30px;
  transform: scale(1);
  transition: transform 0.3s ease-in-out;
}

.header:hover {
  transform: scale(1.05);
}

/* Title text in uppercase with bold and spacing */
.header h2 {
  font-size: 1.5rem;
  font-weight: 700;
  margin: 0;
  text-transform: uppercase;
  letter-spacing: 2px;
}

/* Container for action buttons */
.action-buttons {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

/* Apply button with gradient background */
.btn-primary {
  background: linear-gradient(135deg, #8e44ad, #3498db);
  color: white;
  padding: 15px 30px;
  border: none;
  border-radius: 25px;
  font-size: 1.2rem;
  font-weight: bold;
  cursor: pointer;
  transition: background 0.3s ease, transform 0.2s ease, box-shadow 0.3s ease;
}

/* Hover effects for apply button */
.btn-primary:hover {
  background: linear-gradient(135deg, #3498db, #8e44ad);
  box-shadow: 0 8px 20px rgba(142, 68, 173, 0.5);
  transform: translateY(-3px);
}

/* Active state for apply button */
.btn-primary:active {
  transform: translateY(0);
  box-shadow: none;
}
</style>
