<template>
<div>
    <ul class="list-group">
        <h1 class="text-center">Products added to cart</h1>
        <li class="list-group-item" :key="item.id" v-for="item in items">
            {{item.title}} - ${{ item.price }}
            <button class="btn badge badge-danger float-rigth" @click="$emit('remove-from-cart', item)">Remove from cart</button>
        </li>
    </ul>
    <div class="cart p-3 my-5">
        <h4 class="text-center">${{total}}</h4>
    </div>
    <button :disabled="items.length === 0" @click="$emit('pay')" class="btn btn-info form-control">Pay Now</button>
</div>
</template>

<script>
export default {
    props: ['items'],
    computed: {
        total(){
            return this.items.reduce((acc, item) => acc + Number(item.price), 0);
        }
    }
}
</script>

