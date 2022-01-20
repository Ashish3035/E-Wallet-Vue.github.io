<template>
  <h3 class="text-4xl font-normal leading-normal text-white">Your E-Wallet</h3>
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
      placeholder="Enter Amount to Add into Wallet"
      v-model="enteredAmount"
    />
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
    <div class="text-white">Wallet Balance: ${{ accbalance }}</div>

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
      placeholder="Enter Amount to Send"
      v-model="sendingMoney"
    />
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
      @click="pay"
    >
      Send Money
    </button>

    <h3 class="text-4xl font-normal leading-normal text-white">
      Your Transactions
    </h3>
    <div class="container flex justify-center my-20">
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
                </tr>
              </thead>
              <tbody>
                <tr v-for="(transaction, index) in transactions" :key="index">
                  <td class="text-white">{{ transaction.id }}</td>
                  <td class="text-red-500">-{{ transaction.amount }}$</td>
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
      transactions: [],
      accbalance: 0,
      enteredAmount: "",
      sendMoney: "",
    };
  },
  methods: {
    AddToWallet() {
      if (this.accbalance >= 0) {
        this.accbalance = this.enteredAmount + this.accbalance;
        // const newTransaction = {
        //   id: Date.now(),
        //   amount: this.enteredAmount,
        // };
        // this.transactions.push(newTransaction);
      }

      this.enteredAmount = "";
    },
    pay() {
      if (this.accbalance <= 0 || this.sendingMoney > this.accbalance) {
        alert("insufficient balance plz add amount into wallet first");
      } else {
        this.accbalance -= this.sendingMoney;
        const newTransaction = {
          id: Date.now(),
          amount: this.sendingMoney,
        };
        this.transactions.push(newTransaction);
      }
      this.sendingMoney = "";
    },
  },
};
</script>
