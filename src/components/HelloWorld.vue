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
            ref="cascader"
            placeholder="分類"
            v-model="value"
            size="medium"
            :options="options"
            :disabled="mode === ''"
            :props="{ multiple: false, checkStrictly: true, emitPath: false }"
            clearable
          >
          </el-cascader>
          <small v-if="this.mode == 'create'" class="form-text text-muted">
            若未選擇欲往下新增的分類，則新增為最上層分類</small>

          <h5 class="card-title mt-3">分類名稱</h5>
          <div class="form-group">
            <input type="text" class="form-control"
                   id="categoryName" placeholder="name"
                   v-model="data.name"
            >
            <button class="btn btn-primary mt-3" :disabled="this.mode === '' || this.data.name === ''" @click="save">存檔</button>
            <button v-if="this.mode === 'update' && this.value !== null && this.isLeafCategory === true" class="btn btn-primary mt-3 ml-2" @click="deleteCategory">刪除</button>
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
      optionssrc:[
        {
          "value": "626b8bf9200aa64e335860d7",
          "label": "default_grandpa_one",
          "parent": null,
          "children": [
            {
              "value": "626b8c50200aa64e335860e9",
              "label": "default_parent_one",
              "parent": "626b8bf9200aa64e335860d7",
              "children": [
                {
                  "value": "626b8d5d200aa64e3358610c",
                  "label": "default_child_one",
                  "parent": "626b8c50200aa64e335860e9",
                  "children": []
                },
                {
                  "value": "626b8d8d200aa64e33586113",
                  "label": "default_child_one_one",
                  "parent": "626b8c50200aa64e335860e9",
                  "children": []
                },
                {
                  "value": "626b8d92200aa64e33586117",
                  "label": "default_child_one_one_one",
                  "parent": "626b8c50200aa64e335860e9",
                  "children": []
                }
              ]
            },
            {
              "value": "626b8ce7200aa64e33586101",
              "label": "en_parent_four_but_default_grandpa_one",
              "parent": "626b8bf9200aa64e335860d7",
              "children": []
            },
            {
              "value": "62723127e92248356b9523f5",
              "label": "20220504TEST",
              "parent": "626b8bf9200aa64e335860d7",
              "children": []
            }
          ]
        },
        {
          "value": "626b8c07200aa64e335860da",
          "label": "default_grandpa_two",
          "parent": null,
          "children": [
            {
              "value": "626b8c66200aa64e335860ed",
              "label": "default_parent_two",
              "parent": "626b8c07200aa64e335860da",
              "children": []
            }
          ]
        },
        {
          "value": "626b8c0b200aa64e335860dd",
          "label": "default_grandpa_three",
          "parent": null,
          "children": [
            {
              "value": "626b8c6f200aa64e335860f1",
              "label": "default_parent_three",
              "parent": "626b8c0b200aa64e335860dd",
              "children": []
            }
          ]
        },
        {
          "value": "626b8c20200aa64e335860e0",
          "label": "en_grandma_three",
          "parent": null,
          "children": [
            {
              "value": "626b8c8e200aa64e335860f5",
              "label": "en_parent_three",
              "parent": "626b8c20200aa64e335860e0",
              "children": []
            }
          ]
        },
        {
          "value": "626b8c26200aa64e335860e3",
          "label": "en_grandma_two",
          "parent": null,
          "children": [
            {
              "value": "626b8ca6200aa64e335860f9",
              "label": "en_parent_two",
              "parent": "626b8c26200aa64e335860e3",
              "children": []
            }
          ]
        },
        {
          "value": "626b8c29200aa64e335860e6",
          "label": "en_grandma_one",
          "parent": null,
          "children": [
            {
              "value": "626b8caf200aa64e335860fd",
              "label": "en_parent_one",
              "parent": "626b8c29200aa64e335860e6",
              "children": []
            },
            {
              "value": "626b8d1a200aa64e33586105",
              "label": "default_parent_four_but_en_grandma_one",
              "parent": "626b8c29200aa64e335860e6",
              "children": []
            }
          ]
        },
        {
          "value": "62835f673f8d043681652446",
          "label": "20220517TEST",
          "parent": null,
          "children": []
        }
      ],
      // options: [
      //   {
      //     value: "post",
      //     label: "文章",
      //     children: [
      //       {
      //         value: "postOne",
      //         label: "文章分類一",
      //         children: [
      //           {
      //             value: "postOneOfOne",
      //             label: "文章分類一之一",
      //           },
      //           {
      //             value: "postOneOfTwo",
      //             label: "文章分類一之二",
      //           },
      //           {
      //             value: "postOneOfThree",
      //             label: "文章分類一之三",
      //           },
      //           {
      //             value: "postOneOfFour",
      //             label: "文章分類一之四",
      //           },
      //         ],
      //       },
      //       {
      //         value: "postTwo",
      //         label: "文章分類二",
      //         children: [
      //           {
      //             value: "postTwoOfOne",
      //             label: "文章分類二之一",
      //           },
      //           {
      //             value: "postTwoOfTwo",
      //             label: "文章分類二之二",
      //           },
      //         ],
      //       },
      //     ],
      //   },
      //   {
      //     value: "news",
      //     label: "新聞",
      //     children: [
      //       {
      //         value: "newsOne",
      //         label: "新聞分類一",
      //         children: [
      //           {
      //             value: "newsOneOfOne",
      //             label: "新聞分類一之ㄧ",
      //           },
      //           {
      //             value: "newsOneOfTwo",
      //             label: "新聞分類一之二",
      //           },
      //           {
      //             value: "newsOneOfThree",
      //             label: "新聞分類一之三",
      //           },
      //           {
      //             value: "newsOneOfFour",
      //             label: "新聞分類一之四",
      //           },
      //           {
      //             value: "newsOneOfFive",
      //             label: "新聞分類一之五",
      //           },
      //         ],
      //       },
      //       {
      //         value: "newsTwo",
      //         label: "新聞分類二",
      //         children: [
      //           {
      //             value: "newsTwoOfOne",
      //             label: "新聞分類二之一",
      //           },
      //           {
      //             value: "newsTwoOfTwo",
      //             label: "新聞分類二之二",
      //           },
      //           {
      //             value: "newsTwoOfThree",
      //             label: "新聞分類二之三",
      //           },
      //           {
      //             value: "newsTwoOfFour",
      //             label: "新聞分類二之四",
      //           },
      //           {
      //             value: "newsTwoOfFive",
      //             label: "新聞分類二之五",
      //           },
      //           {
      //             value: "newsTwoOfSix",
      //             label: "新聞分類二之六",
      //           },
      //           {
      //             value: "newsTwoOfSeven",
      //             label: "新聞分類二之七",
      //           },
      //           {
      //             value: "newsTwoOfEight",
      //             label: "新聞分類二之八",
      //           },
      //           {
      //             value: "newsTwoOfNine",
      //             label: "新聞分類二之九",
      //           },
      //           {
      //             value: "newsTwoOfTen",
      //             label: "新聞分類二之十",
      //           }
      //         ],
      //       },
      //       {
      //         value: "newsThree",
      //         label: "新聞分類三",
      //         children: [
      //           {
      //             value: "newsThreeOfOne",
      //             label: "新聞分類三之一",
      //           },
      //           {
      //             value: "newsThreeOfTwo",
      //             label: "新聞分類三之二",
      //           },
      //           {
      //             value: "newsThreeOfThree",
      //             label: "新聞分類三之三",
      //           },
      //           {
      //             value: "newsThreeOfFour",
      //             label: "新聞分類三之四",
      //           },
      //           {
      //             value: "newsThreeOfFive",
      //             label: "新聞分類三之五",
      //           },
      //           {
      //             value: "newsThreeOfSix",
      //             label: "新聞分類三之六",
      //           },
      //         ],
      //       },
      //       {
      //         value: "newsFour",
      //         label: "新聞分類四",
      //         children: [
      //           {
      //             value: "alert",
      //             label: "Alert",
      //           },
      //           {
      //             value: "loading",
      //             label: "Loading",
      //           },
      //           {
      //             value: "message",
      //             label: "Message",
      //           },
      //           {
      //             value: "message-box",
      //             label: "MessageBox",
      //           },
      //           {
      //             value: "notification",
      //             label: "Notification",
      //           },
      //         ],
      //       },
      //       {
      //         value: "newsFive",
      //         label: "新聞分類五",
      //         children: [
      //           {
      //             value: "menu",
      //             label: "NavMenu",
      //           },
      //           {
      //             value: "tabs",
      //             label: "Tabs",
      //           },
      //           {
      //             value: "breadcrumb",
      //             label: "Breadcrumb",
      //           },
      //           {
      //             value: "dropdown",
      //             label: "Dropdown",
      //           },
      //           {
      //             value: "steps",
      //             label: "Steps",
      //           },
      //         ],
      //       },
      //       {
      //         value: "newsSix",
      //         label: "新聞分類六",
      //         children: [
      //           {
      //             value: "dialog",
      //             label: "Dialog",
      //           },
      //           {
      //             value: "tooltip",
      //             label: "Tooltip",
      //           },
      //           {
      //             value: "popover",
      //             label: "Popover",
      //           },
      //           {
      //             value: "card",
      //             label: "Card",
      //           },
      //           {
      //             value: "carousel",
      //             label: "Carousel",
      //           },
      //           {
      //             value: "collapse",
      //             label: "Collapse",
      //           },
      //         ],
      //       },
      //     ],
      //   },
      //   {
      //     value: "item",
      //     label: "商品",
      //     children: [
      //       {
      //         value: "itemOne",
      //         label: "商品分類一",
      //       },
      //       {
      //         value: "itemTwo",
      //         label: "商品分類二",
      //       },
      //       {
      //         value: "itemThree",
      //         label: "商品分類三",
      //       },
      //     ],
      //   },
      // ],
      value: null,
      value1: null,
      mode:"",
      data:{
        categoryId: null,
        parent: null,
        name: ""
      },
      isLeafCategory: false
    };
  },
  computed: {
    options(){
      this.filterOptions(this.optionssrc)
      return this.optionssrc
    }
  },
  watch: {
    value: {
      handler(newValue){
        if(this.mode === 'create'){
          if(newValue !== null){
            this.data.parent = newValue
          }
        }else if(this.mode === 'update'){
          let node = this.$refs["cascader"].getCheckedNodes()[0]
          this.isLeafCategory = !node.hasChildren
          this.data.name = node.label
          this.data.categoryId = newValue
          this.data.parent = null
          if(node.parent != null){
            this.data.parent = node.parent.data.value
          }
        }
        console.log("newValue=", JSON.parse(JSON.stringify(newValue)))
        console.log(" this.data=",  this.data)
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
    filterOptions(list){
      list.forEach((option) =>{
        if(option.children.length === 0){
          delete option.children
        }else {
          this.filterOptions(option.children)
        }
      })
    },
    changeMode(mode){
      this.mode = mode
    },
    save(){
      let data = {}
      if(this.mode === 'create'){
        data.method = 'POST'
        data.errmsg = '新增失敗'
      }else if(this.mode === 'update'){
        data.method = 'PUT'
        data.errmsg = '修改失敗'
      }

      if(this.value !== null){
        this.data.parent = this.value
      }

      console.log("save this.data=", JSON.stringify(this.data))
      // fetch(`/api/clam/category`, {
      //   method: data.method,
      //   headers: {'Content-Type': 'application/json'},
      //   body: JSON.stringify(this.data)
      // }).then(res => {
      //   if (res.ok) {
      //     window.location.reload()
      //   }else {
      //     alert(data.errmsg)
      //   }
      // })
    },
    deleteCategory(){
      console.log("deleteCategory this.data=", JSON.stringify(this.data))

      // fetch(`/api/clam/category?categoryId=${this.data.categoryId}`, {
      //         method: 'DELETE',
      // }).then(res => {
      //   if (res.ok) {
      //     window.location.reload()
      //   }else {
      //     alert('刪除失敗')
      //   }
      // })
    }
  }
};
</script>

<style scoped>
</style>
