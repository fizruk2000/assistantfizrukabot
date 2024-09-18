<template>
<div class="competition">
  <h2>Многоборье "Защитник Отечества"</h2>
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
          { result: 19, points: 0 }, { result: 20, points: 1 }, 
{ result: 21, points: 2 }, 
{ result: 22, points: 3 }, 
{ result: 23, points: 4 }, 
{ result: 24, points: 5 }, 
{ result: 25, points: 6 }, 
{ result: 26, points: 7 }, 
{ result: 27, points: 8 }, 
{ result: 28, points: 9 }, 
{ result: 29, points: 10 }, 
{ result: 30, points: 12 }, 
{ result: 31, points: 14 }, 
{ result: 32, points: 16 }, 
{ result: 33, points: 18 }, 
{ result: 34, points: 20 }, 
{ result: 36, points: 22 }, 
{ result: 37, points: 24 }, 
{ result: 38, points: 26 }, 
{ result: 39, points: 28 }, 
{ result: 40, points: 30 }, 
{ result: 41, points: 32 }, 
{ result: 42, points: 34 }, 
{ result: 43, points: 36 }, 
{ result: 44, points: 38 }, 
{ result: 45, points: 40 }, 
{ result: 46, points: 42 }, 
{ result: 47, points: 44 }, 
{ result: 48, points: 46 }, 
{ result: 49, points: 48 }, 
{ result: 50, points: 50 }, 
{ result: 51, points: 52 }, 
{ result: 52, points: 54 }, 
{ result: 53, points: 56 },  
{ result: 54, points: 58 }, 
{ result: 55, points: 60 },], result: 0, points: 0 },
          { name: 'Плавание', resultsArray: [
          { result: 24.5, points: 60 }, { result: 24.6, points: 59 }, { result: 24.7, points: 58 }, { result: 24.8, points: 57 }, 
          { result: 24.9, points: 56 }, { result: 25.0, points: 55 }, { result: 25.2, points: 54 }, 
          { result: 25.4, points: 53 }, { result: 25.6, points: 52 }, { result: 25.8, points: 51 }, 
          { result: 26.0, points: 50 }, { result: 26.2, points: 49 }, { result: 26.4, points: 48 }, 
          { result: 26.6, points: 47 }, { result: 26.8, points: 46 }, { result: 27.0, points: 45 }, 
          { result: 27.2, points: 44 }, { result: 27.4, points: 43 }, { result: 27.6, points: 42 }, 
          { result: 27.8, points: 41 }, { result: 28.0, points: 40 }, { result: 28.5, points: 39 }, 
          { result: 29.0, points: 38 }, { result: 29.5, points: 37 }, { result: 30.0, points: 36 }, 
          { result: 30.5, points: 35 }, { result: 31.0, points: 34 }, { result: 31.5, points: 33 }, 
          { result: 32.0, points: 32 }, { result: 32.5, points: 31 }, { result: 33.0, points: 30 }, 
          { result: 33.5, points: 29 }, { result: 34.0, points: 28 }, { result: 34.5, points: 27 }, 
          { result: 35.0, points: 26 }, { result: 35.5, points: 25 }, { result: 36.0, points: 24 }, 
          { result: 36.5, points: 23 }, { result: 37.0, points: 22 }, { result: 37.5, points: 21 }, 
          { result: 38.0, points: 20 }, { result: 38.5, points: 19 }, { result: 39.0, points: 18 }, 
          { result: 39.5, points: 17 }, { result: 40.0, points: 16 }, { result: 41.0, points: 15 }, 
          { result: 42.0, points: 14 }, { result: 43.0, points: 13 }, { result: 44.0, points: 12 }, 
          { result: 45.0, points: 11 }, { result: 46.0, points: 10 }, { result: 47.0, points: 9 }, 
          { result: 48.0, points: 8 }, { result: 49.0, points: 7 }, { result: 50.0, points: 6 }, 
          { result: 51.0, points: 5 }, { result: 52.0, points: 4 }, { result: 53.0, points: 3 }, 
          { result: 54.0, points: 2 }, { result: 55.0, points: 1 }, { result: 55.1, points: 0 }], result: 0, points: 0 },
          { name: 'Бег 3000м', resultsArray: [
          { result: 10.2, points: 60 }, 
{ result: 10.25, points: 58 }, 
{ result: 10.30, points: 56 }, 
{ result: 10.35, points: 54 }, 
{ result: 10.40, points: 52 }, 
{ result: 10.45, points: 50 }, 
{ result: 10.50, points: 48 }, 
{ result: 10.55, points: 46 }, 
{ result: 11.00, points: 44 }, 
{ result: 11.05, points: 42 }, 
{ result: 11.10, points: 40 }, 
{ result: 11.15, points: 38 }, 
{ result: 11.20, points: 36 }, 
{ result: 11.25, points: 34 }, 
{ result: 11.30, points: 32 }, 
{ result: 11.35, points: 30 }, 
{ result: 11.40, points: 28 }, 
{ result: 11.45, points: 26 }, 
{ result: 11.50, points: 24 }, 
{ result: 11.55, points: 22 }, 
{ result: 12.00, points: 20 }, 
{ result: 12.10, points: 18 }, 
{ result: 12.20, points: 16 }, 
{ result: 12.30, points: 14 }, 
{ result: 12.40, points: 12 }, 
{ result: 12.50, points: 10 }, 
{ result: 13.00, points: 9 }, 
{ result: 13.20, points: 8 }, 
{ result: 13.40, points: 7 }, 
{ result: 14.00, points: 6 }, 
{ result: 14.20, points: 5 }, 
{ result: 14.40, points: 4 }, 
{ result: 15.00, points: 3 }, 
{ result: 15.20, points: 2 }, 
{ result: 15.40, points: 1 }, 
{ result: 15.41, points: 0 }], result: 0, points: 0 },
          { name: 'Стрельба', resultsArray: [
          { result: 0.9, points: 0 }, { result: 1, points: 1 }, 
{ result: 2, points: 2 }, 
{ result: 3, points: 3 }, 
{ result: 4, points: 4 }, 
{ result: 5, points: 5 }, 
{ result: 6, points: 6 }, 
{ result: 7, points: 7 }, 
{ result: 8, points: 8 }, 
{ result: 9, points: 9 }, 
{ result: 10, points: 10 }, 
{ result: 11, points: 11 }, 
{ result: 12, points: 12 }, 
{ result: 13, points: 13 }, 
{ result: 14, points: 14 }, 
{ result: 15, points: 15 }, 
{ result: 16, points: 16 }, 
{ result: 17, points: 17 }, 
{ result: 18, points: 18 }, 
{ result: 19, points: 19 }, 
{ result: 20, points: 20 }, 
{ result: 21, points: 21 }, 
{ result: 22, points: 22 }, 
{ result: 23, points: 23 }, 
{ result: 24, points: 24 }, 
{ result: 25, points: 25 }, 
{ result: 26, points: 26 }, 
{ result: 27, points: 27 }, 
{ result: 28, points: 28 }, 
{ result: 29, points: 29 }, 
{ result: 30, points: 30 }, 
{ result: 31, points: 31 }, 
{ result: 32, points: 32 }, 
{ result: 33, points: 33 }, 
{ result: 34, points: 34 }, 
{ result: 35, points: 35 }, 
{ result: 36, points: 36 }, 
{ result: 37, points: 37 }, 
{ result: 38, points: 38 }, 
{ result: 39, points: 39 }, 
{ result: 40, points: 40 }, 
{ result: 41, points: 42 }, 
{ result: 42, points: 44 }, 
{ result: 43, points: 46 }, 
{ result: 44, points: 48 }, 
{ result: 45, points: 50 }, 
{ result: 46, points: 52 }, 
{ result: 47, points: 54 }, 
{ result: 48, points: 56 }, 
{ result: 49, points: 58 },  
{ result: 50, points: 60 },], result: 0, points: 0 },
          { name: 'Подтягивание', resultsArray: [
          { result: 0.9, points: 0 }, { result: 1, points: 1 }, 
{ result: 2, points: 2 }, 
{ result: 3, points: 3 }, 
{ result: 4, points: 4 }, 
{ result: 5, points: 5 }, 
{ result: 6, points: 6 }, 
{ result: 7, points: 7 }, 
{ result: 8, points: 8 }, 
{ result: 9, points: 9 }, 
{ result: 10, points: 10 }, 
{ result: 11, points: 11 }, 
{ result: 12, points: 12 }, 
{ result: 13, points: 13 }, 
{ result: 14, points: 14 }, 
{ result: 15, points: 15 }, 
{ result: 16, points: 16 }, 
{ result: 17, points: 17 }, 
{ result: 18, points: 18 }, 
{ result: 19, points: 19 }, 
{ result: 20, points: 20 }, 
{ result: 21, points: 22 }, 
{ result: 22, points: 24 }, 
{ result: 23, points: 26 }, 
{ result: 24, points: 28 }, 
{ result: 25, points: 30 }, 
{ result: 26, points: 32 }, 
{ result: 27, points: 34 }, 
{ result: 28, points: 36 }, 
{ result: 29, points: 38 }, 
{ result: 30, points: 40 }, 
{ result: 31, points: 42 }, 
{ result: 32, points: 44 }, 
{ result: 33, points: 46 }, 
{ result: 34, points: 48 }, 
{ result: 35, points: 50 }, 
{ result: 36, points: 52 }, 
{ result: 37, points: 54 }, 
{ result: 38, points: 56 }, 
{ result: 39, points: 58 }, 
{ result: 40, points: 60 }, { result: 60, points: 60 },], result: 0, points: 0 },
          { name: 'Лыжные гонки 5км', resultsArray: [
          { result: 13.30, points: 60 }, 
{ result: 13.35, points: 59 }, 
{ result: 13.40, points: 58 }, 
{ result: 13.45, points: 57 }, 
{ result: 13.50, points: 56 }, 
{ result: 13.55, points: 55 }, 
{ result: 14.00, points: 54 }, 
{ result: 14.05, points: 53 }, 
{ result: 14.10, points: 52 }, 
{ result: 14.15, points: 51 }, 
{ result: 14.20, points: 50 }, 
{ result: 14.25, points: 49 }, 
{ result: 14.30, points: 48 }, 
{ result: 14.40, points: 47 }, 
{ result: 14.50, points: 46 }, 
{ result: 15.00, points: 45 }, 
{ result: 15.10, points: 44 }, 
{ result: 15.20, points: 43 }, 
{ result: 15.30, points: 42 }, 
{ result: 15.40, points: 41 }, 
{ result: 15.50, points: 40 }, 
{ result: 16.00, points: 39 }, 
{ result: 16.10, points: 38 }, 
{ result: 16.20, points: 37 }, 
{ result: 16.30, points: 36 }, 
{ result: 16.40, points: 35 }, 
{ result: 16.50, points: 34 }, 
{ result: 17.00, points: 33 }, 
{ result: 17.15, points: 32 }, 
{ result: 17.30, points: 31 }, 
{ result: 17.45, points: 30 }, 
{ result: 18.00, points: 29 }, 
{ result: 18.15, points: 28 }, 
{ result: 18.30, points: 27 }, 
{ result: 18.45, points: 26 }, 
{ result: 19.00, points: 25 }, 
{ result: 19.20, points: 24 }, 
{ result: 19.40, points: 23 }, 
{ result: 20.00, points: 22 }, 
{ result: 20.20, points: 21 }, 
{ result: 20.40, points: 20 }, 
{ result: 21.00, points: 19 }, 
{ result: 21.25, points: 18 }, 
{ result: 21.50, points: 17 }, 
{ result: 22.15, points: 16 }, 
{ result: 22.40, points: 15 }, 
{ result: 23.05, points: 14 }, 
{ result: 23.30, points: 13 }, 
{ result: 24.00, points: 12 }, 
{ result: 24.30, points: 11 }, 
{ result: 25.00, points: 10 }, 
{ result: 25.30, points: 9 }, 
{ result: 26.00, points: 8 }, 
{ result: 26.30, points: 7 }, 
{ result: 27.00, points: 6 }, 
{ result: 27.30, points: 5 }, 
{ result: 28.00, points: 4 }, 
{ result: 28.30, points: 3 }, 
{ result: 29.00, points: 2 }, 
{ result: 29.30, points: 1 }, 
{ result: 29.31, points: 0 }], result: 0, points: 0 },
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
}
</script>

<style scoped>
.competition {
font-family: Arial, sans-serif;
max-width: 100%;
margin: auto;
padding: 20px;
}
.event-form {
margin-bottom: 15px;
margin-left: 25%;
}
label {
display: block;
margin-bottom: 5px;
}
input {
margin-right: 10px;
}
h2 {
text-align: center;
}
</style>