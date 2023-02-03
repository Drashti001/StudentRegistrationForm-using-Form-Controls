<template>
    <div>
        <div class="form-group">
            <label>Address</label>
            <textarea 
                cols="80" 
                rows="5" 
                placeholder="Current Address" 
                value="address" 
                required  
                v-model="address"
                @input="textarea">
          </textarea>
        </div><br>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                address:this.textareadata,
            }
            
        },
        props:{
            textareadata: String
        },
        methods: {
            textarea(){
                this.$emit('textarea-event',this.address);
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>