<template>
  <form class="form" action="" method="post" autocomplete="off" v-on:submit.prevent="sendForm">
    <p>
      <label for="product-name">Наименование товара</label>
      <input type="text" name="product-name" id="product-name" required placeholder="Введите наименование товара" v-model="name" @input="checkName">
    </p>
    <p>
      <label for="description">Описание товара</label>
      <textarea name="description" id="description" v-model="description" placeholder="Введите описание товара"></textarea>
    </p>
    <p>
      <label for="link">Ссылка на изображение товара</label>
      <input type="text" name="link" id="link" required placeholder="Введите ссылку" v-model="link" @input="checkLink">
    </p>
    <p>
      <label for="price">Цена товара</label>
      <input type="text" name="price" id="price" required placeholder="Введите цену" v-model="price" @input="checkPrice">
    </p>
    <button type="submit" :disabled="!isFormValid">Добавить товар</button>
  </form>
</template>

<script>
export default {
  props: {
    products: {
      type: Array,
      default () {
        return []
      }
    }
  },
  data () {
    return {
      isPriceValid: null,
      isNameValid: null,
      isLinkValid: null,
      link: null,
      name: null,
      description: null,
      price: null
    }
  },

  computed: {
    isFormValid () {
      return (this.isNameValid && this.isPriceValid && this.isLinkValid)
    }
  },
  methods: {
    checkPrice (evt) {
      if (evt) {
        evt.target.value = evt.target.value.replace(/\D/g, '').replace(/\d{1,3}(?=(\d{3})+(?!\d))/g, '$& ')
      }
      this.isPriceValid = !!evt.target.value
    },

    checkName () {
      this.isNameValid = !!this.name
    },

    checkLink () {
      this.isLinkValid = /\w+.(gif|jpeg|jpg|png|webp)$/i.test(this.link)
    },

    resetForm () {
      this.name = this.description = this.price = this.link = ''
      this.isLinkValid = this.isPriceValid = this.isNameValid = null
    },

    sendForm (evt) {
      this.$emit('sendForm', {
        id: Math.floor((1 + Math.random()) * 0x10000).toString(16).substring(1),
        imagePath: this.link,
        productName: this.name,
        description: this.description,
        price: this.price
      })
      this.resetForm()
    }
  }
}
</script>
