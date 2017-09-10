<template>
  <div class="row">
    <div class="col-md-8 col-md-offset-2">
      <div class="panel panel-default">
        <div class="panel-body">
            <div class="form-group">
                <label>Nome:</label>
                <input type="text" class="form-control" v-model="product.name">
            </div>
            <div class="form-group">
                <label>Upload:</label>
                <input type="text" v-model="product.url" class="form-control">
            </div>
            <div class="row">
                <div class="col-md-6">
                    <div class="form-group">
                        <label>Latitude:</label>
                        <input type="text" class="form-control" id="latitude" v-model="product.lat">
                    </div>
                </div>
                <div class="col-md-6">
                    <div class="form-group">
                        <label>Longitude:</label>
                        <input type="text" class="form-control" id="longitude" v-model="product.lng">
                    </div>
                </div>
              </div>
              <button @click="update" class="btn btn-default pull-right" v-show="product.name && product.url && product.lat && product.lng">Update</button>
            </div>
          </div>
        </div>
      </div>
</template>

<script>
  import swal from 'sweetalert'
  export default {
    created ()  {
      this.getProduct()
    },
    data(){
      return{
        product:  {}
      }
    },
    methods: {
      getProduct  ()  {
        this.$http.get('api/products/'  + this.$route.params.product)
          .then(response  =>  {
            this.product  = response.body
          })
      },

      update () {
        this.$http.put('api/products/' +  this.$route.params.product, this.product)
          .then(response => {
            swal("Updated!", "Your product has been updated!", "success")
          })
      }
    }
  }
</script>

<style lang="css">
</style>
