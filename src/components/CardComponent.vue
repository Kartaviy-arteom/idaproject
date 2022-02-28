<template>
  <li class="card">
    <div class="card__img-wrapper">
      <img :src=productData.imagePath alt="Изображение товара" width="332" height="200">
    </div>
    <div class="card__wrapper">
      <strong class="card__product-name">{{ productData.productName }}</strong>
      <div class="card__description">
        <p>{{ productData.description }}</p>
      </div>
      <div class="card__price">{{ productData.price }} руб.</div>
    </div>
    <button class="card__delete-btn" type="button" title="Удалить карточку товара">
      <svg class="card__btn-icon" width="16" height="16">
        <use xlink:href="#icon"></use>
      </svg>
    </button>
  </li>
</template>

<script>
export default {
  props: {
    productData: {
      type: Object,
      default () {
        return {}
      }
    }
  }
}
</script>
