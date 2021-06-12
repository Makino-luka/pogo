<template>
  <div class="validate-input-container pb-3">
    <input type="text"
    class="form-control"
    :class="{'is-invalid': inputRef.error}"
    :value="inputRef.val"
    @blur="validateInput"
    @input="updateValue"
    v-bind="$attrs"
    >
    <span v-if="inputRef.error" class="invalid-feedback">{{inputRef.message}}</span>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, PropType } from 'vue'
const emailReg = /^[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/
interface rangeRule {
  length: number
}
interface RuleProp {
  type: 'required' | 'email' | 'range';
  message: string
  min?: rangeRule
  max?: rangeRule
}
export type RulesProp = RuleProp[]
export default defineComponent({
  props: {
    rules: Array as PropType<RulesProp>,
    modelValue: String,
    maxlength: String
  },
  inheritAttrs: false,
  setup (props, context) {
    console.log(context.attrs)
    const inputRef = reactive({
      val: props.modelValue || '',
      error: false,
      message: ''
    })
    const updateValue = (e: KeyboardEvent) => {
      const targetValue = (e.target as HTMLInputElement).value
      inputRef.val = targetValue
      context.emit('update:modelValue', targetValue)
    }
    const validateInput = () => {
      if (props.rules) {
        const allPassed = props.rules.every(rule => {
          let passed = true
          inputRef.message = rule.message
          switch (rule.type) {
            case 'required':
              passed = (inputRef.val.trim() !== '')
              break
            case 'email':
              passed = emailReg.test(inputRef.val)
              break
            case 'range':
              if (rule.min && !rule.max) {
                passed = (rule.min.length <= inputRef.val.length)
              } else if (rule.max && !rule.min) {
                passed = (inputRef.val.length <= rule.max.length)
              } else if (rule.min && rule.max) {
                passed = (rule.min.length <= inputRef.val.length && inputRef.val.length <= rule.max.length)
              } else {
                passed = false
              }
              break
            default: break
          }
          return passed
        })
        inputRef.error = !allPassed
      }
    }
    return {
      inputRef,
      validateInput,
      updateValue
    }
  }
})
</script>

<style>

</style>
