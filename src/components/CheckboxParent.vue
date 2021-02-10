<template>
  <div class="label-cont">
    <label>
     <input :class="{ 'checked': isChecked_Child }" type="checkbox" :name="parent_value" v-model="isChecked" :value="parent_value" />

      <span>{{ parent_value }}</span>
    </label>
  </div>
</template>

<script>
  export default {
    name  : "CheckboxParent",
    props : ["parent_data", "checkbox_type", "isCheckedChild"],
    data() {
      return{
        parent_value     : "",
        parent_id        : "",
        isChecked        : false,
        allChecked       : false,
        allCheckedData   : {},
        isChecked_Child  : false

      }
    },

    mounted() {
      this.parent_value = this.parent_data.label;
      this.parent_id    = this.parent_data.id;
    },

    updated(){
        this.allCheckedData.allChecked  = this.isChecked;
        this.allCheckedData.parentValue = this.parent_value;
        this.allCheckedData.parentId    = this.parent_id;
        this.$emit('allChecked', this.allCheckedData)

    },

    watch : {
      'isCheckedChild'(newVal){
        this.isChecked_Child = newVal
      }
    }

  }
</script>

<style scoped>
  span {
    margin-left:10px;
  }

  label {
    display: inline-flex;
    align-items: center;
    width: max-content;
  }

  .label-cont {
    display: inline-block;
  }
</style>