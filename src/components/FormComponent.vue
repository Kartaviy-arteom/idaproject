<template>
  <form class="form" action="" method="post" autocomplete="off" @submit.prevent = "onSubmit">
    <p>
      <label for="product-name">Наименование товара</label>
      <input type="text" name="product-name" id="product-name" required placeholder="Введите наименование товара" v-model="name">
    </p>
    <p>
      <label for="description">Описание товара</label>
      <textarea name="description" id="description" placeholder="Введите описание товара"></textarea>
    </p>
    <p>
      <label for="link">Ссылка на изображение товара</label>
      <input type="text" name="link" id="link" required placeholder="Введите ссылку" v-model="link">
    </p>
    <p>
      <label for="price">Цена товара</label>
      <input type="text" name="price" id="price" required placeholder="Введите цену" pattern="[0-9.]+" v-model="price">
    </p>
    <button type="submit" :disabled="!isFormValid">Добавить товар</button>
  </form>
</template>

<script>
export default {
  computed: {
    isFormValid () {
      return false
    }
  },
  methods: {
    // isFormValid () {
    //   return !this.name
    // }
  }
}
</script>
