<template>
  <form class="form" action="" method="post" autocomplete="off">
    <p>
      <label for="product-name">Наименование товара</label>
      <input type="text" name="product-name" id="product-name" required placeholder="Введите наименование товара">
    </p>
    <p>
      <label for="description">Описание товара</label>
      <textarea name="description" id="description" placeholder="Введите описание товара"></textarea>
    </p>
    <p>
      <label for="link">Ссылка на изображение товара</label>
      <input type="text" name="link" id="link" required placeholder="Введите ссылку">
    </p>
    <p>
      <label for="price">Цена товара</label>
      <input type="text" name="price" id="price" required placeholder="Введите цену" pattern="[0-9.]+">
    </p>
    <button type="submit">Добавить товар</button>
  </form>
</template>
