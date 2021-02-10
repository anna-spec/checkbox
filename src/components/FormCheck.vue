<template>
  <div class="form">
    <form>
      <h2>Выбрать категорю</h2>

<!--      <div :key="data.parentItem.id"-->
<!--           class="parent-cont"-->
<!--           v-for="data of checkboxData" >-->
<!--        <checkbox-->
<!--            :checkbox_type="'parent'"-->
<!--            :label="data.parentItem.label"></checkbox>-->

<!--        <br>-->

<!--        <div class="children" :key="child" v-for="child of data.parentItem.childItem">-->
<!--           <checkbox-->
<!--              :label="child"-->
<!--              :parent_label="data.parentItem.label"-->
<!--              :checkbox_type="'child'"></checkbox>-->
<!--        </div>-->

<!--      </div>-->

      <div :key="data.parentItem.id" v-for="data of checkboxData"  class="parent-cont">
        <ChecksCont :data="data" ></ChecksCont>
      </div>

      <div class="d-flex mt-4 justify-content-end"> <button class="btn btn-primary">Сохранить</button></div>

    </form>
  </div>
</template>

<script>
  export default {
    name  : "FormCheck",
    props : ["checkboxData"],
    data() {
      return {
        allToSaveData : []
      }

    }
  }
</script>

<style scoped>
  .form {
    width: max-content;
    margin: auto;
    position: relative;
    top:100px;
    padding:30px;
    background:white;
    border-radius:10px;
  }

  h2 {
    font-weight:100;
    margin-bottom:20px;
  }

  .parent-cont {
    display: inline-block;
    margin-right:70px;
  }

  .children {
    margin-left:20px;
  }
</style>