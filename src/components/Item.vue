<template>
  <div class="card bg-dark border-info text-left mb-3" @click="switchItem">
    <div class="card-body">
      <h4 class="card-title">{{item.name}}</h4>
      <div v-for="(value, key, index) in item">
        <div v-if="index < 5">
          <strong>{{ key | capitalize | noUnders }}</strong>: {{ value }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['passedItem', 'type'],
  data() {
    return {
      item: {}
    }
  },
  methods: {
    switchItem() {
      let random_id = Math.floor(Math.random() * 83) + 1;
      fetch(`https://swapi.co/api/${this.type}/${random_id}`, {
          method: "GET"
        })
        .then(response => response.json())
        .then(json => this.item = json);
    }
  },
  created() {
    this.item = this.passedItem
  },
  filters: {
    capitalize: function(s) {
      return s[0].toUpperCase() + s.slice(1)
    },
    noUnders: function(s) {
      return s.replace('_', ' ')
    }
  }
}
</script>
