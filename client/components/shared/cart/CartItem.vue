<template>
  <div
    class="relative flex flex-row items-center px-2 my-2 transition-all duration-300 color-primary custom-rounded"
  >
    <div v-if="!onCheckout" class="absolute top-0 left-0 w-4 h-4 text-center transition color-primary rounded-full border border-white cursor-pointer shadow ripple btn-hover focus:outline-none">
      <div
        v-tooltip="'Remover del carrito'"
        @click="remove(cartItem)"
      >
        <img :src="cancel">
      </div>
    </div>
    <img
      :src="cartItem.product.imageUrl"
      class="w-12 h-12 my-auto custom-rounded"
      alt="Product image"
    >
    <div class="flex flex-col w-full mx-2 truncate">
      <span class="text-white truncate">{{ cartItem.product.title }} </span>
      <div>
        <span class="text-white">DOP {{ cartItem.product.price }}</span>
      </div>
    </div>
    <div class="flex items-center text-lg font-bold text-white-500 bg-button">
      <div
        v-if="!onCheckout"
        v-tooltip="'Disminuir cantidad'"
        class="w-6 cursor-pointer select-none"
        @click="decrement(cartItem)"
      >
        <img
          :src="minus"
          alt="-"
          class="py-4 pointer-events-none"
          draggable="false"
        >
      </div>
      <input
        type="number"
        name="quantity"
        min="1"
        :value="cartItem.quantity"
        class="w-8 py-3 font-bold text-center text-white bg-transparent"
      >
      <div
        v-if="!onCheckout"
        v-tooltip="'Incrementar cantidad'"
        class="w-6 cursor-pointer select-none"
        @click="increment(cartItem)"
      >
        <img
          :src="plus"
          alt="+"
          class="py-4 pointer-events-none"
          draggable="false"
        >
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex'
import plus from '@/assets/plus.png'
import minus from '@/assets/minus.png'
import cancel from '@/assets/cancel.svg'
export default {
  name: 'CartItem',
  props: {
    cartItem: {
      type: Object,
      required: true
    },
    // If it is true will be disabled some functions of cart for review in checkout view
    onCheckout: {
      type: Boolean
    }
  },
  data () {
    return {
      plus,
      minus,
      cancel
    }
  },
  methods: {
    ...mapActions('cart', {
      remove: 'removeProductFromCart',
      increment: 'incrementProductQuantity',
      decrement: 'decrementProductQuantity'
    })
  }
}
</script>

<style scoped>
/* Chrome, Safari, Edge, Opera */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
/* Firefox */
input[type='number'] {
  -moz-appearance: textfield;
}
</style>
