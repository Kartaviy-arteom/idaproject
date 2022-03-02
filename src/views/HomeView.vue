<template>
  <section class="board container">
    <SvgSprite />
    <h1 class="visually-hidden">Ввод и редактирование списка товаров</h1>
    <div class="board__header">
      <h2 class="board__title">Добавление товара</h2>
      <SortComponent class="board__sort" />
    </div>
    <div class="board__wrapper">
      <div class="board__form-wrapper">
        <FormComponent class="board__form" :products="products" v-on:sendForm="onSendForm"/>
      </div>
      <transition-group name="list" tag="ul" appear class="board__list">
        <CardComponent v-for="product in products" :key="product.id" :productData="product" v-on:deleteCard="onDeleteCard" />
      </transition-group>
    </div>
  </section>
</template>

<script>
import SvgSprite from '@/components/SvgSprite.vue'
import SortComponent from '@/components/SortComponent.vue'
import FormComponent from '@/components/FormComponent.vue'
import CardComponent from '@/components/CardComponent.vue'

export default {
  name: 'HomeView',
  components: {
    SvgSprite,
    SortComponent,
    FormComponent,
    CardComponent
  },

  mounted () {
    if (localStorage.products) {
      this.products = JSON.parse(localStorage.getItem('products'))
    } else {
      this.saveData()
    }
  },

  methods: {
    onSendForm (data) {
      this.products.push(data)
      this.saveData()
    },
    onDeleteCard (data) {
      const index = this.products.indexOf(data)
      if (index !== -1) {
        this.products.splice(index, 1)
      }
      this.saveData()
    },
    saveData () {
      localStorage.setItem('products', JSON.stringify(this.products))
    }
  },

  data: () => ({
    products: [
      {
        id: '1',
        imagePath: require('../assets/img/product.jpg'),
        productName: 'Наименование товара',
        description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: '10 000'
      },
      {
        id: '2',
        imagePath: require('../assets/img/product.jpg'),
        productName: 'Наименование товара',
        description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: '10 000'
      },
      {
        id: '3',
        imagePath: require('../assets/img/product.jpg'),
        productName: 'Наименование товара',
        description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: '10 000'
      }
    ]
  })
}
</script>
