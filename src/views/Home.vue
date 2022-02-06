<template>
  <div class="home">
    <section class="props-transfer">
      <div class="container">
        <div class="row">
          <h4 class="text-center">
            Передача в пропсах разных типов данных и их обновление
          </h4>
          <p class="description">
            Для тестирования передачи создано три соподчиненных компонента:
            прародитель, родитель и ребенок. У прародителя в данных (
            <code>data(){}</code> ) заданы все типы данных JS. Каждый из типов
            передается от прародителя к родителю с единственным пропсом. Этот
            проп родитель передает далее ребенку. Ребенок выводит на страницу
            значение. По нажатию на кнопку обновления значения данных в
            прародителе изменяются.
          </p>
          <p class="purpose">
            Цель тестирования - выяснить как ведут себя дочерние компоненты при
            изменении значений в родительском компоненте при передаче в качестве
            пропса параметров разного типа данных.
          </p>
        </div>
        <PropsTransferGrandParent />
      </div>
    </section>

    <section class="props-transfer">
      <div class="container">
        <div class="row">
          <h4 class="text-center">Запросы на сервер</h4>
          <p class="description">
            Для тестирования работоспособности и скорости выполнения запросов
            выполняется один и тот же запрос на получение записей списка тремя
            разными методами: AJAX, fetch и axios.
          </p>
          <p class="purpose">
            Цель тестирования - отработать выполнение запросов на сервер разными
            методами и сравнить скорость получения ответа.
          </p>
        </div>
        <button @click="ajaxRequest">Ajax</button>
        <button @click="fetchRequest">Fetch</button>
        <button @click="axiosRequest">Axios</button>
        <p>
          Ajax отработал за {{ ajaxtime }} мс по факту отрабатывает за 263.2 мс,
          {{ ajaxtime - 263 }} мс тратиться на вычисление даты и разницы дат
        </p>
        <p>
          Fetch отработал за {{ fetchtime }} мс по факту отрабатывает за 297.5
          мс, {{ fetchtime - 297 }} мс тратиться на вычисление даты и разницы
          дат
        </p>
        <p>
          Axios отработал за {{ axiostime }} мс по факту отрабатывает за 278.2
          мс, {{ axiostime - 278 }} мс тратиться на вычисление даты и разницы
          дат
        </p>
      </div>
    </section>

    <section class="props-transfer">
      <div class="container">
        <div class="row">
          <h4 class="text-center">Асинхронные запросы</h4>
          <p class="description">
            Из БД запрашиваются иконки, цвета, категории и задания. Необходимо
            сначала привязать иконки и цвета к категориям, затем привязать
            категории к заданиям.
          </p>
          <p class="purpose">
            Цель - разобраться с асинхронными запросами и выполнять действия в
            правильном порядке.
          </p>
        </div>
        <button type="button">Запрос</button>
        <div v-if="!isAppLoaded" class="spinner-border text-primary" role="status">
          <span class="visually-hidden">Loading...</span>
        </div>
        <template v-else>
          <p>Получены данные:</p>
          <p v-for="task of tasks" :key="task.id">
            {{ task.task + categoryName(task) }}
          </p>
        </template>
      </div>
    </section>
  </div>
</template>

<script>
import PropsTransferGrandParent from "../components/PropsTransferGrandParent";
import axios from "axios";

export default {
  name: "Home",
  components: {
    PropsTransferGrandParent,
  },
  props: ["isAppLoaded", "tasks"],
  data() {
    return {
      url: "https://www.d-skills.ru/45_lifeplan/php/gettasks.php",
      ajaxtime: "",
      fetchtime: "",
      axiostime: "",
    };
  },
  methods: {
    ajaxRequest() {
      const xhr = new XMLHttpRequest();
      const request = JSON.stringify({
        id: 1,
        name: "mihail",
      });
      let startDate;
      let finishDate;
      startDate = new Date();
      xhr.open("POST", this.url, true);
      // xhr.responseType = "json";
      xhr.onreadystatechange = () => {
        if (xhr.readyState === 4 && xhr.status === 200) {
          finishDate = new Date();
          console.log(finishDate - startDate);
          this.ajaxtime = finishDate - startDate;
          console.log(xhr.response);
        }
      };
      // xhr.setRequestHeader("Content-type", "application/json");
      xhr.send(request);
    },

    async fetchRequest() {
      let startDate;
      let finishDate;
      const user = {
        id: 1,
        name: "mihail",
      };
      const request = {
        method: "POST",
        body: JSON.stringify(user),
      };
      startDate = new Date();
      let result = await fetch(this.url, request);
      finishDate = new Date();
      console.log(finishDate - startDate);
      this.fetchtime = finishDate - startDate;
      let responseText = await result.text();
      console.log(responseText);
      // let result = await response.json();
    },

    async axiosRequest() {
      let startDate;
      let finishDate;
      const request = JSON.stringify({
        id: 1,
        name: "mihail",
      });
      startDate = new Date();
      let result = await axios.post(this.url, request);
      finishDate = new Date();
      this.axiostime = finishDate - startDate;
      console.log(finishDate - startDate);
      // let responseText = await result.text()
      console.log(JSON.stringify(result.data));
    },

    categoryName(task) {
      const result = task.categoryid ? " (категория - " + task.category.name + ")" : "";
      return result;
    },
  },

  computed: {},
  mounted() {},
};
</script>
