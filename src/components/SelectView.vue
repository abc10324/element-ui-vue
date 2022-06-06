<template>
  <div class="fluid-container">
    <div class="d-flex w-100 justify-content-center p-3 mb-4">
      <div class="card">
        <div class="card-header">Select Mode</div>
        <div class="card-body">
          <div class="form-group">
            <label for="categories">Categories</label>
            <div style="width: 500px">
              <el-cascader
                id="categories"
                class="w-100"
                v-model="value.categories"
                :options="categoryOptions"
                :props="{
                  emitPath: false,
                  multiple: true,
                  checkStrictly: true,
                }"
                :placeholder="placeholder"
                clearable
              >
                <template slot-scope="{ node, data }">
                  <span>{{ data.label }}</span>
                  <span v-if="!node.isLeaf"> ({{ data.children.length }}) </span>
                </template>
              </el-cascader>
            </div>
          </div>
          <div class="form-group">
            <label for="main-categories">Main Categories</label>
            <div style="width: 500px">
              <el-cascader
                id="main-categories"
                class="w-100"
                v-model="value.mainCategory"
                :options="mainCategoryOptions"
                :props="{
                  emitPath: false,
                  checkStrictly: true,
                }"
                :placeholder="placeholder"
                clearable
              >
              </el-cascader>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      placeholder: "請選擇",
      categoryOptions: [],
      value: {},
    }
  },
  created(){
    this.categoryOptions = [
      {
        label: "Root",
        value: "root",
        children: [
          {
            label: "Second-1",
            value: "2-1",
            children: [
              {
                label: "Third-1",
                value: "3-1"
              },
              {
                label: "Third-2",
                value: "3-2"
              },
            ]
          },
          {
            label: "Second-2",
            value: "2-2"
          },
        ]
      }
    ]
  },
  methods: {
    getChildrenOptions(option){
      let options = []
      
      if((option.children ?? []).length > 0){
        option.children.forEach(childOption => {
          options.push({
            label: childOption.label,
            value: childOption.value
          })

          if((childOption.children ?? []).length > 0){
            options = options.concat(this.getChildrenOptions(childOption))
          }
        })
      }

      return options
    }
  },
  computed: {
    flatOptions(){
      let options = []

      this.categoryOptions.forEach(option => {
        options = options.concat(this.getChildrenOptions(option))
      })

      return options
    },
    mainCategoryOptions(){
      return this.flatOptions.filter(option => (this.value.categories ?? []).includes(option.value))
    }
  },
  watch: {
    value: {
      handler(newValue){
        console.log(JSON.parse(JSON.stringify(newValue)))
        console.log(JSON.parse(JSON.stringify(this.flatOptions)))
      },
      deep: true
    }
  }
}
</script>

<style>
</style>