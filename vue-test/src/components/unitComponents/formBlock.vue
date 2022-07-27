<template>
  <div class="">
    <h1 @click="showForm">Добавление товара</h1>
    <div :class="{ 'block-form__show': isActive }" class="block-form">
      <p>Наименование товара</p>
      <input value="Введите наименование товара">
      <span>Описание товара</span>
      <textarea placeholder="Введите описание товара"></textarea>
      <p>Ссылка на изображение товара</p>
      <input value="Введите ссылку">
      <p>Цена товара</p>
      <input value="Введите цену">
      <button>Добавить товар</button>

    </div>
  </div>
</template>

<script>
export default {
  name: "formBlock",
  data() {
    return {
      isActive: false,
    }
  },
  methods: {
    showForm() {
      if (window.innerWidth <= 640) {
        this.isActive = !this.isActive
      }
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
  position: sticky;
  top: 24px;
}
h1, p, span {
  text-align: left;
}
h1{
  font-weight: 600;
  font-size: 28px;
  line-height: 35px;
  margin-top: -53px;
}
p, span{
  font-size: 10px;
  line-height: 13px;
}
p::after{
  content: '';
  display: inline-block;
  width: 5px;
  height: 5px;
  background: #FF8484;
  border-radius: 50%;
  position: absolute;
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
