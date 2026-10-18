<template>
  <div class="container">
    <h2>W3Schools Alapú Feladat: Bevásárlólista Kezelő</h2>
    
    <!-- Forms témakör demonstrációja -->
    <form @submit.prevent="addItem" class="form-box">
      <div class="input-group">
        <label for="itemName">Termék neve:</label>
        <input 
          id="itemName"
          type="text" 
          v-model="itemName" 
          placeholder="Pl. Paradicsom" 
          required
        >
      </div>

      <div class="input-group">
        <label for="itemQty">Mennyiség:</label>
        <input 
          id="itemQty"
          type="number" 
          v-model.number="itemNumber" 
          placeholder="Pl. 5"
          min="1"
          required
        >
      </div>

      <button type="submit">Elem hozzáadása</button>
    </form>

    <div class="list-box">
      <h3>Aktuális lista ({{ itemCount }} elem):</h3>
      <p v-if="shoppingList.length === 0">A lista még üres.</p>
      <ul>
        <li v-for="(item, index) in shoppingList" :key="index">
          {{ item.name }} - {{ item.number }} db
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
 
  data() {
    return {
      itemName: '',
      itemNumber: null,
      shoppingList: [
        { name: 'Paradicsom', number: 5 }
      ]
    }
  },
  computed: {
    itemCount() {
      return this.shoppingList.length;
    }
  },
  // Methods témakör demonstrációja 
  methods: {
    addItem() {
      const newItem = {
        name: this.itemName,   
        number: this.itemNumber
      };

      // Hozzáadás a tömbhöz
      this.shoppingList.push(newItem);

      // Űrlapmezők alaphelyzetbe állítása
      this.itemName = '';
      this.itemNumber = null;
    }
  }
}
</script>

<style scoped>
.container {
  max-width: 500px;
  margin: 40px auto;
  font-family: Arial, sans-serif;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  background-color: #fff;
}
h2 {
  color: #42b883;
  text-align: center;
}
.form-box {
  background: #f4f4f4;
  padding: 15px;
  border-radius: 6px;
  margin-bottom: 20px;
}
.input-group {
  margin-bottom: 10px;
}
.input-group label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}
.input-group input {
  width: 95%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
button {
  background-color: #42b883;
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  width: 100%;
  font-size: 16px;
}
button:hover {
  background-color: #35495e;
}
.list-box {
  border-top: 1px solid #eee;
  padding-top: 15px;
}
ul {
  list-style-type: square;
  padding-left: 20px;
}
li {
  padding: 5px 0;
}
</style>
