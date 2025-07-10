<template>
  <result
    v-if="showResult"
    :items="items"
    @go-back="clearform"
  />

  <div
    v-else
    class="min-h-screen flex flex-col justify-center items-center bg-gray-50 p-6"
  >
    <div
      class="bg-white p-8 rounded-lg shadow-md w-full max-w-md"
    >
      <h2 class="text-2xl font-semibold mb-6 text-center text-teal-700">
        Add Sales Item
      </h2>

      <input
        v-model="name"
        type="text"
        placeholder="Customer Name"
        class="w-full p-3 mb-4 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-teal-400"
      />

      <input
        v-model="number"
        type="number"
        placeholder="Customer Number"
        class="w-full p-3 mb-4 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-teal-400"
      />

      <input
        v-model="served"
        type="text"
        placeholder="Served by"
        class="w-full p-3 mb-4 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-teal-400"
      />

      <input
        v-model="itemDescription"
        type="text"
        placeholder="Item Description"
        class="w-full p-3 mb-4 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-teal-400"
      />

      <div class="flex gap-4 mb-4">
        <input
          v-model.number="quantity"
          type="number"
          placeholder="Quantity"
          class="flex-1 p-3 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-teal-400"
        />
        <input
          v-model.number="price"
          type="number"
          placeholder="Price"
          class="flex-1 p-3 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-teal-400"
        />
      </div>

      <div class="flex gap-4 mb-6">
        <input
          v-model.number="discount"
          type="number"
          placeholder="Discount"
          class="flex-1 p-3 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-teal-400"
        />
        <input
          v-model.number="paid"
          type="number"
          placeholder="Paid"
          class="flex-1 p-3 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-teal-400"
        />
        <input
          v-model.number="balance"
          type="number"
          placeholder="Balance"
          class="flex-1 p-3 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-teal-400"
        />
      </div>

      <div class="flex justify-between">
        <button
          class="bg-green-600 hover:bg-green-700 transition text-white py-3 px-6 rounded shadow"
          @click="addItem"
        >
          Add Item
        </button>

        <button
          class="bg-blue-600 hover:bg-blue-700 transition text-white py-3 px-6 rounded shadow"
          @click="submitForm"
        >
          Submit All
        </button>
      </div>
    </div>
  </div>
</template>


<script>
import result from './components/result.vue';

export default {
  name: 'App',
  components: { result },
  data() {
    return {
      itemDescription: '',
      name: '',
      served: '',
      number: null,
      quantity: null,
      price: null,
      discount: null,
      balance: null,
      paid: null,
      subtotal: null,
      tax: null,
      items: [],
      showResult: false,
    };
  },
  methods: {
    addItem() {
      if (!this.itemDescription || this.quantity <= 0 || this.price <= 0) {
        alert("Please fill all fields correctly.");
        return;
      }

      const item = {
        description: this.itemDescription,
        quantity: this.quantity,
        price: this.price,
        discount: this.paid - this.discount,
        paid: this.paid,
        balance: this.balance,
        name: this.name,
        served: this.served,
        total: this.quantity * this.price,
        number: this.number,
      };

      this.items.push(item);

      // clear form
      this.itemDescription = '';
      this.name = '';
      this.quantity = null;
      this.price = null;
      this.price = null;
      this.discount = null;
      this.subtotal = null;
      this.tax = null;
      this.balance = null;
      this.paid = null;
      this.number = null;
      this.served = '';
    },
    submitForm() {
      if (this.items.length === 0) {
        alert("Please add at least one item before submitting.");
        return;
      }
      this.showResult = true;
    },
    clearform() {
       this.items = [];
      this.showResult = false;
    }
  },
  };
</script>
