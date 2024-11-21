<template>
  <footer class="footer">
    <!-- Footer container with text centered -->
    <div class="container text-center">
      <p>
        &copy; 2024 <strong>Job Portal</strong>. All rights reserved.
      </p>
      <p>
        <span class="text-highlight">Developed by</span>
        <span class="developer-name">Akshata Bhomkar</span>
      </p>
    </div>
  </footer>
</template>

<style>
/* Footer main styles with gradient background and rounded corners */
.footer {
  background: linear-gradient(135deg, #4c8bf5, #4adede);
  color: white;
  padding: 40px 0;
  border-top-left-radius: 50px;
  border-top-right-radius: 50px;
  text-align: center;
  box-shadow: 0 -4px 10px rgba(0, 0, 0, 0.1);
  position: relative;
  overflow: hidden;
}

/* Decorative gradient circles in the footer background */
.footer::before,
.footer::after {
  content: "";
  position: absolute;
  width: 200px;
  height: 200px;
  background: radial-gradient(circle, #ff9a9e, #fad0c4);
  border-radius: 50%;
  opacity: 0.4;
  z-index: 0;
}

/* Top-left decorative circle */
.footer::before {
  top: -40px;
  left: -40px;
}

/* Bottom-right decorative circle */
.footer::after {
  bottom: -40px;
  right: -40px;
}

/* General paragraph styling for footer text */
.footer p {
  font-size: 1.2rem;
  margin: 10px 0;
  color: white;
  position: relative;
  z-index: 1;
}

/* Highlighted text styling (e.g., "Developed by") */
.text-highlight {
  color: #fff;
  font-weight: 400;
}

/* Developer name styled like a button */
.developer-name {
  display: inline-block;
  background: linear-gradient(135deg, #ff7eb3, #ff758c);
  color: white;
  font-weight: bold;
  padding: 5px 15px;
  border-radius: 20px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  margin-left: 10px;
  position: relative;
  overflow: hidden;
  transition: transform 0.3s ease, box-shadow 0.3s ease, background 0.3s ease;
  vertical-align: middle;
}

/* Hover effect for developer name */
.developer-name:hover {
  transform: translateY(-3px) scale(1.1);
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.2);
  background: linear-gradient(135deg, #ff758c, #ff7eb3);
}

/* Decorative golden glow on the left of developer name */
.developer-name::before {
  content: "";
  position: absolute;
  width: 60px;
  height: 60px;
  background: radial-gradient(circle, #f39c12, transparent);
  border-radius: 50%;
  opacity: 0.4;
  top: -10px;
  left: -15px;
  transition: all 0.3s ease;
}

/* Decorative red glow on the right of developer name */
.developer-name::after {
  content: "";
  position: absolute;
  width: 60px;
  height: 60px;
  background: radial-gradient(circle, #e74c3c, transparent);
  border-radius: 50%;
  opacity: 0.4;
  bottom: -10px;
  right: -15px;
  transition: all 0.3s ease;
}

/* Hover effect for the decorative elements */
.developer-name:hover::before,
.developer-name:hover::after {
  transform: scale(1.2);
  opacity: 0.6;
}
</style>
