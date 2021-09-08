<template>
  <section id="app">
    <div class="container">
      <div class="row">
        <div class="col-12 my-5">
          <h1 class="heading">Products</h1>
        </div>
        <div class="col-12 col-lg-8">
          <div class="row">
            <div
              class="col-12 col-lg-4"
              v-for="item in products"
              :key="item.id"
            >
              <div class="card">
                <div class="card-body">
                  <div
                    class="card-badge"
                    :class="{
                      'card-badge--red': item.stock < 10,
                      'card-badge--blue': item.stock >= 10,
                    }"
                  >
                    {{ item.stock }}
                  </div>
                  <div class="card-wrapper">
                    <h5 class="card-title">
                      {{ item.name }}
                    </h5>
                    <div class="card-stock">
                      <h5 class="card-stock__title">Total Sold</h5>
                      <div
                        class="card-stock__item"
                        :class="{
                          'card-stock__item--green':
                            Number(biggerStockProduct) == item.id,
                        }"
                      >
                        {{ sumStock(item.id) }}
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  name: "App",
  data() {
    return {
      products: [
        {
          id: 1,
          name: "IPhone 12",
          stock: 10,
        },
        {
          id: 2,
          name: "DJI Ronin S",
          stock: 5,
        },
        {
          id: 3,
          name: "Sony A7RIII",
          stock: 23,
        },
      ],
      sales: [
        {
          product_id: 1,
          qty: 2,
        },
        {
          product_id: 1,
          qty: 1,
        },
        {
          product_id: 1,
          qty: 1,
        },
        {
          product_id: 2,
          qty: 1,
        },
        {
          product_id: 3,
          qty: 1,
        },
        {
          product_id: 2,
          qty: 1,
        },
        {
          product_id: 3,
          qty: 2,
        },
      ],
    };
  },
  methods: {
    sumStock(id) {
      return this.sales
        .filter((x) => x.product_id === id)
        .reduce((x, val) => {
          return x + val.qty;
        }, 0);
    },
  },
  computed: {
    biggerStockProduct() {
      let sumQty = this.sales.reduce(
        (a, { product_id, qty }) => (
          (a[product_id] = (a[product_id] || 0) + +qty), a
        ),
        {}
      );
      let findBiggerStockProduct = Object.keys(sumQty).reduce((a, b) =>
        sumQty[a] > sumQty[b] ? a : b
      );
      return findBiggerStockProduct;
    },
  },
};
</script>