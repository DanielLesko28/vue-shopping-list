<template>
  <div id="app">

  <div class="content">
  <div class="header">
    <h1>{{ header }}</h1>
    <div class="buttons">
      <button class="addBtn" v-if="state === 'default'" @click="changeState('edit')">Add Item to List</button>
      <button class="cancelBtn" v-else @click="changeState('default')">Cancel</button>
    </div>
  </div>


  <div v-if="state === 'edit'">
    <input v-model="newItem" type="text" placeholder="Add a product" @keyup.enter="saveItem" />
    <p>{{ characterCount }}/200</p>
    <button @click="saveItem" :disabled="newItem.length === 0">Save Item</button>
  </div>
    <ul>
      <li v-for="(product, index) in products" :key="index" :class="{strikeout: product.purchased}" @click="togglePurchased(product)">{{ product.label }}</li>
    </ul>

    <p v-if="products.length === 0">Nice, You have empty shopping list</p>
  </div>

  </div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return {
      products: [
        {
          label:"2 hams",
          purchased: false,
        },
        {
          label:"3 carrots",
          purchased: false,
        },
        {
          label: "1 bread",
          purchased: true,
        },
      ],
      newItem: '',
      state: 'default',
    }
  },
  props:{
    header:{
      type: String,
      default: "Shopping List"
    }
  },
  computed:{
    characterCount(){
      return this.newItem.length
    }
  },
  methods: {
    saveItem(){
      this.products.push({
                    label:this.newItem,
                    purchased: false
                  })
      this.newItem = ''
    },
    changeState(newState){
      this.state = newState
      this.newItem = ''
    },
    togglePurchased(product){
      product.purchased = !product.purchased
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  justify-content: center;
  align-items: center;
}

li {
  list-style: none;
}

.content{
  width: 600px;
}

.header{
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: column;
}

.buttons{
  padding: 20px;
  margin-bottom: 1rem;
  margin: 10px;
}

.addBtn{
  padding: 10px;
  border-radius: 5px;
  background-color: green;
  color: white;
}

.cancelBtn{
  padding: 10px;
  border-radius: 5px;
  background-color: red;
  color: white;
}

.strikeout{
  text-decoration-line: line-through;
}

</style>
