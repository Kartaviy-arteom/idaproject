<template>
  <section class="board container">
    <SvgSprite />
    <h1 class="visually-hidden">Ввод и редактирование списка товаров</h1>
    <div class="board__header">
      <h2 class="board__title">Добавление товара</h2>
      <SortComponent class="board__sort" v-on:sort="onSortClick"/>
    </div>
    <div class="board__wrapper">
      <div class="board__form-wrapper">
        <FormComponent class="board__form" :products="products" v-on:sendForm="onSendForm"/>
      </div>
      <transition-group name="list" tag="ul" appear class="board__list">
        <CardComponent v-for="product in copyArray" :key="product.id" :productData="product" v-on:deleteCard="onDeleteCard" />
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
      this.copyArray = this.products.slice()
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
      this.copyArray = this.products.slice()
    },

    onSortClick (option) {
      switch (option) {
        case 'ascending':
          this.copyArray.sort((a, b) => a.price.replace(/\s+/g, '') - b.price.replace(/\s+/g, ''))
          break
        case 'descending':
          this.copyArray.sort((a, b) => b.price.replace(/\s+/g, '') - a.price.replace(/\s+/g, ''))
          break
        case 'alphabetical':
          this.copyArray.sort((a, b) => (a.productName > b.productName) ? 1 : -1)
          break
        default:
          this.copyArray = this.products.slice()
      }
    }

  },

  data: () => ({
    copyArray: [],
    products: [
      {
        id: '1',
        imagePath: require('../assets/img/product.jpg'),
        productName: 'C.Наименование товара',
        description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: '20 000'
      },
      {
        id: '2',
        imagePath: require('../assets/img/product.jpg'),
        productName: 'A.Наименование товара',
        description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: '10 000'
      },
      {
        id: '3',
        imagePath: require('../assets/img/product.jpg'),
        productName: 'B.Наименование товара',
        description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: '30 000'
      }
    ]
  })
}
</script>
