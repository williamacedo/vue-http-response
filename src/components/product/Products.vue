<template>
  <table class="table table-bordered">
    <thead>
      <tr>
        <th>ID</th>
        <th>Nome</th>
        <th>Username</th>
        <th>Url</th>
        <th>Lat</th>
        <th>Lng</th>
        <th>Date</th>
        <th>Actions</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="product in products"
      @delete-product = "deleteProduct(product.id)"
      :authenticatedUser="authenticatedUser"
      :product="product">
        <td>{{product.id}}</td>
        <td>{{product.name}}</td>
        <td>{{product.user_id}}</td>
        <td>{{product.url}}</td>
        <td>{{product.lat}}</td>
        <td>{{product.lng}}</td>
        <td>{{product.created_at}}</td>
        <td v-if="product.user_id == authenticatedUser.id">
          <a href="#" style="float:left" class="btn btn-danger" role="button" @click="deleteProduct(product.id)">
            Delete
          </a>

          <router-link :to="'/products/' + product.id + '/edit'" class="btn btn-warning" style="float:left">
            Edit
          </router-link>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
  //import Product from './Product.vue'
  import swal from 'sweetalert'
  export default {
    props:  ['product'],
    data()  {
      return {
        products: []
      }
    },

    computed: {
      authenticatedUser ()  {
        return this.$auth.getAuthenticatedUser()
      }
    },

    created ()  {
      this.$http.get('api/products')
        .then(response  =>  {
          this.products = response.body
        })
    },

    methods:  {
      deleteProduct (product)  {
        swal({
          title: "Are you sure?",
          text: "Once deleted, you will not be able to recover this product!",
          icon: "warning",
          buttons: true,
          dangerMode: true,
        })
        .then((willDelete) => {
          if (willDelete) {
            this.$http.delete('api/products/' + product)
              .then(response  =>  {
                let index = this.products.indexOf(product)

                this.products.splice(index, 1)
              })
            swal("Poof! Your product has been deleted!", {
              icon: "success",
            }
          );
          }
        });
      }
    },
  }
</script>

<style lang="css">
</style>
