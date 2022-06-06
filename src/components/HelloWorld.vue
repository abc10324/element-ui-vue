<template>
  <div class="fluid-container">
    <div class="d-flex w-100 justify-content-center p-3 mb-4">
      <div>
        <button type="button" class="btn btn-info" @click="changeMode('create')">新增</button>
        <button type="button" class="btn btn-success ml-2" @click="changeMode('update')">修改</button>
      </div>
    </div>
    <div class="d-flex w-100 justify-content-center p-3 mb-4">
      <div class="card text-left">
        <div class="card-header">
          {{ this.mode === '' ? '請選擇操作' : this.mode === 'create' ? '新增分類' : '修改分類' }}
        </div>
        <div class="card-body">
          <h5 class="card-title">分類選擇</h5>
          <el-cascader
            v-model="value"
            :options="options"
            :props="{ multiple: false, checkStrictly: true, emitPath: false }"
            clearable
          ></el-cascader>
          <small v-if="this.mode == 'create'" class="form-text text-muted">
            若未選擇欲往下新增的分類，則新增最上層分類</small>


          <h5 class="card-title mt-3">分類名稱</h5>
          <div class="form-group">
<!--            <label for="categoryName">分類名稱</label>-->
            <input type="text" class="form-control"
                   id="categoryName" placeholder="name"
                   v-model="data.name"
            >

            <button class="btn btn-primary mt-3" :disabled="this.mode === '' || this.data.name === ''" @click="save">存檔</button>
          </div>
        </div>
      </div>
    </div>

<!--    <div class="d-flex w-100 justify-content-center p-3 mb-4">-->
<!--      <div class="card">-->
<!--        <div class="card-header">-->
<!--          Ex 2-->
<!--        </div>-->
<!--        <div class="card-body">-->
<!--          <h5 class="card-title">Special title treatment</h5>-->
<!--          <el-cascader-->
<!--            v-model="value1"-->
<!--            :options="options"-->
<!--            :show-all-levels="false"-->
<!--          ></el-cascader>      -->
<!--        </div>-->
<!--      </div>-->
<!--    </div>-->
   
  </div>
</template>

<script>
export default {
  data() {
    return {
      options: [
        {
          value: "guide",
          label: "Guide",
          children: [
            {
              value: "disciplines",
              label: "Disciplines",
              children: [
                {
                  value: "consistency",
                  label: "Consistency",
                },
                {
                  value: "feedback",
                  label: "Feedback",
                },
                {
                  value: "efficiency",
                  label: "Efficiency",
                },
                {
                  value: "controllability",
                  label: "Controllability",
                },
              ],
            },
            {
              value: "navigation",
              label: "Navigation",
              children: [
                {
                  value: "side nav",
                  label: "Side Navigation",
                },
                {
                  value: "top nav",
                  label: "Top Navigation",
                },
              ],
            },
          ],
        },
        {
          value: "component",
          label: "Component",
          children: [
            {
              value: "basic",
              label: "Basic",
              children: [
                {
                  value: "layout",
                  label: "Layout",
                },
                {
                  value: "color",
                  label: "Color",
                },
                {
                  value: "typography",
                  label: "Typography",
                },
                {
                  value: "icon",
                  label: "Icon",
                },
                {
                  value: "button",
                  label: "Button",
                },
              ],
            },
            {
              value: "form",
              label: "Form",
              children: [
                {
                  value: "radio",
                  label: "Radio",
                },
                {
                  value: "checkbox",
                  label: "Checkbox",
                },
                {
                  value: "input",
                  label: "Input",
                },
                {
                  value: "input-number",
                  label: "InputNumber",
                },
                {
                  value: "select",
                  label: "Select",
                },
                {
                  value: "cascader",
                  label: "Cascader",
                },
                {
                  value: "switch",
                  label: "Switch",
                },
                {
                  value: "slider",
                  label: "Slider",
                },
                {
                  value: "time-picker",
                  label: "TimePicker",
                },
                {
                  value: "date-picker",
                  label: "DatePicker",
                },
                {
                  value: "datetime-picker",
                  label: "DateTimePicker",
                },
                {
                  value: "upload",
                  label: "Upload",
                },
                {
                  value: "rate",
                  label: "Rate",
                },
                {
                  value: "form",
                  label: "Form",
                },
              ],
            },
            {
              value: "data",
              label: "Data",
              children: [
                {
                  value: "table",
                  label: "Table",
                },
                {
                  value: "tag",
                  label: "Tag",
                },
                {
                  value: "progress",
                  label: "Progress",
                },
                {
                  value: "tree",
                  label: "Tree",
                },
                {
                  value: "pagination",
                  label: "Pagination",
                },
                {
                  value: "badge",
                  label: "Badge",
                },
              ],
            },
            {
              value: "notice",
              label: "Notice",
              children: [
                {
                  value: "alert",
                  label: "Alert",
                },
                {
                  value: "loading",
                  label: "Loading",
                },
                {
                  value: "message",
                  label: "Message",
                },
                {
                  value: "message-box",
                  label: "MessageBox",
                },
                {
                  value: "notification",
                  label: "Notification",
                },
              ],
            },
            {
              value: "navigation",
              label: "Navigation",
              children: [
                {
                  value: "menu",
                  label: "NavMenu",
                },
                {
                  value: "tabs",
                  label: "Tabs",
                },
                {
                  value: "breadcrumb",
                  label: "Breadcrumb",
                },
                {
                  value: "dropdown",
                  label: "Dropdown",
                },
                {
                  value: "steps",
                  label: "Steps",
                },
              ],
            },
            {
              value: "others",
              label: "Others",
              children: [
                {
                  value: "dialog",
                  label: "Dialog",
                },
                {
                  value: "tooltip",
                  label: "Tooltip",
                },
                {
                  value: "popover",
                  label: "Popover",
                },
                {
                  value: "card",
                  label: "Card",
                },
                {
                  value: "carousel",
                  label: "Carousel",
                },
                {
                  value: "collapse",
                  label: "Collapse",
                },
              ],
            },
          ],
        },
        {
          value: "resource",
          label: "Resource",
          children: [
            {
              value: "axure",
              label: "Axure Components",
            },
            {
              value: "sketch",
              label: "Sketch Templates",
            },
            {
              value: "docs",
              label: "Design Documentation",
            },
          ],
        },
      ],
      value: [],
      value1: null,
      mode:"",
      data:{
        parent: null,
        name: ""
      }
    };
  },
  watch: {
    value: {
      handler(newValue){
        console.log(JSON.parse(JSON.stringify(newValue)))
      },
      deep: true
    },
    value1: {
      handler(newValue){
        console.log(JSON.parse(JSON.stringify(newValue)))
      },
      deep: true
    },
  },
  methods:{
    changeMode(mode){
      this.mode = mode
    },
    save(){
      switch (this.mode){
        case "create":
          if(this.value.length != 0){
            this.data.parent = this.value[0]
          }
          fetch(`/api/clam/category`, {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify(this.data)
          }).then(res => {
            if (res.ok) {
              window.location.reload()
            }else {
              alert("新增失敗")
            }
          })
          break;
        case "update":
          fetch(`/api/clam/category`, {
            method: 'PUT',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify(this.data)
          }).then(res => {
            if (res.ok) {
              window.location.reload()
            }else {
              alert("修改失敗")
            }
          })
          break;
      }



    },
    createCategory(){
      this.mode = 'create'
    },
    updateCategory(){
      this.mode = 'update'
    }
  }
};
</script>

<style scoped>
</style>
