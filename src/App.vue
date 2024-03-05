<script setup>
import { onMounted, reactive } from "vue";
import Card from "./components/Card.vue"
import Checkbox from "./components/Checkbox.vue";
import { shuffleString } from "./utils";

const state = reactive({
  output: "click to copy",
})

const dataSet = {
  upper: {
    value: "ABCDEFGHIJKLMNOPRSTUVYZWQX",
    default: true,
    description: "Include Uppercase"
  },
  lower: {
    value: "abcdefghijklmnoprstuvyzwqx",
    default: true,
    description: "Include Lowercase"
  },
  number: {
    value: "0123456789",
    default: true,
    description: "Include Numbers"
  },
  char: {
    value: "./*-_?!",
    default: false,
    description: "Include Special Chars"
  }
}


let selectedDatas = {}

onMounted(() => {
  let keys = Object.keys(dataSet)
  for (let i = 0; i < keys.length; i++) {
    if (dataSet[keys[i]].default) {
      selectedDatas[keys[i]] = dataSet[keys[i]].value
    }
  }

  console.log(selectedDatas)
})

const generateButtonClick = (e) => {
  if (Object.keys(selectedDatas).length < 1){
    alert("You must select at least one option.")
    return
  }

  let allSelectedValues = Object.values(selectedDatas).map(value => value).join("")
  allSelectedValues = shuffleString(allSelectedValues)

  let out = ""
  for (let i = 0; i < 16; i++) {
    out += allSelectedValues[Math.floor(Math.random() * allSelectedValues.length)]
  }

  state.output = out
  console.log(allSelectedValues)
}

const handleOnChange = (e) => {
  const { id, checked } = e.target
  if (checked) {
    selectedDatas[id] = dataSet[id].value
  } else {
    delete selectedDatas[id]
  }
  console.log(selectedDatas)
}

const copyOutput = () => {
  navigator.clipboard.writeText(state.output)
    .then(() => {
      console.log("copy success");
      alert("copy success")
    })
    .catch(err => {
      console.error("copy error: ", err);
    });
}
</script>

<template>
  <Card cardTitle="Password Generator" :outputString="state.output" buttonLabel="Generate"
    :buttonClickFunc="generateButtonClick" :output-click-func="copyOutput">
    <Checkbox v-for="([key, item]) in Object.entries(dataSet)" :key="key" :input-id="key"
      :label-string="item.description" :checkbox-checked="item.default" :on-change-func="handleOnChange" />
  </Card>
</template>
