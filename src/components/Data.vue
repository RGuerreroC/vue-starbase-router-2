<template>
  <div class="col-md-12">
    <div class="card-columns">
      <Item
        v-for="(item, index) in items"
        :key="index"
        :passedItem="item"
        :type="type"
      />
    </div>
  </div>

</template>

<script>
import Item from './Item.vue'

export default {
  data() {
    return {
      type: this.$route.params.type,
      items: []
    };
  },
  watch: {
    '$route': 'fetchItems'
  },
  methods: {
    fetchItems() {
      this.items = []
      this.type = this.$route.params.type
      let initials_ids = [1, 13, 14]

      for (let i in initials_ids) {
        let id = initials_ids[i]
        fetch(`https://swapi.co/api/${this.type}/${id}`, {
          method: "GET"
        })
        .then(response => response.json())
        .then(json => this.items.push(json));
      }
    }
  },
  created() {
    this.fetchItems()
  },
  components: {
    Item
  }
};
</script>

