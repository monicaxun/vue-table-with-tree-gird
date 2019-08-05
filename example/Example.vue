<template lang="html">
  <div id="example">
    <ul class="switch-list">
      <li class="switch-item" v-for="item in propList">
        <span>{{ item.name }}: </span>
        <zk-switch v-model="props[item.name]"></zk-switch>
      </li>
    </ul>
    <zk-table
      ref="table"
      sum-text="sum"
      index-text="#"
      :data="data"
      :columns="columns"
      :stripe="props.stripe"
      :border="props.border"
      :show-header="props.showHeader"
      :show-summary="props.showSummary"
      :show-row-hover="props.showRowHover"
      :show-index="props.showIndex"
      :tree-type="props.treeType"
      :is-fold="props.isFold"
      :disable-checkbox-by="disableCheckboxBy"
      @checkbox-click="checkboxClick"
      @toggle-all-checked="toggleChecked"
      :expand-type="props.expandType"
      :selection-type="props.selectionType">
      <template slot="$expand" slot-scope="scope">
        {{ `My name is ${scope.row.name},
           this rowIndex is ${scope.rowIndex}.`
         }}
      </template>
      <template slot="likes" slot-scope="scope">{{ scope.row.likes.join(',') }}</template>
    </zk-table>
  </div>
</template>

<script>
import ZkSwitch from "./Switch/Switch";

export default {
  name: "example",
  components: {
    ZkSwitch
  },
  data() {
    return {
      props: {
        stripe: false,
        border: false,
        showHeader: true,
        showSummary: false,
        showRowHover: true,
        showIndex: false,
        treeType: true,
        isFold: true,
        expandType: false,
        selectionType: true,
      },
      disableCheckboxBy: (row) => {
        return row.score <= 10;
      },
        data: [
        {
          name: "Jack",
          sex: "male",
          likes: ["football", "basketball"],
          score: 10,
          isRedudent: 1,
          children: [
            {
              name: "Ashley",
              sex: "female",
              likes: ["football", "basketball"],
              score: 20,
              isRedudent: 0,
              children: [
                {
                  name: "Ashley",
                  sex: "female",
                  likes: ["football", "basketball"],
                  score: 20,
                  isRedudent: 0,
                },
                {
                  name: "Taki",
                  sex: "male",
                  likes: ["football", "basketball"],
                  score: 10,
                  isRedudent: 1,
                  children: [
                    {
                      name: "Ashley",
                      sex: "female",
                      likes: ["football", "basketball"],
                      score: 20,
                      isRedudent: 0,
                    },
                    {
                      name: "Taki",
                      sex: "male",
                      likes: ["football", "basketball"],
                      score: 10,
                      isRedudent: 1,
                      children: [
                        {
                          name: "Ashley",
                          sex: "female",
                          likes: ["football", "basketball"],
                          score: 20,
                          isRedudent: 0,
                        },
                        {
                          name: "Taki",
                          sex: "male",
                          likes: ["football", "basketball"],
                          score: 10,
                          isRedudent: 1,
                        }
                      ]
                    }
                  ]
                }
              ]
            },
            {
              name: "Taki",
              sex: "male",
              likes: ["football", "basketball"],
              score: 10,
              isRedudent: 1,}
          ]
        },
        {
          name: "Tom",
          sex: "male",
          likes: ["football", "basketball"],
          score: 10,
          isRedudent: 1,
          children: [
            {
              name: "Ashley",
              sex: "female",
              likes: ["football", "basketball"],
              score: 20,
              isRedudent: 0,
              children: [
                {
                  name: "Ashley",
                  sex: "female",
                  likes: ["football", "basketball"],
                  score: 20,
                  isRedudent: 0,
                },
                {
                  name: "Taki",
                  sex: "male",
                  likes: ["football", "basketball"],
                  score: 10,
                  isRedudent: 1,
                }
              ]
            },
            {
              name: "Taki",
              sex: "male",
              likes: ["football", "basketball"],
              score: 10,
              isRedudent: 1,
              children: [
                {
                  name: "Ashley",
                  sex: "female",
                  likes: ["football", "basketball"],
                  score: 20,
                  isRedudent: 0,
                },
                {
                  name: "Taki",
                  sex: "male",
                  likes: ["football", "basketball"],
                  score: 10,
                  isRedudent: 1,
                }
              ]
            }
          ]
        },
        {
          name: "Tom",
          sex: "male",
          likes: ["football", "basketball"],
          score: 20
        },
        {
          name: "Tom",
          sex: "male",
          likes: ["football", "basketball"],
          score: 20,
          children: [
            {
              name: "Ashley",
              sex: "female",
              likes: ["football", "basketball"],
              score: 20
            },
            {
              name: "Taki",
              sex: "male",
              likes: ["football", "basketball"],
              score: 10
            }
          ]
        }
      ],
      columns: [
        {
          label: "",
          type: "checkbox",
          disable: 'score'
        },
        {
          label: "name",
          prop: "name",
          width: "400px"
        },
        {
          label: "sex",
          prop: "sex",
          minWidth: "50px"
        },
        {
          label: "score",
          prop: "score"
        },
        {
          label: "likes",
          prop: "likes",
          minWidth: "200px",
          type: "template",
          template: "likes"
        }
      ]
    };
  },
  computed: {
    propList() {
      return Object.keys(this.props).map(item => ({
        name: item
      }));
    }
  },
  methods: {
    toggleChecked(e) {
      // eslint-disable-next-line
      console.log("E", e);
      const ss = this.$refs.table.getCheckedProp("name");
      // eslint-disable-next-line
      console.log("checked id", ss);
      // return ss;
    },
    checkboxClick(row, rowIndex, $event) {
      // eslint-disable-next-line
      debugger;
      // eslint-disable-next-line
      console.log("checkboxClick", row, rowIndex, $event);
    },
  }
};
</script>

<style scoped lang="less">
* {
  margin: 0;
  padding: 0;
}

.switch-list {
  margin: 20px 0;
  list-style: none;
  overflow: hidden;
}

.switch-item {
  margin: 20px;
  float: left;
}
</style>
