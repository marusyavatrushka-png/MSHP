<template>
  <div id="app">
    <div class="container mt-4">
      <div class="row">
        <div class="col-12 text-center">
          <h1>Магазин товаров</h1>
        </div>
      </div>
      <div class="row mt-4">
        <div v-for="item in items" :key="item.id" class="col-12 col-md-6 col-lg-4 mb-4">
          <div class="card h-100">
            <div class="card-body">
              <h5 class="card-title">{{ item.name }}</h5>
              <p class="card-text">Цена: {{ item.price }} ₽</p>
              <p class="card-text">В наличии: {{ item.inStock ? ' Да' : ' Нет' }}</p>
              <button 
                class="btn btn-primary"
                @click="addToCart(item)"
                :disabled="!item.inStock"
              >
                В корзину
              </button>
            </div>
          </div>
        </div>
      </div>
      <div class="row mt-5">
        <div class="col-12">
          <div class="card">
            <div class="card-body">
              <h5> Корзина ({{ cart.length }})</h5>
              <div v-if="cart.length === 0" class="text-muted">
                Корзина пуста
              </div>
              <ul class="list-group" v-else>
                <li v-for="(item, idx) in cart" :key="item.id" class="list-group-item d-flex justify-content-between">
                  {{ item.name }} - {{ item.price }} ₽
                  <button class="btn btn-sm btn-danger" @click="removeFromCart(idx)">Удалить</button>
                </li>
              </ul>
              
              <hr v-if="cart.length > 0">
              <h6 v-if="cart.length > 0">Итого: {{ totalPrice }} ₽</h6>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      items: [
        { id: 1, name: 'Ноутбук', price: 50000, inStock: true },
        { id: 2, name: 'Мышь', price: 1500, inStock: true },
        { id: 3, name: 'Клавиатура', price: 3000, inStock: false },
        { id: 4, name: 'Монитор', price: 25000, inStock: true }
      ],
      cart: []
    }
  },
  computed: {
    totalPrice() {
      return this.cart.reduce((sum, item) => sum + item.price, 0)
    }
  },
  methods: {
    addToCart(item) {
      this.cart.push(item)
    },
    removeFromCart(index) {
      this.cart.splice(index, 1)
    }
  }
}
</script>

<style>
body {
  background: #f0f2f5;
}
.card {
  transition: transform 0.2s;
}
.card:hover {
  transform: translateY(-3px);
}
</style>