<template>
  <div>
    <ul>
      <li v-if="demo === '1'" @click="handleClick(1)">
        <yn-button type="primary">简单用法（单选）</yn-button>
      </li>
      <li v-if="demo === '2'" @click="handleClick(2)">
        <yn-button type="primary">简单用法（多选）</yn-button>
      </li>
      <li v-if="demo === '3'" @click="handleClick(4)">
        <yn-button type="primary">简单用法(可以不需要异步操作)</yn-button>
      </li>
      <li v-if="demo === '4'" @click="handleClick(3)">
        <yn-button type="primary">高级用法（多步骤）</yn-button>
      </li>
      <li v-if="demo === '5'" @click="handleClick(5)">
        <yn-button type="primary">高级用法实际案例（多步骤）</yn-button>
      </li>
      <li v-if="demo === '6'" @click="handleClick(6)">
        <yn-button type="primary">动态数据案例（多步骤）</yn-button>
      </li>
    </ul>
    <yn-picky-stepper
      v-model="picker1"
      :submit="submit"
      :steps="steps1"
    ></yn-picky-stepper>
    <yn-picky-stepper
      v-model="picker2"
      :submit="submit"
      :steps="steps2"
    ></yn-picky-stepper>
    <yn-picky-stepper
      v-model="picker3"
      :submit="submit"
      :steps="steps3"
    ></yn-picky-stepper>
    <yn-picky-stepper
      v-model="picker4"
      @success="handleSuccess"
      :steps="steps4"
    ></yn-picky-stepper>
    <yn-picky-stepper
      v-model="picker5"
      @success="handleSuccess"
      :steps="steps5"
    ></yn-picky-stepper>
    <yn-picky-stepper
      v-model="picker6"
      @success="handleSuccess"
      :steps="steps6"
    ></yn-picky-stepper>
  </div>
</template>
<script type="text/javascript">
const persons = require("./persons.json");
persons.forEach(p => {
  p.label = p.Name;
});
const reasons = require("./reasons.json");
export default {
  name: "DemoPickyStepper",
  props: {
    demo: String
  },
  methods: {
    handleClick(e) {
      this[`picker${e}`] = !this[`picker${e}`];
    },
    submit(args = {}) {
      console.log("这个是需要提交的参数", args);
      return new Promise((resolve, reject) => {
        console.log(reject);
        setTimeout(() => {
          resolve("ok");
        }, 3000);
      }).catch(err => {
        console.log("错误要在外面执行", err);
      });
    },
    handleSuccess(res) {
      console.log("选择的数据", res);
    }
  },
  data() {
    return {
      picker1: false,
      picker2: false,
      picker3: false,
      picker4: false,
      picker5: false,
      picker6: false,
      steps5: [
        {
          title: "请选择改签人员",
          list: persons,
          multiple: true
        },
        {
          title: "请选择原因",
          list: reasons,
          multiple: false
        }
      ],
      steps6: [],
      steps4: [
        {
          title: "请选择改签人员",
          list: [
            { label: "lizhuang", value: "李壮" },
            { label: "keyanqin", value: "柯艳琴" },
            { label: "xionglonghui", value: "熊龙辉" },
            { label: "liyan", value: "李妍" },
            { label: "wangshengzi", value: "王生资" }
          ],
          multiple: true
        },
        {
          title: "请选择原因",
          list: [
            { label: "行程变化", value: "行程变化" },
            { label: "目的地有住宿", value: "目的地有住宿" },
            { label: "预算超支", value: "预算超支" },
            {
              label: "其他",
              type: "input",
              placeholder: "请输入原因",
              value: ""
            }
          ],
          multiple: false
        }
      ],
      steps3: [
        {
          title: "请选择改签人员",
          list: [
            { label: "lizhuang", value: "李壮" },
            { label: "keyanqin", value: "柯艳琴" },
            { label: "xionglonghui", value: "熊龙辉" },
            { label: "liyan", value: "李妍" },
            { label: "wangshengzi", value: "王生资" }
          ],
          multiple: true
        },
        {
          title: "请选择原因",
          list: [
            { label: "行程变化", value: "行程变化" },
            { label: "目的地有住宿", value: "目的地有住宿" },
            { label: "预算超支", value: "预算超支" },
            {
              label: "其他",
              type: "input",
              placeholder: "请输入原因",
              value: ""
            }
          ],
          multiple: false
        }
      ],
      steps2: [
        {
          title: "请选择改签人员",
          list: [
            { label: "lizhuang", value: "李壮" },
            { label: "keyanqin", value: "柯艳琴" },
            { label: "xionglonghui", value: "熊龙辉" },
            { label: "liyan", value: "李妍" },
            { label: "wangshengzi", value: "王生资" }
          ],
          multiple: true
        }
      ],
      steps1: [
        {
          title: "请选择原因",
          list: [
            { label: "行程变化", value: "行程变化" },
            { label: "目的地有住宿", value: "目的地有住宿" },
            { label: "预算超支", value: "预算超支" },
            {
              label: "其他",
              type: "input",
              placeholder: "请输入原因，不是必填",
              value: "",
              required: false
            },
            {
              label: "还有其他呢",
              type: "textarea",
              placeholder: "请输入原因，默认必填",
              value: "",
              counter: true,
              maxlength: 100,
              // required: true
            }
          ],
          multiple: false
        }
      ]
    };
  },
  mounted() {
    const personStep = {
      title: "请选择改签人员",
      list: persons,
      multiple: true
    };
    const reasonStep = {
      title: "请选择原因",
      list: reasons,
      multiple: false
    };
    this.steps6.push(personStep);
    setTimeout(() => {
      this.steps6.push(reasonStep);
    }, 1000);
    console.log(this.steps6);
  }
};
</script>
<style type="text/css" scoped="scoped">
  ul {list-style: none;padding: 0;}
</style>

