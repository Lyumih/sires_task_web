<template lang="pug">
  .headline
    .filters
      .filter
        a-icon(type='filter')
        span.name СОРТИРОВКА:
        a-select.select(:defaultValue='0', @change='changeSort')
          a-select-option(v-for='sortType,index in sort' :value='index') {{sortType.name}}
      .filter(v-if='$route.name!=="Входящие"')
        a-icon(type='project')
        span.name Проект:
        a-select.select(defaultValue='datedesc')
          a-select-option(value='datedesc') Любой
          a-select-option(value='alphdesc') от А до Я
          a-select-option(value='alphdesc') от Я до А
    .spacer
    .add(@click='addTask')
      i.la.icon 
      span НОВАЯ ЗАДАЧА
</template>
<script>
export default {
  data () {
    return {
      sort: [
        {
          name: 'По возрастанию дедлайна',
          type: 'date',
          desc: true
        },{
          name: 'По убыванию дедлайна',
          type: 'date',
          desc: false
        },{
          name: 'от А до Я',
          type: 'alphabet',
          desc: false
        },{
          name: 'от Я до А',
          type: 'alphabet',
          desc: true
        },
      ]
    }
  },
  methods: {
    changeSort (index) {
      this.$emit('sort', this.sort[index])
    },
    addTask () {
      this.$store.dispatch('addTask')
    }
  }
}
</script>

<style lang="sass" scoped>
.headline
  display: flex
  .add
    display: flex
    align-items: center
    user-select: none
    color: $primary-color
    font-size: 12px
    i
      color: $primary-color
      font-size: 18px
    &:hover
      cursor: pointer
    span
      margin-left: 5px
      font-weight: 500
  .filters
    display: flex
    align-items: center
    .filter
      display: flex
      align-items: center
      font-size: 12px
      font-weight: 500
      margin-right: 23px
      i
        color: #778ca2
        font-size: 18px
      .name
        color: #778ca2
        margin-left: 6px
        margin-right: 10px
</style>
