<template>
  <div>
    <preloader-block v-if="isVisiblePreloader"/>
    <div v-else class="block-products">
      <div
        :class="{'delete-product-block' : item.hideProduct}"
        class="block-products__product modal-visible"
        v-for="(item, index) of arrProducts"
        :key="index"
      >
        <div
          @click="hideProduct(item, index)"
          class="showDel"
        ></div>
        <div class="product-img">
          <img :src="item.img" alt="logo">
        </div>
        <div class="product-text">
          <h1>{{item.title}}</h1>
          <h2>{{item.description}}</h2>
          <p>{{item.price}} руб.</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import PreloaderBlock from './preloaderBlock'
export default {
  name: 'productBlock',
  components: {
    PreloaderBlock
  },
  props: {
    arrProducts: Array
  },
  data () {
    return {
      isVisiblePreloader: true
    }
  },
  mounted () {
    if (this.isVisiblePreloader) {
      setTimeout(() => this.hidePreloader(), 400)
    }
  },
  methods: {
    // Скрыть прелоадер
    hidePreloader () {
      this.isVisiblePreloader = false
    },
    // Плавное скрытие удаляемого товара и
    // Передача индекса в родительский компонент удаляемого товара
    hideProduct (item, index) {
      item.hideProduct = true
      setTimeout(() => this.$emit('productIndex', index), 400)
    }
  }
}
</script>

<style scoped>
.block-products {
  display: grid;
}
.block-products__product{
  display: block;
  cursor: pointer;
  position: relative;
  border: 1px solid #FFFEFBCC;
  background: #FFFEFB;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  margin: 0 8px 16px;
  opacity: 1;
  -webkit-transition: opacity 400ms ease-in;
  -moz-transition: opacity 400ms ease-in;
  transition: opacity 400ms ease-in;
}
.delete-product-block {
  opacity: 0;
  -webkit-transition: opacity 400ms ease-in;
  -moz-transition: opacity 400ms ease-in;
  transition: opacity 400ms ease-in;
}
.product-text{
  padding: 16px;
}
.product-img{
  height: 200px;
}
img{
  object-fit: cover;
  width: 100%;
  height: 100%;
}
h1,h2, p{
  text-align: left;
}
h1{
  font-weight: 600;
  font-size: 20px;
  margin-top: 0;
  margin-bottom: 16px;
  overflow: hidden;
  display: -webkit-box;
  -webkit-line-clamp: 1;
  -webkit-box-orient: vertical;
}

h2{
  font-weight: 400;
  font-size: 16px;
  line-height: 20px;
  margin-top: 0;
  margin-bottom: 32px;
  height: 80px;
  overflow: hidden;
  display: -webkit-box;
  -webkit-line-clamp: 4;
  -webkit-box-orient: vertical;
}
p{
  font-weight: 600;
  font-size: 24px;
  line-height: 30px;
  margin: 0;
}
.block-products__product:hover{
  border: 1px solid #FF8484;
  transition-duration: 0.3s;
}

.showDel{
  background: url('../../../static/iconCard.svg') repeat-y;
  width: 40px;
  height: 40px;
  display: none;
}
@media (max-width: 640px) {
  .block-products__product{
    margin: 0 0 16px 0;
  }
  .showDel{
    display: block;
    position: absolute;
    right: 0;
    top: 0;
  }
}
@media (min-width: 768px) and (max-width: 1000px) {
  .block-products{
    grid-template-columns: 50% 50% ;
  }
  .showDel{
    display: block;
    position: absolute;
    right: 0;
    top: 0;
  }
}
@media (min-width: 1000px ) and (max-width: 1920px) {
  .block-products{
    grid-template-columns: 33% 33% 33%;
    margin-left: 8px;
    margin-right: -19px;
  }
}
@media (min-width: 1920px ) {
  .block-products{
    grid-template-columns: 33% 33% 33%;
    margin-left: 8px;
    margin-right: -19px;
  }
}
@media  (min-width: 1000px) {
.block-products__product:hover .showDel{
  display: block !important;
  position: absolute;
  right: -14px;
  top: -14px;
}
.showDel:hover{
  transform: scale(1.3);
  transition-duration: 0.3s;
}

}
</style>
