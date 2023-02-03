<template>
<div>
    <div class="radio-button-group"> Gender: 
       <label :for="option" v-for="option in options" v-bind:key="option.id"> 
            <input 
                type="radio" 
                name="radio-input" 
                :value="option" 
                :id="option" 
                @change="$emit('input', option)" v-model="gender" />
           {{ option }}
        </label> 
      
    </div>
     
</div> 
</template>

<script>
export default {
    data() {
        return {
            gender: this.radiodata
        }
    },
    props: {
        options: {
            required: true,
            type: Array
        },
        radiodata:String
        
    },

    methods: {
        radiomethod() {
            this.$emit('radio-button-event', this.gender);
        }
    }
}
</script>

<style lang="scss" scoped>

</style>
