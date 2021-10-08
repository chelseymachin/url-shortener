<template>
  <div>
    <div id="inputContainer">
      <input type="text" placeholder="Paste your URL here" ref="input" @focus="resetInput"/>
      <button @click='click'>
        Shorten It!
      </button>
    </div>
    <div id="resultsContainer">
      <textarea v-model="shortenedUrl" rows="6" cols="63"/>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
const BITLY_API_KEY = "b52bd0bb77e9ff76755cfd5c7d171663621da4b9";

export default {
  name: 'url-shortener',
  props: {
    msg: String,
  },
  emits: [
    'click'
  ],
  data () {
    return {
      shortenedUrl: 'example',
      originalUrl: ''
    }
  },
  setup () {
    const input = ref(null)

    return {
      input
    }
  },
  methods: {
    click() {
      if (this.input.value.length != 0) {
        this.originalUrl = this.input.value;
        this.resetInput();

        fetch('https://api-ssl.bitly.com/v4/shorten', {
          method: 'POST',
          headers: {
            'Authorization': `Bearer ${BITLY_API_KEY}`,
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({ "long_url": this.originalUrl, "domain": "bit.ly"})
        })
        .then(response => response.json())
        .then(data => {
          console.log(data);
          this.shortenedUrl = data.link;
        })
      } else {
        window.alert("Please enter a URL in need of shortening!");
      }
      
    },
    resetInput () {
      this.input.value = "";
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Arvo:wght@700&display=swap');
#inputContainer {
  display: flex;
  justify-content: center;
  width: 100%;
  height: auto;
}

#inputContainer > * {
  margin-right: 10px;
}


button {
  font-family: 'Arvo', serif;
  font-size: 1.3rem;
  background-color: #16B4F2;
  color: #FEFBE9;
  padding: .5rem;
  border-radius: 10px;
  border-color: #16B4F2;
}

input {
  font-size: 1.3rem;
  width: 20rem;
  border: #0D0D0D 2px solid;
  border-radius: 10px;
}

textarea {
  border: #0D0D0D 2px solid;
  border-radius: 10px;
}

#resultsContainer {
  margin-top: 20px;
}
</style>
