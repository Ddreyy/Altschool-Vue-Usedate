<script setup>
defineProps({
  msg: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="container">
    <div class="date-section">
      <h1>Current Date</h1>
      <p>Date: {{ currentDate }}</p>
      <p>Day: {{ getDay(currentDate) }}</p>
      <p>Month: {{ getMonth(currentDate) }}</p>
    </div>

    <div class="date-section">
      <h1>New Date</h1>
      <p>Date: {{ newDate }}</p>
      <p>Day: {{ getDay(newDate) }}</p>
      <p>Month: {{ getMonth(newDate) }}</p>
    </div>

    <div class="date-section">
      <h1>New Month</h1>
      <p>Date: {{ newMonth }}</p>
      <p>Month: {{ getMonth(newMonth) }}</p>
    </div>

    <div class="button-section">
      <button @click="handleAddDay">Add days</button>
      <button @click="handleAddMonth">Add months</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentDate: new Date(),
      newDate: new Date(),
      newMonth: new Date(),
    };
  },
  methods: {
    getDay(date) {
      return date.getDate();
    },
    getMonth(date) {
      return date.getMonth() + 1; 
    },
    addDay(numberOfDays) {
      const newDate = new Date(this.newDate);
      newDate.setDate(newDate.getDate() + numberOfDays);
      return newDate;
    },
    addMonth(numberOfMonths) {
      const newMonth = new Date(this.newMonth);
      newMonth.setMonth(newMonth.getMonth() + numberOfMonths);
      return newMonth;
    },
    handleAddDay() {
      const updatedDate = this.addDay(20);
      this.newDate = updatedDate;
      if (updatedDate.getMonth() !== this.currentDate.getMonth()) {
        console.log("Wow, it's a brand new month! Time flies!");
      } else {
        console.log(`The month is still ongoing with ${updatedDate.getDate()} days`);
      }
    },
    handleAddMonth() {
      const updatedMonth = this.addMonth(3);
      this.newMonth = updatedMonth;
      if (updatedMonth.getFullYear() !== this.currentDate.getFullYear()) {
        console.log("It's a new year");
      } else {
        console.log(`Current Month: ${updatedMonth.getMonth() + 1}`);
      }
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  justify-content: center; 
  align-items: center; 
  margin-top: 50px;
  height: 100vh; 
}

.date-section {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 20px;
  margin-bottom: 20px;
  text-align: center;
}

.button-section button {
  padding: 10px 20px;
  margin: 10px;
  font-size: 16px;
  cursor: pointer;
  background-color: #4caf50;
  color: black;
  border: none;
  border-radius: 5px;
  outline: none;
}

.button-section button:hover {
  background-color: #45a049;
}


@media screen and (max-width: 768px) {
  .container {
    margin-top: 20px; 
  }
  .date-section {
    padding: 15px; 
    margin-bottom: 15px; 
  }
}
</style>