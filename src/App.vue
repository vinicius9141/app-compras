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
        <p>R$ {{ item.price.toFixed(2) }}</p>
        <button @click="removeItem(index)" class="btnRemove">Remover</button>
      </li>
    </ul>

    <p class="totalPrice">👉 Total: R$ {{ calculateTotal().toFixed(2) }} 👈</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newItem: '',
      newPrice: 0,
      items: []
    };
  },
  mounted() {
    this.loadItemsFromLocalStorage();
  },
  methods: {
    addItem() {
      this.items.push({ name: this.newItem, price: this.newPrice });
      this.newItem = '';
      this.newPrice = 0;
      this.saveItemsToLocalStorage();
    },
    removeItem(index) {
      this.items.splice(index, 1);
      this.saveItemsToLocalStorage();
    },
    calculateTotal() {
      return this.items.reduce((total, item) => total + item.price, 0);
    },
    saveItemsToLocalStorage() {
      localStorage.setItem('items', JSON.stringify(this.items));
    },
    loadItemsFromLocalStorage() {
      const storedItems = localStorage.getItem('items');
      if (storedItems) {
        this.items = JSON.parse(storedItems);
      }
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #acb3ff;
  font-family: sans-serif;
}

.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.title {
  font-size: 2rem;
  text-align: center;
  padding: 10px;
  font-weight: 300;
  margin-bottom: 2vw;
}

.mainForm {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.mainForm input {
  padding: 20px 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.mainForm input:focus {
  outline: 2px solid blue;
}
.backgroundListItem {
  background: #acb3ff;
  height: 100%;
  border-radius: 8px;
}
.nameInput {
  width: 28vw;
}
.priceInput {
  width: 10vw;
}
.inputs {
  display: flex;
  flex-direction: row;
  gap: 15px;
}
.buttonAdd {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #008000;
  color: #fff;
  width: 35vw;
  height: 8vw;
  cursor: pointer;
}

.yourBag {
  color: #000;
  padding: 3px;
  width: 100%;
  text-align: center;
}

.listItems {
  list-style: none;
  height: 300px;
  width: 70vw;
  overflow: scroll;
  padding: 8px;
  border-radius: 8px;
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
.btnRemove{
  background-color: #6A041D;
  color: #fff;
  padding: 5px;
  border: none;  
  border-radius: 8px;
}
.totalPrice {
  margin-top: 10px;
  font-size: 1.5rem;
}

@media screen and (max-width: 768px) {
  li {
    width: 70vw;
  }
  .mainForm input {
    padding: 15px 10px;
  }
}
</style>
