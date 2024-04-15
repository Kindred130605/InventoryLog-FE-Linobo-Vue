<template>
	<div class="container">
	  <!-- Delete Records Title -->
	  <h2 class="delete-title">Delete Records</h2>
	  
	  <!-- Display Records -->
	  <div v-if="inventory.length" class="inventory-list">
		<ul class="list-group">
		  <li v-for="(item, index) in inventory" :key="index" class="list-group-item">
			<button @click="deleteItem(index)" class="delete-button">Delete</button>
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
  const inventory = ref<InventoryItem[]>([
	{ name: 'Item 1', quantity: 10, description: 'Description for Item 1' },
	{ name: 'Item 2', quantity: 20, description: 'Description for Item 2' },
	{ name: 'Item 3', quantity: 30, description: 'Description for Item 3' }
  ]);
  
  // Function to delete item
  const deleteItem = (index: number) => {
	inventory.value.splice(index, 1);
  };
  </script>
  
  <style scoped>
  body {
	margin: 0;
	padding: 0;
	font-family: 'Arial', sans-serif;
  }
  
  .container {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	min-height: 100vh;
	padding: 20px;
	background-color: #f4f4f4;
  }
  
  .delete-title {
	color: #dc3545;
	margin-bottom: 1rem;
  }
  
  .inventory-list {
	width: 100%;
	max-width: 800px;
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
  
  .delete-button {
	background-color: #dc3545;
	color: #fff;
	border: none;
	border-radius: 4px;
	padding: 0.5rem;
	cursor: pointer;
	margin-right: 1rem;
  }
  
  .item-info {
	flex-grow: 1;
  }
  </style>
  