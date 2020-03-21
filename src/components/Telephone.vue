<template>
  <div class="mt-6">
    <input
      type="text"
      :placeholder="template"
      class="w-56 text-2xl bg-gray-300 p-3 rounded-lg focus:ouline-none"
      v-model="number"
    />
  </div>
</template>

<script>
export default {
  name: "Telephone",
  props: {
    template: String
  },
  data() {
    return {
      number: "",
      format: "",
      regex: ""
    };
  },
  mounted() {
    let x = 1;
    this.format = this.template.replace(/X+/g, () => "$" + x++);

    this.template.match(/X+/g).forEach(char => {
      this.regex += "(\\d{" + char.length + "})?";
    });
    console.log(this.regex);
  },
  watch: {
    number(next, prev) {
      if (next.length > prev.length) {
        this.number = this.number
          .replace(/[^0-9]/g, "")
          .replace(new RegExp(this.regex), this.format)
          .substr(0, this.template.length);
      }
    }
  }
};
</script>

<style lang="scss" scoped>
</style>