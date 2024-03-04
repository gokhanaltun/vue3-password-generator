<script setup>
import { defineProps } from "vue";

const props = defineProps({
    cardTitle: String,
    outputString: {type: String, default: "Output"},
    outputClickFunc: Function,
    buttonLabel: String,
    buttonClickFunc: Function
})
</script>

<template>
    <div class="bg-secondary rounded p-4 p-sm-5 my-4 mx-3">
        <div class="d-flex align-items-center justify-content-between mb-3">
            <h3 class="text-primary"><i class="fa fa-key me-2"></i>{{ cardTitle }}</h3>
        </div>
        <div @click="outputClickFunc" class="form-floating mb-3 bg-dark rounded text-center mb-5" style="cursor: pointer">
            <p class="p-3">{{ outputString }}</p>
        </div>
        <slot> </slot>
        <button class="btn btn-primary py-3 w-100 mt-4" @click="buttonClickFunc">{{ buttonLabel }}</button>
    </div>
</template>