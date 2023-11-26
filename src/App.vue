<template>

    <header class="header">
      <nav>
        <ul class="nav" style="margin: 0">
          <img
              src="/jsoFormatterFavicon.svg"
              alt="" style="background-color: white"/>
          <a class="common-button nav-item mx-1 border border-light rounded-pill btn btn-danger" href="/about_me/luke">Tutorials</a>
          <a class="common-button nav-item mx-1 border border-light rounded-pill btn btn-danger" href="/star_wars">Excercises</a>
          <a class="common-button nav-item mx-1 border border-light rounded-pill btn btn-danger" href="/contact">SignUp</a>
          <a class="common-button nav-item mx-1 border border-light rounded-pill btn btn-danger" href="/contact">LogIn</a>
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
    <footer class="rounded-bottom-4">
      <div className="nav-item btn btn-danger border border-light rounded-pill mx-1 common-button my-3">
        <p>Send me an <span className={style.email}>email</span></p>
      </div>

    </footer>

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
  //width: 100vw;
  font-family: 'Poller One', cursive;

}
.header{
  margin: 0;
  background-color: rgba(60, 69, 67, 0.6);



}
.nav{

}
.text-header{
  text-align:center;


}

.common-button
{
  cursor: url("styles/images/cursor_st_1.png"), auto;
  background-color: rgba(204, 3, 35, 0.5);
  box-shadow: rgba(60, 69, 67, 0.6) 5px 5px;
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

//height: 150px;
  //padding: 10px;
  //margin-bottom: 15px;
  //border: 1px solid lightgrey;
  //border-radius: 4px;
  //resize: vertical;
}
.format-button {
  background-color: rgba(204, 3, 35, 0.5);
  box-shadow: rgba(60, 69, 67, 0.6) 5px 5px;
  //padding: 8px 16px;
  //background-color: blue;
  //color: white;
  //border: none;
  //border-radius: 4px;
  //cursor: pointer;
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


.toggle-buttons {
  margin-top: 10px;
}

.toggle-buttons button {
  padding: 5px 10px;
  margin-right: 10px;
  border: 1px solid #007bff;
  background-color: transparent;
  color: #007bff;
  border-radius: 4px;
  cursor: pointer;
}

.toggle-buttons button.active {
  background-color: #007bff;
  color: white;
}
.footer
{
  background-color: rgba(60, 69, 67, 0.6);
}
</style>