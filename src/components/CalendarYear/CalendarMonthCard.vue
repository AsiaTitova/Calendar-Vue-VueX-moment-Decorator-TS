<template>
  <div class="grid-year__card">
    <h2 class="grid-year__month-name"> {{setMonthName}}</h2>
    <ul class="grid-year__week-day week-day">
      <li class="week-day__item" v-for="(day, index) in weekdays" :key="index">{{ day }}</li>
    </ul>
     <CalendarMonthWeek v-for="week in month.weeks" :key="`month_${month.id}_week_${week.id}`" :week="week" />
  </div>
</template>

<script lang="ts">
import {Component, Prop, Vue} from "vue-property-decorator";
import CalendarMonthWeek from "@/components/CalendarYear/CalendarMonthWeek.vue";
import moment from "moment";
import {IMonth} from "@/store/calendarInterface";

@Component({
  components: {CalendarMonthWeek}
})
export default class CalendarMonthCard extends Vue {
  @Prop({
    type: Object,
    default: () => null
  })
  month!: IMonth | null;

  weekdays: Array<string> = ['пн', 'вт', 'ср', 'чт', 'пт', 'сб', 'вс'];

  get setMonthName() {
    return this.month ? moment(this.month.month).locale('ru').format('MMMM') : '';
  }

}
</script>

<style scoped lang="scss">
@import "~@/assets/base/colors";
@import "~@/assets/base/breakpoints";

.grid-year {
  &__card {
    width: 23%;

    @media (max-width: $xxl) {
      width: 30%;
    }

    @media (max-width: $xl) {
      width: 48%;
    }

    @media (max-width: $sm) {
      width: 100%;
    }
  }

  &__month-name {
    width: 100%;
    margin: 0 0 16px;
    font-size: 16px;
    line-height: 20px;
    text-align: right;
    color: $system-text;
  }
}

.week-day {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 0;
  padding: 0;
  list-style: none;

  &__item {
    width: 12%;
    height: 24px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: $system-surface;
    font-size: 14px;
    line-height: 20px;
    margin-bottom: 8px;
  }
}
</style>
