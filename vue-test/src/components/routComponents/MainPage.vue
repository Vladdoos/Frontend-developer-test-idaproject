<template>
  <div class="container">
    <div class="block-btn">
      <button>По умолчанию</button>
    </div>
    <div class="block-products">
      <form-block/>
      <product-block :arrProducts="arrProducts"/>
    </div>
  </div>
</template>

<script>
import ProductBlock from "../unitComponents/productBlock";
import FormBlock from "../unitComponents/formBlock";
export default {
  name: 'mainPage',
  components: {
    FormBlock,
    ProductBlock
  },
  data () {
    return {
      arrProducts: [
        {
          title: 'Наименование товара',
          img: '../../../static/imgProduct.jpg',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 10000
        },
        {
          title: 'Наименование товара',
          img: '../../../static/imgProduct.jpg',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 10000
        },
        {
          title: 'Наименование товара',
          img: '../../../static/imgProduct.jpg',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 10000
        },
        {
          title: 'Наименование товара',
          img: '../../../static/imgProduct.jpg',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 10000
        }
      ]
    }
  }
}
</script>

<style scoped>
.container{
  padding: 0 32px;
  display: flex;
  flex-direction: column;
}
.block-products {
  display: grid;
}
.block-btn{
  width: 100%;
  display: flex;
  justify-content: right;
  margin-bottom: 16px;
}

button{
  width: 121px;
  height: 36px;
  background: #FFFEFB;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  font-weight: 400;
  font-size: 12px;
  line-height: 15px;
  color: #B4B4B4;
  border: #FFFEFB;
  padding: 10px;
}
button:hover{
  background: #E5E5E5;
  color: #FFFEFB;
}
button:active{
  border: 2px solid #FF8484;
}
button::after {
  border-style: solid;
  border-width: 0.15em 0.15em 0 0;
  content: '';
  display: inline-block;
  height: 0.45em;
  left: 0.15em;
  top: 0.15em;
  vertical-align: top;
  width: 0.45em;
  transform: rotate(135deg);
  margin-left: 7px;
  margin-top: 1px;
}
@media (max-width: 640px ){
  .container {
    padding: 0 15px;
  }
  .block-btn{
    justify-content: center;
  }
  button{
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
</style>
