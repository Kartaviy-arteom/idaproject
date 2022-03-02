<template>
  <div class="sort">
    <select class="sort__select" name="sort" id="card-sort" v-model="select" v-on:change.prevent.stop="sort">
      <option value="default">По умолчанию</option>
      <option value="ascending">По возрастанию цены</option>
      <option value="descending">По убыванию цены</option>
      <option value="alphabetical">По наименованию</option>
    </select>
  </div>
</template>

<script>
export default {
  data () {
    return {
      select: 'default'
    }
  },
  methods: {
    sort () {
      this.$emit('sort', this.select)
    }
  }
}
</script>
