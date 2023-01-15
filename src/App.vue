<script lang="ts">
import { Configuration, OpenAIApi } from "openai";

export default {
  data() {
    return {
      apiKey: "Insert api key here",
      prompt: "Write a prompt here",
      response: "openapi response here",
      // organization: "Insert organization code here",
    };
  },
  methods: {
    async submitPrompt() {
      const configuration = new Configuration({
        // organization: this.organization,
        apiKey: this.apiKey,
      });
      const openai = new OpenAIApi(configuration);
      try {
        const completion = await openai.createCompletion({
          model: "text-davinci-003",
          prompt: this.prompt,
          temperature: 0,
          max_tokens: 2048,
        });
        this.response = completion.data.choices[0].text || "no response";
        console.log(JSON.stringify(completion.data));
      } catch (error) {
        // @ts-ignore
        if (error.response) {
          // @ts-ignore
          console.log(error.response.status);
          // @ts-ignore
          console.log(error.response.data);
        } else {
          // @ts-ignore
          console.log(error.message);
        }
      }
    },
  },
};
</script>

<template>
  <header>
    <h2>api key here</h2>
    <input v-model="apiKey" />
    <!-- <h2>organization code here</h2>
    <input v-model="organization" /> -->
  </header>

  <main>
    <h2>prompt here</h2>
    <textarea v-model="prompt" />
    <button @click="submitPrompt">Submit Prompt</button>
  </main>
  <footer>
    <h2>response</h2>
    <textarea v-model="response" />
  </footer>
</template>

<style>
input {
  display: block;
  margin-bottom: 1em;
}
button {
  display: block;
  margin-bottom: 1em;
}
</style>
