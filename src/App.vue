<template>
  <div v-if="showSuccess" class="alert-container success-container" role="alert">
    <svg aria-hidden="true" class="alert-svg" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
      <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd"></path>
    </svg>
    <div>
      <span class="font-medium">Success!</span> The webhook has been successfully deleted.
      <a @click="hideMessage('success')"><svg class="close-icon" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="gray">
        <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
      </svg></a>
    </div>
  </div>

  <div v-if="showError" class="alert-container error-container" role="alert">
    <svg aria-hidden="true" class="alert-svg" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
      <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd"></path>
    </svg>
    <div>
      <span class="font-medium">Error:</span> {{ errorMessage }}
      <a @click="hideMessage('error')"><svg class="close-icon" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="gray">
        <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
      </svg></a>
    </div>
  </div>

  <div class="content">
    <h1 class="webhook-deleter">ᴡᴇʙʜᴏᴏᴋ ɴᴜᴋᴇʀ/ᴅᴇʟᴇᴛᴇʀ</h1>
  </div>

 <label for="webhook-url" class="webhook-url-label">youtube.com/@XDash_o</label>

  <label for="webhook-url" class="webhook-url-label">ᴇɴᴛᴇʀ ᴡᴇʙʜᴏᴏᴋ ᴜʀʟ:</label>
  <div class="webhook-input">
    <input type="text" @input="handleInput" v-model="webhookurl" class="webhook-url-input-box" id="webhook-url" placeholder="discord.com/api/webhooks/...">
  </div>

  <div class="delete">
    <button @click="deleteWebhook" class="delete-btn">Delete</button>
  </div>

  <div class="footer">
    <p class="madewith-text">made by Dash.</p>
    <a href="https://github.com/1nOnlyDash">
      <img src="./assets/gh.svg" alt="github logo" class="gh-logo">
    </a>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: "App",
  data() {
    return {
      webhookurl: '',
      errorMessage: null,
      showSuccess: false,
      showError: false,
    };
  },

  methods: {
    deleteWebhook() {
      axios.delete(this.webhookurl)
        .then(() => {
          this.showMessage('success');
        })
        .catch((error) => {
          console.error(error);
          this.errorMessage = error.response ? error.response.data.message : 'An unexpected error occurred';
          this.showMessage('error');
        });
    },
    handleInput(event) {
      this.webhookurl = event.target.value;
    },
    showMessage(type) {
      if (type === 'success') {
        this.showSuccess = true;
        setTimeout(() => this.showSuccess = false, 3000);
      } else if (type === 'error') {
        this.showError = true;
        setTimeout(() => this.showError = false, 5000);
      }
    },
    hideMessage(type) {
      if (type === 'success') this.showSuccess = false;
      if (type === 'error') this.showError = false;
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap');

* {
  font-family: 'Inter', sans-serif;
}

body {
  background: linear-gradient(to right, rgb(249, 168, 212), rgb(216, 180, 254), rgb(129, 140, 248));
  background-size: 400% 400%;
  animation: gradient 15s ease infinite;
  height: 100vh;
}

@keyframes gradient {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

.webhook-deleter {
  text-align: center;
  padding-top: 10em;
}

.webhook-url-label {
  display: block;
  text-align: center;
}

.webhook-input {
  display: flex;
  justify-content: center;
  margin-top: 8px;
}

.webhook-url-input-box {
  width: 50%;
  padding: 10px;
  text-align: center;
  border-radius: 0.5rem;
  background: rgb(116, 164, 246);
  border: 1px solid transparent;
}

.delete {
  display: flex;
  justify-content: center;
  margin-top: 24px;
}

.delete-btn {
  padding: 10px 15px;
  background: rgb(237, 66, 69);
  border: none;
  color: white;
  font-weight: 600;
  border-radius: 0.5rem;
  cursor: pointer;
}

.delete-btn:hover {
  background: rgb(210, 58, 61);
}

.alert-container {
  display: flex;
  position: absolute;
  right: 0;
  padding: 1rem;
  border-radius: 0.5rem;
  margin: 0.5rem;
  width: 25%;
}

.success-container {
  background-color: #bbf7d0;
  color: #166534;
}

.error-container {
  background-color: #e13732;
  color: white;
}

.alert-svg {
  width: 1.25rem;
  height: 1.25rem;
  margin-right: 0.75rem;
}

.font-medium {
  font-weight: 700;
}

.close-icon {
  width: 1.5rem;
  height: 1.5rem;
  cursor: pointer;
}

.footer {
  padding-top: 20rem;
  text-align: center;
}

.gh-logo {
  height: 1.5rem;
  width: 1.5rem;
}
</style>
