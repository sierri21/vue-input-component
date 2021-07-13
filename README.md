# vue-input-component

Simple input component with validation messages, used in vuelidate
just insert it into your project and fill validations in parent component

you can add v-model, like in usual input HTML tag 

props: 
    - entity: parent Object with fields (type: String, required)
    - field: key in Object (type: String, required)
    - disabled (type: boolean, default: false)
    - label (type: string)  
    - placeholder (type: string)
    - type (type: string, default: 'text')