<template>
  <div>
    <b-container>
      <b-list-group v-for="inventory in inventories " :key="inventory.id">
        <b-list-group-item> Name : {{inventory.name}}, Available Qty: {{inventory.available_qty}}</b-list-group-item>
      </b-list-group>
    </b-container>
  </div>

</template>

<script>
  export default {
    name: 'inventory',
    data: () => ({
      some_thing: {
        name: 'Cooper',
        desc: 'This can be any data'
      }
    }),
    computed: {
      inventories() {
        return this.$store.getters['inventory/GET_INVENTORIES']
      }
    },

    async fetch({store, $axios}) {
      const res = await $axios.get('http://localhost:5000/inventories');
      store.commit('inventory/SET_INVENTORIES', res.data);
    }
  }
</script>
