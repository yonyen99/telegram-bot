<template>
  <div class="container">
    <form @submit.prevent="submitForm" class="mt-3">
      <div class="mb-3">
        <label for="fullname" class="form-label">Full Name</label>
        <input type="text" id="fullname" class="form-control" v-model="fullname" required />
      </div>
      <div class="mb-3">
        <label for="subject" class="form-label">Subject</label>
        <input type="text" id="subject" class="form-control" v-model="subject" required />
      </div>
      <div class="mb-3">
        <label for="message" class="form-label">Message</label>
        <textarea id="message" class="form-control" v-model="message" required></textarea>
      </div>
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      fullname: '',
      subject: '',
      message: '',
      chatId: 1498988407,
    };
  },
  methods: {
    async submitForm() {
      try {
        const telegramAPI = 'https://api.telegram.org/bot6325839849:AAEr7jAmX5kMoFWCq5Sgca6dUAOHZ6EOq4k/sendMessage';
        const message = `Name: ${this.fullname}\nSubject: ${this.subject}\nMessage: ${this.message}`;

        const response = await axios.post(telegramAPI, {
          chat_id: this.chatId,
          text: message,
        });

        if (response.data.ok) {
          alert('Message sent successfully!');
        } else {
          alert('Failed to send message. Please try again later.');
        }
      } catch (error) {
        console.error('Error sending message:', error);
        alert('Error sending message. Please try again later.');
      }
    },
  },
};
</script>
