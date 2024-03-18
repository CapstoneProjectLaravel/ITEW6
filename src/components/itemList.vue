<template>
  <div class="item-list">
    <div v-for="(item, index) in items" :key="index" class="item">
      <div class="item-details">
        <p class="item-name">{{ item.name }}</p>
        <p class="item-price">$ {{ item.price }}</p>
      </div>
      <div class="button-group">
        <button @click="addToCart(item)" class="add-to-cart-btn">Add to Cart</button>
        <button @click="updateItem(index)" class="update-btn">Update</button>
        <button @click="removeItem(index)" class="remove-btn">Remove</button>
      </div>
    </div>
    <button @click="addItem" class="add-item-btn">Add New Item</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { name: 'Item 1', price: 10 },
        { name: 'Item 2', price: 20 },
        { name: 'Item 3', price: 15 },
        { name: 'Item 4', price: 11 },
        { name: 'Item 5', price: 32 },
        { name: 'Item 6', price: 23 }
      ]
    };
  },
  methods: {
    addToCart(item) {
      this.$emit('add-to-cart', item);
    },
    updateItem(index) {
      const item = this.items[index];
      const newName = prompt('Enter the new name:', item.name);
      const newPrice = parseFloat(prompt('Enter the new price:', item.price));
      
      if (newName && !isNaN(newPrice)) {
        item.name = newName;
        item.price = newPrice;
      }
    },
    removeItem(index) {
      this.items.splice(index, 1);
    },
    addItem() {
      const name = prompt('Enter the name for the new item:');
      const price = parseFloat(prompt('Enter the price for the new item:'));
      
      if (name && !isNaN(price)) {
        this.items.push({ name, price });
      }
    }
  }
};
</script>

<style scoped>
.item-list {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20px;
}

.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #ccc;
  width: 80%;
}

.item-details {
  flex: 1;
}

.item-name {
  margin: 0;
  font-weight: bold;
}

.item-price {
  margin: 0;
}

.button-group {
  display: flex;
  gap: 10px;
}

.add-to-cart-btn, .update-btn, .remove-btn, .add-item-btn {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.add-to-cart-btn:hover, .update-btn:hover, .remove-btn:hover, .add-item-btn:hover {
  background-color: #45a049;
}
</style>
