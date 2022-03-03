<template>
  <br />
  <div class="container card">
    <label for="text" class="City">Enter your country</label>
    <div class="input-group mb-3">
      <input
        type="text"
        class="form-control rounded"
        placeholder="region"
        aria-label="Recipient's username"
        aria-describedby="button-addon2"
        v-model.trim="queryIP"
        @keyup.enter="newAdd"
      />

      <button
        class="btn btn-outline-primary"
        type="button"
        id="button-addon2"
        @click="newAdd"
      >
        Click me
      </button>
    </div>
  </div>

  <!-- loaded -->
  <div v-if="showLoaded" class="lds-spinner">
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
  </div>

  <div v-if="showText" class="container card-group pt-5">
    <div class="card m-2">
      <p>NAME:</p>
      <h2 v-if="this.name !== ''">
        <li v-for="item in data" :key="item.name">{{ item.name }}</li>
      </h2>
      <div v-else class="lds-ring">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>
    </div>
    <div class="card m-2">
      <p>DOMAINS:</p>
      <h2 v-if="this.domains !== ''">
        <li v-for="item in data" :key="item.domains">{{ item.domains }}</li>
      </h2>
      <div v-else class="lds-ring">
        <div></div>
        <div></div>
        <div></div> 
        <div></div>
      </div>
    </div>
    <div class="card m-2">
      <p>COUNTRY:</p>
      <h2 v-if="this.country !== ''">
        <li v-for="item in data" :key="item.country">{{ item.country }}</li>
      </h2>
      <div v-else class="lds-ring">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>
    </div>
  </div>
</template>


<script>
import axios from "axios";
export default {
  name: 'App',
  methods: {
    async newAdd() {
      this.saveData()
      this.showLoaded = !this.showLoaded
      this.showText = !this.showText

      this.queryIP = ""
    },

    async saveData() {
      try {
        const getIp = await axios
          .get(`http://universities.hipolabs.com/search?country=${this.queryIP}`)
          .then(res => {
            this.data = res.data
            this.name = res.data.name
            this.domains = res.data.domains
            this.country = res.data.country
            console.log(this.data)
          });
      } catch (error) {
        console.log(error);
      }
    },
  },

  data() {
    return {
      name: '',
      domains: '',
      country: '',
      showText: false,
      showLoaded: true,
      queryIP: "",
      data: []
    };
  },
};
</script>

