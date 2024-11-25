<template>
  <div class="modal">
    <div class="modal-content">
      <button class="close-btn" @click="$emit('close')">&times;</button>
      <div class="header">
        <h2>{{ job.title }}</h2>
      </div>
      <div class="details">
        <div class="circle circle-top"></div>
        <div class="info">
          <p><span class="label">Company:</span> {{ job.company }}</p>
          <p><span class="label">Location:</span> {{ job.location }}</p>
        </div>
        <div class="circle circle-bottom"></div>
        <div class="circle circle-bottom-right"></div>
        <div class="description">
          <p><strong>Details:</strong> {{ job.detailedDescription }}</p>
          <p><strong>Requirements:</strong></p>
          <ul>
            <li v-for="(req, index) in job.requirements" :key="index">{{ req }}</li>
          </ul>
          <p><strong>Basic Information:</strong></p>
          <ul>
            <li><strong>Salary:</strong> {{ job.salary }}</li>
            <li><strong>Type:</strong> {{ job.type }}</li>
            <li><strong>Remote:</strong> {{ job.remote }}</li>
          </ul>
        </div>
      </div>
      <div class="action-buttons">
        <button class="btn-primary" @click="applyNow">Apply Now</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    job: Object,
  },
  methods: {
    applyNow() {
      this.$emit('apply');
      this.$emit('close');
    },
  },
};
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(8px); 
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  animation: fade-in 0.4s ease-in-out;
}

.modal-content {
  background: linear-gradient(135deg, #ffffff, #f5f5f5);
  border-radius: 40px; 
  padding: 40px;
  width: 600px;
  max-width: 90%;
  box-shadow: 0 15px 50px rgba(0, 0, 0, 0.2);
  position: relative;
  animation: slide-in 0.5s ease-out;
  overflow: hidden;
}

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

.details {
  position: relative;
  z-index: 1;
  margin-bottom: 30px;
}

.info p {
  font-size: 1.2rem;
  margin: 12px 0;
  color: #7f8c8d;
}

.label {
  font-weight: bold;
  color: #2980b9;
}

.description ul {
  padding-left: 20px;
  margin: 10px 0;
}

.description ul li {
  margin-bottom: 10px;
  font-size: 1.1rem;
  color: #7f8c8d;
  line-height: 1.6;
}

.description p {
  font-size: 1.1rem;
  line-height: 1.6;
  text-align: justify;
  background: #ecf0f1;
  padding: 15px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.close-btn {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  font-size: 2rem;
  cursor: pointer;
  color: #e74c3c;
  transition: transform 0.3s ease, color 0.3s ease;
  z-index: 2;
}

.close-btn:hover {
  color: #c0392b;
  transform: rotate(90deg);
}

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

.header h2 {
  font-size: 1.5rem;
  font-weight: 700;
  margin: 0;
  text-transform: uppercase;
  letter-spacing: 2px;
}

.action-buttons {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

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

.btn-primary:hover {
  background: linear-gradient(135deg, #3498db, #8e44ad);
  box-shadow: 0 8px 20px rgba(142, 68, 173, 0.5);
  transform: translateY(-3px);
}

.btn-primary:active {
  transform: translateY(0);
  box-shadow: none;
}

@keyframes fade-in {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes slide-in {
  from {
    transform: translateY(-10px);
  }
  to {
    transform: translateY(0);
  }
}
</style>
