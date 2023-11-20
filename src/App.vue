<template>
  <div class="json-formatter">
    <h2>JSON Formatter</h2>
    <textarea
        v-model="jsonInput"
        placeholder="Enter JSON here"
        class="json-input"
    ></textarea>
    <button @click="formatJSON" class="format-button">Format</button>
    <div class="formatted-json">
      <pre v-if="formattedJSON">{{ formattedJSON }}</pre>
      <p v-else class="error-message">{{ errorMessage }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      jsonInput: '',
      formattedJSON: '',
      errorMessage: ''
    };
  },
  methods: {
    formatJSON() {
      try {
        const parsedJSON = JSON.parse(this.jsonInput);
        this.formattedJSON = JSON.stringify(parsedJSON, null, 2);
        this.errorMessage = '';
      } catch (error) {
        this.errorMessage = 'Invalid JSON format';
        this.formattedJSON = '';
      }
    }
  }
};
</script>

<style scoped>
.json-formatter {
  max-width: 600px;
  margin: 0 auto;
  font-family: Arial, sans-serif;
}

.json-input {
  width: 100%;
  height: 150px;
  padding: 10px;
  margin-bottom: 15px;
  border: 1px solid lightgrey;
  border-radius: 4px;
  resize: vertical;
}

.format-button {
  padding: 8px 16px;
  background-color: blue;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.formatted-json pre {
  background-color: white;
  padding: 10px;
  border-radius: 4px;
  white-space: pre-wrap;
}

.error-message {
  color: red;
  font-weight: bold;
  margin-top: 5px;
}
</style>