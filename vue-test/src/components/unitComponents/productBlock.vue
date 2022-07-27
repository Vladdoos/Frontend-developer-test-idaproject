<template>
  <div class="block-products">
    <div class="block-products__product" v-for="item of arrProducts">
      <div class="showDel"></div>
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
</template>

<script>
export default {
  name: "productBlock",
  props: {
    arrProducts: []
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
}
.product-text{
  padding: 16px;
}
img{
  width: 100%;
}
h1,h2, p{
  text-align: left;
}
h1{
  font-weight: 600;
  font-size: 20px;
  margin-top: 0;
  margin-bottom: 16px;
}
h2{
  font-weight: 400;
  font-size: 16px;
  line-height: 20px;
  margin-top: 0;
  margin-bottom: 32px;
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
