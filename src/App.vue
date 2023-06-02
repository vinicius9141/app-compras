<template>
  <div class="container">
    <h1>Lista de Compras</h1>

    <form @submit.prevent="addItem" class="mainForm">
      <input v-model="newItem" placeholder="Nome do item" required />
      <input v-model.number="newPrice" placeholder="Preço" required />
      <button type="submit" class="buttonAdd">Adicionar</button>
    </form>

    <ul class="listItems">
      <li v-for="(item, index) in items" :key="index">
        <p>{{ item.name }}</p>
        -
        <p>R${{ item.price }}</p>
      </li>
    </ul>

    <p class="totalPrice">Total: R$ {{ calculateTotal() }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newItem: '',
      newPrice: 0,
      items: [],
    }
  },
  methods: {
    addItem() {
      this.items.push({ name: this.newItem, price: this.newPrice })
      this.newItem = ''
      this.newPrice = 0
    },
    calculateTotal() {
      return this.items.reduce((total, item) => total + item.price, 0)
    },
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  background-color: #e2e2e2;
  font-family: sans-serif;
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.mainForm {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.mainForm input {
  margin: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
.buttonAdd {
  margin: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #008000;
  color: #fff;
}
ul {
  list-style: none;
  height: 300px;
  width: 200px;
  overflow: scroll;
  border: 1px solid red;
}
li {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  gap: 10px;
  width: 200px;
  min-width: 100%;
  padding: 10px;
  border-bottom: 1px solid green;
}
</style>
