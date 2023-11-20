<template>
  <div>
    <textarea v-model="jsonInput" placeholder="Enter JSON here"></textarea>
    <button @click="formatJSON">Format</button>
    <pre>{{ formattedJSON }}</pre>
  </div>
</template>

<script>
export default {
  data() {
    return {
      jsonInput: '',
      formattedJSON: ''
    };
  },
  methods: {
    formatJSON() {
      try {
        const parsedJSON = JSON.parse(this.jsonInput);
        this.formattedJSON = JSON.stringify(parsedJSON, null, 2);
      } catch (error) {
        this.formattedJSON = 'Invalid JSON format';
      }
    }
  }
};
</script>

<style>
textarea {
  width: 100%;
  height: 150px;
  margin-bottom: 10px;
}
button {
  padding: 8px 16px;
  background-color: blue;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
pre {
  background-color: lightgrey;
  padding: 10px;
  border-radius: 4px;
  white-space: pre-wrap;
}
</style>