<template>
  <div class="label-cont">
    <label>
      <input v-model="isChecked"  type="checkbox"  :name="parent_label" :value="child_label" />
      <span>{{ child_label }}</span>
    </label>
  </div>
</template>

<script>
export default {
  name  : "CheckboxChild",
  props : {
    checkbox_type : {
      type: String,
    },

    parent_id : {
      type: Number
    },

    parent_label : {
      type: String
    },

    child_label: {
      type: String
    },

    allChecked: {
      type: Boolean
    }
  },

  data() {
    return{
      isChecked : false,
      childCheckedData : {}
    }
  },

  created() {
   this.isChecked = this.allChecked
  },

  updated(){
    this.childCheckedData.isChildChecked  = this.isChecked;
    this.childCheckedData.childValue      = this.child_label;
    this.childCheckedData.parentId        = this.parent_id;
    this.$emit('childChecked',  this.childCheckedData)
  },

  watch : {
    'allChecked'(newVal){
      this.isChecked = newVal
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