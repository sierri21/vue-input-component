<template>
    <div>
        <label :for="entity + field + 'input'" v-if="label">
          {{ label }}
        </label>
        <input
            :id="entity + field + 'input'"
            :type="type"
            :value="value"
            :disabled="disabled"
            :placeholder="placeholder"
            @input="updateValue">
          <template v-if="validations.includes('required')">
            <div v-if="!this.$parent.$v[entity][field].required">
                Это поле обязательно к заполнению
            </div>
          </template>
          <template v-if="validations.includes('maxLength')">
            <div v-if="!this.$parent.$v[entity][field].maxLength">
                  Максимальная длина поля
                  {{this.$parent.$v[entity][field].$params.maxLength.max}}
                  символов
            </div>
          </template>
          <template v-if="validations.includes('minLength')">
            <div v-if="!this.$parent.$v[entity][field].minLength">
              Минимальная длина поля
              {{this.$parent.$v[entity][field].$params.minLength.min}}
              символов
            </div>
          </template>
          <template v-if="validations.includes('numeric')">
            <div v-if="!this.$parent.$v[entity][field].numeric">
              Введенное значение должно быть числом
            </div>
          </template>
          <template v-if="validations.includes('maxValue')
                    && this.$parent.$v[entity][field].numeric">
            <div v-if="!this.$parent.$v[entity][field].maxValue">
              Это значение должно быть меньше
              {{this.$parent.$v[entity][field].$params.maxValue.max}}
            </div>
          </template>
          <template v-if="validations.includes('minValue')
                    && this.$parent.$v[entity][field].numeric">
            <div v-if="!this.$parent.$v[entity][field].minValue">
              Это значение должно быть больше
              {{this.$parent.$v[entity][field].$params.minValue.min}}
            </div>
          </template>
        <slot>
        </slot>
        <div>
        </div>
    </div>
</template>

<script>
export default ({
  name: 'text-input',
  props: {
    value: { type: String },
    entity: {},
    field: {},
    disabled: {
      type: Boolean,
      default: false
    },
    label: {
      type: String,
      default: ''
    },
    placeholder: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'text'
    }
  },
  methods: {
    updateValue (e) {
      this.$emit('input', e.target.value)
      // eslint-disable-next-line no-unused-expressions
      this.$parent.$v[this.entity][this.field].$touch
    }
  },
  computed: {
    validations () {
      return Object.keys(this.$parent.$v[this.entity][this.field])
    }
  }
})
</script>
