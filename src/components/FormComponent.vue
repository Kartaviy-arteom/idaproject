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
      <input type="text" name="price" id="price" required placeholder="Введите цену" pattern="[0-9.]+" v-model="price" @input="checkForm">
    </p>
    <button type="submit" :disabled="!isFormValid">Добавить товар</button>
  </form>
</template>

<script>
export default {
  data () {
    return {
      formPrice: null,
      isEmailTouched: false
    }
  },

  computed: {
    isFormValid () {
      return this.checkForm()
    }
  },
  methods: {
    checkForm (evt) {
      if (evt) {
        evt.target.value = this.price.replace(/\D/g, '').replace(/^(\d{1,3})(\d{3})/, '$1 $2 ')
      }
      console.log(this.price)
    }
  }
}
</script>
