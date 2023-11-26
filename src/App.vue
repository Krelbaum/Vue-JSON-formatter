<template>
    <header class="header">
      <nav>
        <ul class="nav" style="margin: 0">
          <img src="/src/styles/images/jsoFormatterFavicon.svg"
              alt="" style="
              background-color: white;
              width: 50px;
              height: 50px;"/>
        </ul>
        <h1 class="text-header">My JSONFormatter</h1>
      </nav>
    </header>
    <div class="container">
      <div class="json-formatter">
        <textarea
            class="json-input"
            v-model="jsonInput"
            placeholder="Enter JSON here"
        ></textarea>
        <div class="button-container">
          <button @click="formatJSON" class="format-button">Format</button>
          <div class="toggle-buttons">
            <button @click="toggleFormat('short')" :class="{ active: format === 'short' }">Short</button>
            <button @click="toggleFormat('long')" :class="{ active: format === 'long' }">Long</button>
          </div>
        </div>
        <div class="formatted-json">
          <pre v-if="formattedJSON">{{ formattedJSON }}</pre>
          <p v-else class="error-message">{{ errorMessage }}</p>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      jsonInput: '',
      formattedJSON: '',
      errorMessage: '',
      format: 'short' // format po defoltu
    };
  },
  methods: {
    formatJSON() {
      try {
        const parsedJSON = JSON.parse(this.jsonInput);
        this.formattedJSON = this.format === 'long'
            ? JSON.stringify(parsedJSON, null, 4)
            : JSON.stringify(parsedJSON);
        this.errorMessage = '';
      } catch (error) {
        this.errorMessage = 'Invalid JSON format';
        this.formattedJSON = '';
      }
    },
    toggleFormat(type) {
      this.format = type;
      if (this.formattedJSON) {
        this.formatJSON();
      }
    }
  }
};
</script>
<style scoped>
.container
{
  height: 100vh;
}
.header{
  margin: 0;
  background-color: rgba(60, 69, 67, 0.6);
}
.text-header{
  text-align:center;
}
.json-formatter {
  max-width: 600px;
  margin: 0 auto;
}
.json-input {
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  margin-top: 6px;
  margin-bottom: 16px;
  resize: vertical;
}
.format-button {
  background-color: rgba(204, 3, 35, 0.5);
  box-shadow: rgba(60, 69, 67, 0.6) 5px 5px;
  padding: 8px 16px;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.formatted-json pre {
  padding: 10px;
  border-radius: 4px;
  white-space: pre-wrap;
  background-color: orangered;
}
.error-message {
  color: red;
  font-weight: bold;
  margin-top: 5px;
}
.toggle-buttons {
  margin-top: 10px;
}
.toggle-buttons button {
  padding: 8px 16px;
  margin-right: 10px;
  background-color: rgba(204, 3, 35, 0.5);
  box-shadow: rgba(60, 69, 67, 0.6) 5px 5px;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.toggle-buttons button.active {
  background-color: greenyellow;
  color: white;
}
</style>