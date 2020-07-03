<template>
  <div class="container">
        <div class="card">
            <div class="card-header">
                <h3>Edit Item</h3>
            </div>
            <div class="card-body">
                <form v-on:submit.prevent="updateItem">
                     <div class="form-group">
                        <label>Id:</label>
                      <input type="text" disabled class="form-control" v-model="item.id"/>
                    </div>
                   <div class="form-group">
                        <label>Item Name:</label>
                      <input type="text" class="form-control" v-model="item.name"/>
                    </div>
                    <div class="form-group">
                        <label>Item Quantity</label>
                      <input type="text" class="form-control" v-model="item.quantity"/>
                    </div>
                      <div class="form-group">
                        <label>Price</label>
                        <input type="text" class="form-control" v-model="item.price"/>
                    </div>
                    <div class="form-group">
                        <input type="submit" class="btn btn-primary" value="Update Item"/>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>
<script>
export default{
        data(){
            return{
                item:{}
            }
        },
        created: function(){
            this.getItem();
        },
        methods: {
            getItem()
            {
              let uri = 'http://localhost:8013/productById/' + this.$route.params.id;
                this.axios.get(uri).then((response) => {
                    this.item = response.data;
                });
            },
            updateItem()
            {
              let uri = 'http://localhost:8013/update/'+ this.$route.params.id;
                this.axios.put(uri, this.item).then((response) => {
                  this.$router.push({name: 'home'});
                    this.item = response.data;
                });
            }
        }
    }
</script>