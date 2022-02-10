<template>
  <h3 class="text-4xl font-normal leading-normal text-white">Your E-Wallet</h3>
  <div class="text-white">Wallet Balance: ${{ accbalance }}</div>
  <div class="home">
    <input
      class="
        shadow
        appearance-none
        border border-red-500
        rounded
        w-96
        py-2
        px-3
        text-gray-700
        mb-3
        leading-tight
        focus:outline-none focus:shadow-outline
      "
      type="number"
      placeholder="Enter Amount"
      v-model="amount"
    />

    <br />
    <input
      class="
        shadow
        appearance-none
        border border-red-500
        rounded
        w-96
        py-2
        px-3
        text-gray-700
        mb-3
        leading-tight
        focus:outline-none focus:shadow-outline
      "
      type="text"
      placeholder="Enter Name"
      v-model="Name"
    />
    <br />
    <button
      class="
        bg-blue-500
        hover:bg-blue-700
        text-white
        font-bold
        py-2
        px-4
        rounded
        focus:outline-none focus:shadow-outline
      "
      type="button"
      @click="AddToWallet"
    >
      Add to Wallet
    </button>
    <button
      class="
        bg-blue-500
        hover:bg-blue-700
        text-white
        font-bold
        py-2
        ml-2
        px-4
        rounded
        focus:outline-none focus:shadow-outline
      "
      type="button"
      @click="pay"
    >
      Send Money
    </button>

    <h3 class="text-4xl font-normal leading-normal text-white my-10">
      Your Transactions
    </h3>
    <div class="container flex justify-center my-10">
      <div class="flex flex-col">
        <div class="w-full">
          <div class="border-b border-gray-200 shadow">
            <table>
              <thead class="bg-gray-50">
                <tr>
                  <th class="px-6 py-2 text-xs text-gray-500">
                    Transaction ID
                  </th>
                  <th class="px-6 py-2 text-xs text-gray-500">
                    Transactions Amount
                  </th>
                  <th class="px-6 py-2 text-xs text-gray-500">Name</th>
                  <th class="px-6 py-2 text-xs text-gray-500">Credit/Debit</th>
                  <th class="px-6 py-2 text-xs text-gray-500">Balance</th>
                  <th class="px-6 py-2 text-xs text-gray-500">Offers</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(transaction, index) in transactions" :key="index">
                  <td class="text-white">{{ transaction.id }}</td>
                  <td class="text-white">{{ transaction.amount }}$</td>
                  <td class="text-white">
                    {{ transaction.Name }}
                  </td>
                  <td class="text-white">
                    {{ transaction.status }}
                  </td>
                  <td class="text-white">
                    {{ transaction.balance }}
                  </td>
                  <td class="text-white">
                    {{ transaction.reward }}
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  components: {},
  data() {
    return {
      offers: [
        "10% off on zomato",
        "try next time",
        "10rs cashback",
        "10% off on myntra",
      ],
      transactions: [],
      accbalance: 0,
      amount: "",
      Name: "",
    };
  },
  methods: {
    AddToWallet() {
      if (this.accbalance >= 0) {
        this.accbalance = this.amount + this.accbalance;
      }
      const newTransaction = {
        id: Date.now(),
        amount: "+" + this.amount,
        Name: this.Name,
        status: "Credit",
        balance: this.accbalance + "$",
        reward: this.offers[Math.floor(Math.random() * this.offers.length)],
      };
      this.transactions.push(newTransaction);
      this.Name = "";
      this.amount = "";
    },
    pay() {
      if (this.accbalance <= 0 || this.amount > this.accbalance) {
        alert("insufficient balance plz add amount into wallet first");
      } else {
        this.accbalance -= this.amount;
        const newTransaction = {
          id: Date.now(),
          amount: "-" + this.amount,
          Name: this.Name,
          status: "Debit",
          balance: this.accbalance + "$",
          reward: this.offers[Math.floor(Math.random() * this.offers.length)],
        };
        this.transactions.push(newTransaction);
      }
      this.amount = "";
      this.Name = "";
    },
  },
};
</script>
