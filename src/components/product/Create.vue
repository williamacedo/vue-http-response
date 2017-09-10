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
              <button @click="create" class="btn btn-default pull-right" v-show="product.name && product.url && product.lat && product.lng">Enviar</button>
            </div>
          </div>
        </div>
      </div>
</template>

<script>
  export default {
    data(){
      return{
        product:  {
          name: '',
          url:  '',
          lat:  '',
          lng:  ''
        }
      }
    },
    methods: {
      create () {
        this.$http.post('api/products', this.product)
          .then(response => {
            this.$router.push('/feed')
          })
      },
    }
  }
</script>

<style lang="css">
</style>
