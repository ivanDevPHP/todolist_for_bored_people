<template>
  <div class="item">
      <input type="checkbox" @change="update()" v-model="item.completed">
      <span :class="['itemText', item.completed? 'completed' : '']">{{item.todo}}</span>
      <button class="delete" @click="remove()">
           <font-awesome-icon
           icon="trash"
           />
      </button>
  </div>
</template>

<script>
export default {
    props: ['item'],
    methods:{
        update(){
            axios.put('api/todos/update/' + this.item.id, {
                completed: this.item.completed
            }).then(response =>{
                if(response.status >= 200 && response.status <= 300){
                    alert('Item updated succesfully');
                    this.$emit('reload');
                }
            })
        },
        remove(){
            axios.delete('api/todos/delete/' + this.item.id, {
                completed: this.item.completed
            }).then(response =>{
                if(response.status >= 200 && response.status <= 300){
                    alert('Item deleted succesfully');
                    this.$emit('reload');
                }
            })
        }
    }
}
</script>

<style>
    .item{
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .completed{
        text-decoration: line-through;
        color: #999999;
    }
    .itemText{
        width: 100%;
        margin-left: 20px;
    }
    .edit{
        color:blue;
        border-radius: 5px;
        border: none;
        outline: none;
        margin-right:5px;
        background-color: white;
        font-size: 17px;
    }
    .delete{
        color:red;
        border-radius: 5px;
        border: none;
        outline: none;
        margin-right:5px;
        background-color: white;
        font-size: 17px;
    }
</style>