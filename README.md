# vue-input-component

Simple input component with validation messages, used in vuelidate
just insert it into your project and fill validations in parent component

you can add v-model, like in usual input HTML tag 

props: 
* entity: parent Object with fields (type: String, required)
*0 field: key in Object (type: String, required)
*0 disabled (type: boolean, default: false)
*0 label (type: string)  
*0 placeholder (type: string)
*0 type (type: string, default: 'text')