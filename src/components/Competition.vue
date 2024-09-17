<template>
<div class="competition">
  <h1>Многоборье "Защитник Отечества"</h1>
  <div v-for="(event, index) in events" :key="index" class="event-form">
    <label :for="'result-' + index">{{ event.name }}</label>
    <input
      type="number"
      :id="'result-' + index"
      v-model.number="event.result"
      @input="calculatePoints(index)"
      min="0"
    />
    <span>Очки: {{ event.points }}</span>
  </div>
  <h2>Итоговая сумма очков: {{ totalPoints }}</h2>
</div>
</template>

<script>
export default {
data() {
  return {
    events: [
      { name: 'Бег 100м', resultsArray: [
      { result: 10.3, points: 60 }, { result: 11.3, points: 60 }, { result: 11.4, points: 58 }, { result: 11.5, points: 56 },
          { result: 11.6, points: 54 }, { result: 11.7, points: 52 }, { result: 11.8, points: 50 },
          { result: 11.9, points: 48 }, { result: 12.0, points: 46 }, { result: 12.1, points: 44 },
          { result: 12.2, points: 42 }, { result: 12.3, points: 40 }, { result: 12.4, points: 38 },
          { result: 12.5, points: 36 }, { result: 12.6, points: 34 }, { result: 12.7, points: 32 },
          { result: 12.8, points: 30 }, { result: 12.9, points: 28 }, { result: 13.0, points: 26 },
          { result: 13.1, points: 24 }, { result: 13.2, points: 22 }, { result: 13.3, points: 20 },
          { result: 13.4, points: 18 }, { result: 13.5, points: 16 }, { result: 13.6, points: 14 },
          { result: 13.7, points: 12 }, { result: 13.8, points: 10 }, { result: 13.9, points: 9 },
          { result: 14.0, points: 8 }, { result: 14.1, points: 7 }, { result: 14.2, points: 6 },
          { result: 14.3, points: 5 }, { result: 14.4, points: 4 }, { result: 14.5, points: 3 },
          { result: 14.6, points: 2 }, { result: 14.7, points: 1 }, { result: 14.8, points: 0 }], result: 0, points: 0 },
      { name: 'Метание гранаты', resultsArray: [
          { result: 10.3, points: 60 }, { result: 14.8, points: 0 }], result: 0, points: 0 },
          { name: 'Плавание', resultsArray: [
          { result: 10.3, points: 60 }, { result: 14.8, points: 0 }], result: 0, points: 0 },
          { name: 'Бег 3000м', resultsArray: [
          { result: 10.3, points: 60 }, { result: 14.8, points: 0 }], result: 0, points: 0 },
          { name: 'Стрельба', resultsArray: [
          { result: 10.3, points: 60 }, { result: 14.8, points: 0 }], result: 0, points: 0 },
          { name: 'Подтягивание', resultsArray: [
          { result: 10.3, points: 60 }, { result: 14.8, points: 0 }], result: 0, points: 0 },
          { name: 'Лыжные гонки 5км', resultsArray: [
          { result: 10.3, points: 60 }, { result: 14.8, points: 0 }], result: 0, points: 0 },
    ]
  };
},
computed: {
  totalPoints() {
    return this.events.reduce((sum, event) => sum + event.points, 0);
  }
},
methods: {
  calculatePoints(index) {
    const result = this.events[index].result;
    const resultArray = this.events[index].resultsArray;
    
    // Бинарный поиск для нахождения подходящего количества очков
    let low = 0;
    let high = resultArray.length - 1;
    let points = 0;

    while (low <= high) {
      const mid = Math.floor((low + high) / 2);
      if (resultArray[mid].result >= result) {
        points = resultArray[mid].points;
        high = mid - 1; // Ищем дальше, чтобы найти наименьшие очки
      } else {
        low = mid + 1;
      }
    }

    this.events[index].points = points;
  }
}
};
</script>

<style scoped>
.competition {
font-family: Arial, sans-serif;
max-width: 600px;
margin: auto;
padding: 20px;
}
.event-form {
margin-bottom: 15px;
}
label {
display: block;
margin-bottom: 5px;
}
input {
margin-right: 10px;
}
h1 {
text-align: center;
}
</style>
