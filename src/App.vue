<template>
  <div id="app">
    <div class="drop">
    <div 
      class='drop__drop-zone'
      @drop='onDrop($event, 1)' 
      @dragover.prevent
      @dragenter.prevent
    >
    <button class="drop__btn" @click="addOne">+</button>
      <div 
        class='drop__drag-el' 
        v-for='item in listOne' 
        :key='item.title' 
        draggable
        @dragstart='startDrag($event, item)'
   
      
      >
        {{ item.title }}
      </div>
    </div>
    <div
      class='drop__drop-zone'
      @drop='onDrop($event, 2)' 
      @dragover.prevent
      @dragenter.prevent
    >
    <button class="drop__btn" @click="addTwo">+</button>
      <div 
        class='drop__drag-el' 
        v-for='item in listTwo' 
        :key='item.title' 
        draggable
        @dragstart='startDrag($event, item)'
      >
        {{ item.title }}
      </div>
    </div>
    <div
      class='drop__drop-zone'
      @drop='onDrop($event, 3)' 
      @dragover.prevent
      @dragenter.prevent
    >
    <button class="drop__btn" @click="addThree">+</button>
      <div 
        class='drop__drag-el' 
        v-for='item in listThree' 
        :key='item.title' 
        draggable
        @dragstart='startDrag($event, item)'
      >
        {{ item.title }}
      </div>
    </div>
  </div>
  </div>
</template>

<script>

let id=6;
export default {
  name: 'App',
   data () {
    return {
      items: [
      {
        id: 0,
        title: 'Item 1',
        list: 1
      },
      {
        id: 1,
        title: 'Item 2',
        list: 3
      },
      {
        id: 2,
        title: 'Item 3',
        list: 2
      },
      {
        id: 3,
        title: 'Item 4',
        list: 2
      },
      {
        id: 4,
        title: 'Item 5',
        list: 3
      }]
    }
},
computed: {
    listOne () {
      return this.items.filter(item => item.list === 1)
    },
    listTwo () {
      return this.items.filter(item => item.list === 2)
    },
    listThree () {
      return this.items.filter(item => item.list === 3)
    },
    
},
methods:{
  startDrag: (evt, item) => {
      evt.dataTransfer.dropEffect = 'move'
      evt.dataTransfer.effectAllowed = 'move'
      evt.dataTransfer.setData('itemID', item.id)
    },
    onDrop(evt, list) {
          const itemID = evt.dataTransfer.getData('itemID')
          const item = this.items.find(item => item.id == itemID)
          item.list = list
    },
    addOne: function() {
      this.items.push({ title: "Item  " + id, id: id++ ,list:1});
    },
    addTwo: function() {
      this.items.push({ title: "Item  " + id, id: id++ ,list:2});
    },
    addThree: function() {
      this.items.push({ title: "Item  " + id, id: id++ ,list:3});
    }

},

}
</script>
<style lang="scss">
 .drop{
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    &__drop-zone {
    width: 200px;
    background-color: #eee;
    margin-bottom: 10px;
    padding: 10px;
  }
  &__drag-el {
    background-color: #fff;
    margin-bottom: 10px;
    padding: 5px;
  }
  &__btn{
    min-width: 80px;
    min-height: 30px;
    padding: 5px;
    margin: 5px;
    background: #fff;
    border: 0.4px solid;
    text-align: center;
    font-size: 26px;
    border-radius: 8px;

  }
  
  }
  


</style>