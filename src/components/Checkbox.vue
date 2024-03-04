<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  inputId: String,
  checkboxChecked: Boolean,
  labelString: String,
  onChangeFunc: Function
})
</script>

<template>
  <div class="form-check mb-3">
    <input class="form-check-input" type="checkbox" value="" :id="inputId" :checked="checkboxChecked" @change="onChangeFunc">
    <label class="form-check-label" :for="inputId">
      {{ labelString }}
    </label>
  </div>
</template>
