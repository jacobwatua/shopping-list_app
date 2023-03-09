<template>
  <div id="alert">
    <p>Item name cannot be blank</p>
  </div>
  <p class="text-center count">No items on the list</p>
  <h1 class="text-sm-center"><span>Shopping</span><span> List</span></h1>
  <div class="cart">
    <div class="input" name="added_item">
      <div><input type="text" name="item" id="" class="form-control" placeholder="Enter item name" v-model="item" @keyup.enter="update_items(item)"></div>
      <div><button class="btn btn-success btn-sm" @click="update_items(item)">Add item</button></div>
    </div>
    <div class="items" id="items">
      <div class="item" v-for="(item, n) in items" :key="`item${n}`" style="margin: 10px;">
        <div>{{ item }}</div>
        <button class="btn btn-danger btn-sm" @click="remove_item(item)">Remove</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data (){
    return{
      item : "",
      items : [],
    }
  },

  mounted (){
    document.getElementById("items").style.display = "none";
    document.querySelector(".count").textContent = "Shopping list is empty";
  },

  updated (){
    if (this.items.length < 1){
      document.getElementById("items").style.display = "none";
      document.querySelector(".count").textContent = "Shopping list is empty";
    }
    else{
      if (this.items.length == 1) {
        document.getElementById("items").style = null;
        document.querySelector(".count").textContent = `Your list has ${this.get_count()} item`;
      }
      else{
        document.getElementById("items").style = null;
        document.querySelector(".count").textContent = `Your list has ${this.get_count()} items`;
      }
    }
  },

  methods : {
    update_items (item) {
      if (item != ""){
        this.items.push(item);
        return this.items;
      }
      else{
        document.getElementById("alert").style.display = "block";
        setTimeout(()=>{
          document.getElementById("alert").style = null;
        }, 3000);
      }
    },

    remove_item(item){
      this.items.pop(this.items.indexOf(item));
      return this.items;
    },

    get_count() {
      return this.items.length;
    },

    empty_input (){
      this.item = "";
      return this.item;
    }
  }
}
</script>

<style>
.cart {
  width: 50vw;
  top: 0px;
  margin-left: auto;
  margin-right: auto;
  display: grid;
  grid-template-rows: 100px 1fr;
  padding: 10px;
}

.items {
  padding: 10px;
  border: 1px rgba(0, 0, 0, 0.2) solid;
}

.input,
.items .item{
  display: grid;
  grid-auto-columns: 85% 1fr;
  grid-template-areas:
  "input button ";
  grid-gap: 7px;
  justify-content: center;
}
.item {
  padding: 5px;
}
</style>