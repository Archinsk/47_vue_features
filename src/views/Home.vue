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
  </div>
</template>

<script>
import PropsTransferGrandParent from "../components/PropsTransferGrandParent";

export default {
  name: "Home",
  components: {
    PropsTransferGrandParent,
  },
};
</script>
