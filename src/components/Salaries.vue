<template>
  <div class="company-salaries">
    <h2 class="salaries-title">Salaries</h2>
    <div class="country-select">
      <label for="country">Select Country:</label>
      <select id="country" v-model="selectedCountry" @change="filterSalaries">
        <option value="all">All</option>
        <option value="us">United States</option>
        <option value="uk">United Kingdom</option>
        <option value="ca">Canada</option>
      </select>
    </div>
    <div
      v-for="salary in filteredSalaries"
      :key="salary.position"
      class="salary-item"
    >
      <div class="salary-position">{{ salary.position }}</div>
      <div class="salary-amount">{{ salary.amount }}</div>
      <div class="salary-comparison" :style="getComparisonStyle(salary)"></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      salaries: [
        { position: "Software Engineer", amount: "$120,000", country: "us" },
        { position: "Account Manager", amount: "$130,000", country: "us" },
        {
          position: "Sales Development Representative",
          amount: "$70,000",
          country: "us",
        },
        {
          position: "Customer Success Representative",
          amount: "$65,000",
          country: "uk",
        },
        { position: "Product Manager", amount: "$140,000", country: "uk" },
        { position: "Marketing Specialist", amount: "$80,000", country: "uk" },
        { position: "Data Analyst", amount: "$90,000", country: "ca" },
        { position: "UX/UI Designer", amount: "$110,000", country: "ca" },
        {
          position: "Business Development Manager",
          amount: "$120,000",
          country: "ca",
        },
        { position: "Financial Analyst", amount: "$100,000", country: "ca" },
      ],
      selectedCountry: "all",
    };
  },
  computed: {
    filteredSalaries() {
      if (this.selectedCountry === "all") {
        return this.salaries;
      } else {
        return this.salaries.filter(
          (salary) => salary.country === this.selectedCountry
        );
      }
    },
  },
  methods: {
    getComparisonStyle(salary) {
      const maxSalary = Math.max(
        ...this.filteredSalaries.map((s) =>
          parseInt(s.amount.replace("$", "").replace(",", ""))
        )
      );
      const salaryPercentage =
        (parseInt(salary.amount.replace("$", "").replace(",", "")) /
          maxSalary) *
        100;
      return {
        width: `${salaryPercentage}%`,
      };
    },
    filterSalaries(event) {
      this.selectedCountry = event.target.value;
    },
  },
};
</script>

<style lang=scss scoped>
.company-salaries {
  text-align: left;
  max-width: 500px;
}

.salaries-title {
  color: green;
  border-bottom: 3px solid green;
  max-width: 100px;
  text-align: center;
  margin-bottom: 30px;
}

.salary-position {
  font-weight: bold;
}

.salary-comparison {
  background-color: #0077b5;
  height: 20px;
  margin-bottom: 15px;
  transition: all 0.7s;
  border-radius: 0px;
  &:hover {
    background: green;
    border-radius: 10px;
  }
}

.country-select {
  margin-bottom: 20px;
}

.country-select label {
  margin-right: 10px;
}
</style>