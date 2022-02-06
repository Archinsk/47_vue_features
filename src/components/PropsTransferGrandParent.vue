<template>
  <div class="features-table">
    <div class="row table-title">
      <div class="col">Описание</div>
      <div class="col">Тип входного параметра</div>
      <div class="col">Значение</div>
    </div>
    <PropsTransferParent description="" type="Строка" :option="propString" />
    <PropsTransferParent description="" type="Число" :option="propNumber" />
    <PropsTransferParent
      description=""
      type="Логическое"
      :option="propBoolean"
    />
    <PropsTransferParent description="" type="null" :option="propNull" />
    <PropsTransferParent description="" type="undefined" />
    <PropsTransferParent description="" type="Объект" :option="propObject" />
    <PropsTransferParent description="" type="Массив" :option="propArray" />
    <PropsTransferParent description="" type="Дата" :option="propDate" />
    <PropsTransferParent description="" type="Функция" :option="propFunction" />
    <PropsTransferParent description="" type="Символ" :option="propSymbol" />
    <ButtonIconSquare @click-handler="refresh" icon="refresh" class="btn-primary mt-3" />
  </div>
</template>

<script>
import PropsTransferParent from "./PropsTransferParent";
import ButtonIconSquare from "./universal/ButtonIconSquare";

export default {
  name: "PropsTransferGrandParent",

  components: {
    PropsTransferParent,
    ButtonIconSquare,
  },

  data() {
    return {
      propString: "OldString",
      propNumber: 13,
      propBoolean: false,
      propNull: null,
      propArray: [1, 2, 3, 4, 5],
      propObject: {
        user: {
          firstName: "John",
          lastName: "Doe",
          skills: {
            professional: "programming",
            amateur: "football",
          },
        },
      },
      propDate: new Date(1587186000),
      propFunction: function multiplication(value) {
        return value * 2;
      },
      propSymbol: Symbol("id"),
    };
  },

  methods: {
    refresh() {
      this.propString = "NewString";
      this.propNumber = 258;
      this.propBoolean = true;
      this.propArray = [10, 9, 8, 7, 6];
      this.propObject = {
        user: {
          firstName: "Robert",
          lastName: "Smith",
          skills: {
            professional: "analytics",
            amateur: "chess",
          },
        },
      };
      this.propDate = new Date(1300000000000);
      this.propFunction = function multiplication(value) {
        return value * 3;
      };
      this.propSymbol = Symbol("user");
      console.log("Обновление значений прародителя");
    },
  },
};
</script>

<style lang="scss" scoped></style>
