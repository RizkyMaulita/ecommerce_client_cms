<template>
  <tr>
    <th>{{ index + 1 }} </th>
    <td><img :src="product.image_url" alt="" class="img-product"></td>
    <td>{{ product.name }}</td>
    <td>Rp{{ convertRupiah }},00</td>
    <td>{{ product.stock }} </td>
    <td><button @click.prevent="onEdit(product.id)" class="btn btn-edit">Edit</button> <button @click.prevent="onDelete" type="button" class="btn btn-danger">Delete</button></td>
  </tr>
</template>

<script>
export default {
  name: 'ProductList',
  props: ['product', 'index'],
  methods: {
    onEdit (id) {
      this.$store.dispatch('editProduct', id)
    },
    onDelete () {
      this.$store.dispatch('deleteProduct', this.product.id)
    }
  },
  computed: {
    convertRupiah () {
      const numberString = this.product.price.toString()
      const sisa = numberString.length % 3
      var rupiah = numberString.substr(0, sisa)
      const ribuan = numberString.substr(sisa).match(/\d{3}/g)
      if (ribuan) {
        const separator = sisa ? '.' : ''
        rupiah += separator + ribuan.join('.')
      }
      return rupiah
    }
  }
}
</script>

<style>
  .img-product{
    width: 100px;
  }
  .table-product th{
    color: #16a592;
  }
  .btn-edit{
    background-color: #1ee2c8;
  }
</style>
