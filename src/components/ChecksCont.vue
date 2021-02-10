<template>
  <div>
    <checkbox-parent
        :checkbox_type="'parent'"
        :parent_data="data.parentItem"
        :isCheckedChild.sync="isCheckedChild"
        @allChecked="allCheckedDataEvent"
        ></checkbox-parent>
    <span> (выбрано {{ childCheckedData.length }} из {{  data.parentItem.childItem.length }})</span>
    <br>

    <div class="children" :key="child" v-for="child of data.parentItem.childItem">
      <checkbox-child
          :child_label="child"
          :checkbox_type="'child'"
          :parent_id="data.parentItem.id"
          :parent_label="data.parentItem.label"
          :allChecked.sync="allChecked"
          @childChecked="childCheckedDataEvent"
    ></checkbox-child>
    </div>

  </div>

</template>

<script>
export default {
  name: "ChecksCont",
  props:["data"],
  data() {
    return {
      allChecked        : false,
      childChecked      : false,
      allCheckedData    : {},
      childCheckedData  : [],
      allCheckedDatas   : [],
      isCheckedChild    : false
    }
  },

  methods: {
    allCheckedDataEvent(target) {
      this.allChecked = target.allChecked;
      this.childCheckedData = []
    },

    childCheckedDataEvent(target) {
      if(target.isChildChecked == true) {
        this.childCheckedData.push(target)
        console.log(this.childCheckedData)

        // for(let i = 0; i < this.childCheckedData.length; i++) {
        //   this.allCheckedDatas.push({
        //     parentId    : this.childCheckedData[i].parentIt,
        //     childValue  : this.childCheckedData[i].childValue,
        //   })
        // }

      }else {
        console.log(this.childCheckedData)

        this.childCheckedData.pop()
      }


    }
  },

  created() {
    this.allCheckedData.allChecked = false
  },

  watch : {
    'childCheckedData'(newVal){
      if( newVal.length > 0) {
        this.isCheckedChild = true;
      }else {
        this.isCheckedChild = false;
      }

    }
  }

}
</script>

<style scoped>
  .children {
    margin-left:20px;
  }
</style>