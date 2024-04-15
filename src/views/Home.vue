<template>
	<div class="container">
	  <!-- Add Records Title -->
	  <h2 class="add-title">Add Records</h2>
  
	  <!-- Add Record Form -->
	  <form @submit.prevent="addItem" class="form">
		<div class="form-group">
		  <label for="itemName">Item Name:</label>
		  <input type="text" id="itemName" v-model="itemName" required />
		</div>
		
		<div class="form-group">
		  <label for="quantity">Quantity:</label>
		  <input type="number" id="quantity" v-model.number="quantity" required />
		</div>
		
		<div class="form-group">
		  <label for="description">Description:</label>
		  <textarea id="description" v-model="description"></textarea>
		</div>
		
		<button type="submit" class="add-button">Add Item</button>
	  </form>
  
	  <!-- Display Records -->
	  <div v-if="inventory.length" class="inventory-list">
		<h2 class="list-title">Inventory List</h2>
		<ul class="list-group">
		  <li v-for="(item, index) in inventory" :key="index" class="list-group-item">
			<div class="item-info">
			  <strong>{{ item.name }}</strong>
			  <p>Quantity: {{ item.quantity }}</p>
			  <p>Description: {{ item.description }}</p>
			</div>
		  </li>
		</ul>
	  </div>
	</div>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue';
  
  // Define inventory item type
  type InventoryItem = {
	name: string;
	quantity: number;
	description: string;
  };
  
  // Reactive references
  const itemName = ref('');
  const quantity = ref(0);
  const description = ref('');
  const inventory = ref<InventoryItem[]>([]);
  
  // Function to add item
  const addItem = () => {
	// Create new item object
	const newItem: InventoryItem = {
	  name: itemName.value,
	  quantity: quantity.value,
	  description: description.value
	};
  
	// Add item to inventory
	inventory.value.push(newItem);
  
	// Clear form fields
	itemName.value = '';
	quantity.value = 0;
	description.value = '';
  };
  
  </script>
  
  <style scoped>
  .container {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	min-height: 100vh;
	padding: 20px;
	background-color: #f4f4f4;
  }
  
  .add-title,
  .list-title {
	color: #007BFF;
	margin-bottom: 1rem;
  }
  
  .form {
	width: 100%;
	max-width: 400px;
  }
  
  .form-group {
	margin-bottom: 1rem;
  }
  
  label {
	display: block;
	margin-bottom: 0.5rem;
	color: #333;
  }
  
  input[type="text"],
  input[type="number"],
  textarea {
	width: 100%;
	padding: 0.5rem;
	border-radius: 4px;
	border: 1px solid #ccc;
  }
  
  .add-button,
  .delete-button {
	width: 100%;
	padding: 0.5rem;
	background-color: #007BFF;
	color: #fff;
	border: none;
	border-radius: 4px;
	cursor: pointer;
  }
  
  .delete-button {
	background-color: #dc3545;
  }
  
  .inventory-list {
	margin-top: 2rem;
	width: 100%;
	max-width: 600px;
  }
  
  .list-group {
	list-style-type: none;
	padding: 0;
  }
  
  .list-group-item {
	display: flex;
	justify-content: flex-start;
	align-items: center;
	border: 1px solid #ccc;
	border-radius: 4px;
	margin-bottom: 0.5rem;
	padding: 1rem;
  }
  
  .item-info {
	flex-grow: 1;
  }
  </style>
  