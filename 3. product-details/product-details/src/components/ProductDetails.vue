<template>
  <div class="item" :class="{ 'hided': this.hided, 'not-availiable': !product.availiable }" @click="hided = !hided">

    <div class="item__brief-info">
      <slot></slot>
    </div>
    <div class="item__full-info" v-if="!this.hided">
      <div class="item__info">
        <div class="item__name"> {{ `Товар ${product.name} ${product.availiable ? ' (available)' : ''}` }}</div>
        <div class="item__price" v-if="product.price"> {{ `Цена ${product.price} $ ` }}</div>
      </div>

      <div class="item__count" v-if="product.count">
        {{ `в корзине ${product.count} шт.` }}
      </div>
      <div class="item__sum">
        {{ `Итого ${formattedPrice} ` }}
      </div>
    </div>

  </div>
</template>
<script>
export default {
  name: 'ProductDetails',
  props: {
    product: {
      type: Object,
      required: true,
      validator: (val) => {
        const struct = Boolean(val.name)

        let types = true
        if (val.count) types = types && typeof (val.count) === 'number'
        if (val.price) types = types && typeof (val.price) === 'number'

        if (!(types && struct)) alert('Неправильные исходные данные ' + val.name)
        return types && struct
      }
    },
    max_width: {
      type: String,
      required: false,
      default: '100vw'
    }
  },
  data () {
    return {
      hided: true
    }
  },
  computed: {
    formattedPrice () {
      if (!this.product.price) return 'Ошибка'
      const count = this.product.count || 0

      return '$' + this.product.price * count
    }
  }

}
</script>

<style lang="scss" scoped>
.item {
  width: fit-content;
  margin: 6px 6px;

}

div:not(.hided).item.not-availiable {
  background: gray;
  position: relative;

  &::after {
    content: "Out of stock";
    position: absolute;
    color: rgb(163, 27, 27);
    background: white;
    display: inline-block;
    font-size: 2em;

    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
  }
}

div:not(.hided).item {

  background: rgb(86, 160, 141);
  color: white;

  .item {
    &__brief-info {
      background: black;
      width: 40vw;
      max-width: v-bind(max_width);
      min-width: 100%;
    }

    &__full-info {
      display: flex;
      justify-content: space-between;
      flex-direction: column;
    }

    &__info {
      display: flex;
      justify-content: space-between;
      padding: 0px 35px 0px 20px;
    }

    &__count,
    &__sum {
      display: flex;
      justify-content: end;
    }

    &__count {
      padding: 17px 12px 0px 20px;
    }

    &__sum {
      padding: 0px 14px 0px 19px;
    }

  }
}
</style>
