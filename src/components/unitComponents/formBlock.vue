<template>
  <div>
        <h1 @click="showForm">Добавление товара</h1>
      <div :class="{ 'block-form__show': isActiveShowForm }" class="block-form">

        <label for="title">Наименование товара</label>
        <input
          @blur="checkTitle"
          :class="{ 'inp-error': errorTittle }"
          id="title"
          v-model="title"
          placeholder="Введите наименование товара"
        >
        <p v-if="errorTittle">Поле является обязательным</p>

        <span>Описание товара</span>
        <textarea
          id="description"
          v-model="description"
          placeholder="Введите описание товара"
        >
        </textarea>

        <label for="img">Ссылка на изображение товара</label>
        <input
          @blur="checkImg"
          :class="{ 'inp-error': errorImg}"
          id="img"
          v-model="img"
          placeholder="Введите ссылку"
        >
        <p v-if="errorImg">Поле является обязательным</p>

        <label for="price">Цена товара</label>
        <input
          @blur="checkPrice"
          @focus="changePrice"
          placeholder="Введите цену"
          :class="{ 'inp-error': errorPrice }"
          id="price"
          v-model="price"
        >
        <p v-if="errorPrice">Поле является обязательным и должно быть числом</p>

        <button
          @click="addProduct()"
          :class="{ 'btn-active': !activityBtn()}"
          :disabled="activityBtn()"
        >Добавить товар</button>
      </div>
  </div>
</template>

<script>
export default {
  name: 'formBlock',
  data () {
    return {
      isActiveShowForm: false,
      title: '',
      description: '',
      price: '',
      img: '',
      errorTittle: false,
      errorPrice: false,
      errorImg: false
    }
  },
  methods: {
    // Добавление товара
    addProduct () {
      let itemProduct = {}
      itemProduct.title = this.title
      itemProduct.description = this.description
      itemProduct.img = this.img
      itemProduct.price = this.price
      itemProduct.hideProduct = false
      this.$emit('item', itemProduct)
      this.title = ''
      this.description = ''
      this.img = ''
      this.price = ''
    },
    // Валидация наименования
    checkTitle () {
      this.errorTittle = !this.title
    },
    // Валидация ссылки изображения
    checkImg () {
      this.errorImg = !this.img
    },
    // Валидация цены
    checkPrice () {
      // eslint-disable-next-line
      if ((this.price ^ 0) == this.price && this.price) {
        this.errorPrice = false
        this.price = this.price.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ' ')
      } else {
        this.errorPrice = true
      }
    },
    // Редактирование цены
    changePrice () {
      if (this.price) {
        this.price = this.price.split(' ').join('')
      }
    },
    // Скрытие/показ формы для мобильных устройств
    showForm () {
      if (window.innerWidth <= 640) {
        this.isActiveShowForm = !this.isActiveShowForm
      }
    },
    // Активация кнопки
    activityBtn () {
      return !(this.title && this.img && String(parseInt(this.price.split(' ').join(''), 10)) === String(this.price.split(' ').join('')))
    }
  }
}
</script>

<style scoped>
.block-form{
  padding: 24px;
  background: #FFFEFB;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  text-align: left;
  position:-webkit-sticky;
  position:sticky;
  top: 24px;
}
h1, label, span {
  text-align: left;
}
h1{
  font-weight: 600;
  font-size: 28px;
  line-height: 35px;
  margin-top: -53px;
}
label, span{
  font-size: 13px;
  line-height: 13px;
}
label::after{
  content: '';
  display: inline-block;
  width: 5px;
  height: 5px;
  background: #FF8484;
  border-radius: 50%;
  position: absolute;
}
p{
  color: #FF8484;
  font-size: 11px;
  margin: 0;
}
input{
  width: 100%;
  height: 36px;
  background: #FFFEFB;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  border: 0;
  font-size: 12px;
  line-height: 15px;
  color: #B4B4B4;
}
input:focus-visible{
  border: 1px solid #7BAE73;
}
.inp-error{
  border: 1px solid #FF8484;
}
input:active, :hover, :focus {
  outline: 0;
  outline-offset: 0;
}
textarea{
  width: 100%;
  height: 108px;
  background: #FFFEFB;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  border: 0;
  resize: none;
  font-family: 'Source Sans Pro';
}
input,textarea{
  margin-bottom: 16px;
}

button{
  width: 100%;
  height: 36px;
  background: #EEEEEE;
  border-radius: 10px;
  border: 0;
  margin-top: 8px;
  font-weight: 600;
  font-size: 12px;
  line-height: 15px;
  text-align: center;
  letter-spacing: -0.02em;
  color: #B4B4B4;
}
.btn-active{
  background: #7BAE73;
  color: #FFFFFF;
}
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
@media (max-width: 640px) {
  .block-form__show{
    max-height: 700px !important;
    -webkit-transition: max-height .5s, padding .5s !important;
    transition: max-height .5s, padding .5s !important;
    padding: 24px !important;
  }
  .block-form{
    max-height: 0;
    overflow: hidden;
    transition: height 500ms ease;
    padding: 0;
  }
  h1{
    margin-top: 0;
    background: #FF8484;
    border-radius: 5px;
    font-size: 20px;
    position: relative;
    text-align: center;
  }

  h1::after {
    border-style: solid;
    border-width: 0.15em 0.15em 0 0;
    content: '';
    display: inline-block;
    height: 0.35em;
    right: 20px;
    top: 10px;
    vertical-align: top;
    width: 0.35em;
    transform: rotate(135deg);
    position: absolute;
  }
}
</style>
