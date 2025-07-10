<template>
  <div class="max-w-4xl mx-auto bg-white p-8 rounded-lg shadow-lg mt-8 mb-12 print:p-0 print:shadow-none print:rounded-none">
    <!-- Header: logo + title + date -->
    <header class="flex justify-between items-center border-b pb-4 mb-6">
      <div class="flex items-center gap-4">
        <img
          class="w-36 rounded"
          src="../assets/Black and Blue Mobile Phone Repair Logo.png"
          alt="Logo"
        />
        <div>
          <h1 class="text-3xl font-extrabold text-teal-700">SALES</h1>
          <p class="text-sm text-gray-600">
            {{data.month}} {{data.day}}, {{data.year}}
          </p>
        </div>
      </div>
    </header>

    <!-- Customer & billing info -->
    <section class="grid grid-cols-1 md:grid-cols-2 gap-8 mb-8 text-gray-700">
      <div>
        <h2 class="text-xl font-semibold text-teal-700 mb-2">AWOOWE ELECTRONICS</h2>
        <p>Soobe, Abdishideeye, Somalia</p>
        <p>0619538337</p>
      </div>
      <div>
        <h2 class="text-xl font-semibold text-teal-700 mb-2">Bill To</h2>
        <p class="font-semibold text-teal-600">{{items[0]?.name}}</p>
        <p>{{items[0]?.number}}</p>
      </div>
    </section>

    <!-- Items table -->
    <table class="w-full border border-gray-300 rounded mb-6 table-auto">
      <thead>
        <tr class="bg-teal-700 text-white text-left">
          <th class="px-4 py-2 border-r border-teal-600">#</th>
          <th class="px-6 py-3 border-r border-teal-600">Item Description</th>
          <th class="px-4 py-3 border-r border-teal-600">Quantity</th>
          <th class="px-4 py-3 border-r border-teal-600">Price</th>
          <th class="px-4 py-3">Total</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(item, index) in items"
          :key="index"
          class="border-b border-gray-300 hover:bg-gray-50 transition"
        >
          <td class="px-4 py-2 align-top">{{ index + 1 }}</td>
          <td class="px-6 py-2 font-semibold align-top">{{ item.description }}</td>
          <td class="px-4 py-2 align-top">{{ item.quantity }} PC</td>
          <td class="px-4 py-2 align-top">${{ item.price }}</td>
          <td class="px-4 py-2 text-green-700 font-semibold align-top">${{ item.total }}</td>
        </tr>
      </tbody>
    </table>

    <!-- Payment and totals section -->
    <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-8 border-t border-gray-300 pt-6">
      <div class="space-y-6 text-gray-700 max-w-xs">
        <div>
          <h3 class="font-semibold text-teal-700 mb-1">Payment Info</h3>
          <p>evc0619538337 / <br /> edhab 0629538337</p>
        </div>
        <div>
          <h3 class="font-semibold text-teal-700 mb-1">Served by</h3>
          <p>{{items[0]?.served}}</p>
        </div>
        <div>
          <img
            class="w-36 mt-4 rounded"
            src="../assets/Black and Blue Mobile Phone Repair Logo.png"
            alt="Logo"
          />
        </div>
      </div>

      <div class="bg-teal-50 rounded-lg p-6 w-full max-w-xs shadow">
        <div class="flex justify-between py-1 border-b border-teal-200">
          <span class="font-semibold text-teal-700">Total Amount</span>
          <span class="font-bold text-teal-800">${{ totalPrice }}</span>
        </div>
        <div class="flex justify-between py-1 border-b border-teal-200">
          <span class="font-semibold text-teal-700">Discount</span>
          <span class="font-bold text-teal-800">${{items[0]?.discount}}</span>
        </div>
        <div class="flex justify-between py-1 border-b border-teal-200">
          <span class="font-semibold text-teal-700">Paid</span>
          <span class="font-bold text-teal-800">${{items[0]?.paid}}</span>
        </div>
        <div class="flex justify-between py-1">
          <span class="font-semibold text-teal-700">Balance</span>
          <span class="font-bold text-teal-800">${{items[0]?.balance}}</span>
        </div>
      </div>
    </div>

    <!-- Thank you note -->
    <p class="mt-8 text-green-700 font-semibold text-lg text-center">
      Thank you {{ items[0]?.name }} for your purchase!
    </p>

    <!-- Print button -->
    <div class="text-center mt-6">
      <button
        class="bg-blue-600 hover:bg-blue-700 transition text-white py-2 px-6 rounded shadow"
        @click="window.print()"
      >
        Print Receipt
      </button>
    </div>
  </div>
</template>




<script>
export default {
  name: "Result",
  data() {
    const today = new Date();
    return {
      data:{
      month: today.toLocaleString('default', { month: 'long' }),
      day: today.getDate(),
      year: today.getFullYear(),
      }
    };
  },
  props: {
    items: {
      type: Array,
      required: true,
    },
  },

  computed: {
    totalPrice() {
      return this.items.reduce((sum, item) => sum + item.total , 0);
    },
  },
};
</script>

<style>
body{
  padding:0;
  margin:0;
}

@media print {
  /* Make sure colors and backgrounds are printed */
  body {
    -webkit-print-color-adjust: exact;
    print-color-adjust: exact;
    background: white;
  }

  /* Center the content on the page */
  #receipt {
    width: 800px;
    margin: 0 auto;
    padding: 20px;
  }

  /* Hide elements like buttons */
  .print-button, .no-print {
    display: none !important;
  }

  th, td {
    padding: 8px !important;
    text-align: left !important;
    font-size: 12px !important;
  }


  @media print {
  .print-button {
    display: none !important;
  }
}

 

  /* Background colors */
  .bg-teal-500, .bg-teal-400 {
    background-color: #14b8a6 !important; /* Tailwind's teal */
    color: white !important;
  }

  .bg-gray-100,
  .bg-gray-200 {
    background-color: #e5e7eb !important;
  }





  /* Avoid page breaks inside tables */
  table {
    page-break-inside: avoid !important;
  }
}

</style>
