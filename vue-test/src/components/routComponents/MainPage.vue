<template>
  <div class="container">
    <modal-block
    :isShowModal="isShowModal"
    @getOpenModal="getDataModal"
    />
    <div class="block-select">
      <select v-model="selected">
        <option
          v-for="(option, index) in options"
          :value="option.value"
          :key="index"
        >{{option.text}}</option>
      </select>
    </div>
    <div class="block-products">
      <form-block
        @item="addProduct"
      />
      <product-block
        :arrProducts="sortedArr"
        @productIndex="deleteProduct"
      />
    </div>
  </div>
</template>

<script>
import ProductBlock from '../unitComponents/productBlock'
import FormBlock from '../unitComponents/formBlock'
import ModalBlock from '../unitComponents/modalBlock'
export default {
  name: 'mainPage',
  components: {
    ModalBlock,
    FormBlock,
    ProductBlock
  },
  data () {
    return {
      isShowModal: false,
      options: [
        { text: 'По умолчанию', value: 'default' },
        { text: 'По цене min', value: 'priceMin' },
        { text: 'По цене max', value: 'priceMax' },
        { text: 'По наименованию', value: 'title' }
      ],
      selected: 'default',
      arrProducts: [
        {
          title: 'Наименование товара 2',
          img: '../../../static/imgProduct.jpg',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько стро Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: '10 000',
          hideProduct: false
        },
        {
          title: 'Наименование товара 1',
          img: '../../../static/imgProduct.jpg',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: '14 000',
          hideProduct: false
        },
        {
          title: 'Наименование товара 4',
          img: '../../../static/imgProduct.jpg',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: '5 000',
          hideProduct: false
        },
        {
          title: 'Наименование товара 3',
          img: '../../../static/imgProduct.jpg',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: '11 000',
          hideProduct: false
        }
      ]
    }
  },
  methods: {
    // Добавление товара
    addProduct (data) {
      this.arrProducts.push(data)
      this.isShowModal = true
      this.saveProducts()
    },
    // Удаление товара
    deleteProduct (data) {
      this.arrProducts.splice(data, 1)
      this.saveProducts()
    },
    // Получение данных о модальном окне
    getDataModal (data) {
      this.isShowModal = data
    },
    // Сохранение товаров в localStorage
    saveProducts () {
      let parsed = JSON.stringify(this.arrProducts)
      localStorage.setItem('arrProducts', parsed)
    },
    // Сортировка по возрастанию цены
    sortPriceMin () {
      return this.arrProducts.sort((a, b) => a.price.split(' ').join('') - b.price.split(' ').join(''))
    },
    // Сортировка по убыванию цены
    sortPriceMax () {
      return this.arrProducts.sort((a, b) => b.price.split(' ').join('') - a.price.split(' ').join(''))
    },
    // Сортировка по названию
    sortTittle () {
      return this.arrProducts.sort((a, b) => a.title.toLowerCase() > b.title.toLowerCase() ? 1 : -1)
    },
    // Получение массива товаров из localStorage
    getArrProduct () {
      if (localStorage.getItem('arrProducts')) {
        this.arrProducts = JSON.parse(localStorage.getItem('arrProducts'))
        return this.arrProducts
      } else {
        this.saveProducts()
        return this.arrProducts
      }
    },
  },
  computed: {
    // Сортировка товаров
    sortedArr () {
      switch (this.selected) {
        case 'priceMin': return this.sortPriceMin()
        case 'priceMax': return this.sortPriceMax()
        case 'title': return this.sortTittle()
        case 'default': return this.getArrProduct()
      }
    }
  }
}
</script>

<style scoped>
.container{
  padding: 0 32px;
  display: flex;
  flex-direction: column;
  z-index: 1;
}
.block-products {
  display: grid;
}

@media (max-width: 640px ){
  .container {
    padding: 0 15px;
  }
  .block-select{
    justify-content: center;
  }
  select{
    width: 100%;
  }
}
@media (min-width: 768px) and (max-width: 1000px) {
  .container {
    padding: 0 15px;
  }
}
@media (min-width: 1000px ) and (max-width: 1920px) {
  .block-products{
    grid-template-columns: 25% 75%;
  }
  .container {
    padding: 0 32px;
  }
}
@media (min-width: 1920px ) {
  .block-products{
    grid-template-columns: 25% 75%;
  }
  .container {
    padding: 0 32px;
  }
}

/*Стили сортировки*/
.block-select{
  width: 100%;
  display: flex;
  justify-content: right;
  margin-bottom: 16px;
  position: relative;
}

select{
  background: #FFFEFB;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  font-weight: 400;
  font-size: 12px;
  line-height: 15px;
  color: #B4B4B4;
  border: #FFFEFB;
  padding: 10px 0px 10px 16px;
}
select:active, select:focus{
  outline:none
}
</style>
