<template>
  <div class="flex justify-center">
    <div class="w-1/2 bg-blue-900 rounded-lg shadow px-6 py-12 flex flex-col items-center">
      <div class="bg-gray-400 rounded-full flex justify-around p-1">
        <button
          v-for="frequency in frequencies"
          :key="frequency"
          @click="currentFrequency = frequency"
          :class="(currentFrequency == frequency) ? 'bg-blue-600 text-gray-200': ''"
          class="rounded-full text-xs font-bold px-6 py-1 uppercase focus:outline-none"
        >{{frequency}}</button>
      </div>
      <div class="flex w-full pt-8">
        <div v-for="plan in plans" :key="plan.name" class="text-white w-1/2">
          <h1 class="text-2xl font-bold">{{plan.name}}</h1>
          <ul class="pt-4">
            <li v-for="benefit in plan.benefits[currentFrequency]" :key="benefit">{{benefit}}</li>
          </ul>
          <div class="flex justify-center pt-8">
            <div class="text-4xl font-bold">{{getPrice(plan.pricing[currentFrequency].price)}}</div>
            <div class="pl-1 pt-2 text-gray-300">{{plan.pricing[currentFrequency].label}}</div>
          </div>
        </div>
      </div>
      <div class="pt-4 text-center text-gray-400 text-sm font-bold">
        <a v-for="(currency, index) in currencies" :key="currency" href="#" @click.prevent="currentCurrency = currency">{{currency.toUpperCase()}} {{(index + 1) > currencies.length -1 ? '' : '|'}} </a> 
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
     //!Aumentar precio de las monedas
    getPrice(price) {
      switch (this.currentCurrency) {
        case "usd":
          return "$" + price;
          
        case "eur":
          return Math.round(price * 0.93) + "€";

        case "sol": 
          return 'S/' + Math.round(price * 3.23);
      }
    }
  },
  data() {
    return {
      //!Aumentar mas formas de periodo de pago
      frequencies: ["monthly", "yearly", "lifetime"],
      currentFrequency: "monthly",

      //!Aumentar mas monedas
      currencies: ["usd", "eur", "sol"],
      currentCurrency: "usd",

     //!Aumentar mas planes de pago
      plans: [
        {
          name: "Starter",
          pricing: {
            //!Aumenta precios de lass formas de periodo de pago
            monthly: { price: "99", label: "/mo" },
            yearly: { price: "999", label: "/yr" },
            lifetime: { price: "9999", label: "/yr" }
          },
          benefits: {
            //!Aumentar mas beneficio de periodo de pago
            monthly: ["Benefit 1", "Benefit 2", "Benefit 3"],
            yearly: ["Benefit 1", "Benefit 2", "Benefit 3", "Benefit 4"],
            lifetime: [
              "Benefit 1",
              "Benefit 2",
              "Benefit 3",
              "Benefit 4",
              "Benefit 5"
            ]
          }
        },
        {
          name: "Pro",
          pricing: {
            //!Aumentar precios de las formas de periodo de pago
            monthly: { price: "199", label: "/mo" },
            yearly: { price: "1999", label: "/yr" },
            lifetime: { price: "19999", label: "/yr" }
          },
          benefits: {
            //!Aumentar mas beneficio de periodo de pago
            monthly: ["Benefit 1", "Benefit 2", "Benefit 3", "Benefit 4"],
            yearly: [
              "Benefit 1",
              "Benefit 2",
              "Benefit 3",
              "Benefit 4",
              "Benefit 5"
            ],
            lifetime: [
              "Benefit 1",
              "Benefit 2",
              "Benefit 3",
              "Benefit 4",
              "Benefit 5",
              "Benefit 6  "
            ]
          }
        },
        {
          name: "All-Star",
          pricing: {
            //!Aumentar precios de las formas de periodo de pago
            monthly: { price: "299", label: "/mo" },
            yearly: { price: "2999", label: "/yr" },
            lifetime: { price: "29999", label: "/yr" }
          },
          benefits: {
            //!Aumentar mas beneficio de periodo de pago
            monthly: [
              "Benefit 1",
              "Benefit 2",
              "Benefit 3",
              "Benefit 4",
              "Benefit 5"
            ],
            yearly: [
              "Benefit 1",
              "Benefit 2",
              "Benefit 3",
              "Benefit 4",
              "Benefit 5",
              "Benefit 6"
            ],
            lifetime: [
              "Benefit 1",
              "Benefit 2",
              "Benefit 3",
              "Benefit 4",
              "Benefit 5",
              "Benefit 6",
              "Benefit 7"
            ]
          }
        }
      ]
    };
  }
};
</script>

<style lang="scss" scoped>
</style>