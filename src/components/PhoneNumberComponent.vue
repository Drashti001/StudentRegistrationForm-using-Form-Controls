<template>
    <div>
        <div class="form-group">
            <label>Phone No.</label>
           
            <input 
                type="text" 
                pattern="[789][0-9]{9}"
                name="phone" 
                placeholder="phone no." 
                max="10"
                required  
                v-model="phone"
                @input="phonenumber">
        </div><br>
    </div>
</template>

<script>
    export default {
        props:{
            phonenumberdata:String
        },
        data(){
            return{
                phone:this.phonenumberdata,
            }
        },
        methods:{
            phonenumber(){
                this.$emit('phone-number-event',this.phone);
            }
        }
        
    }
</script>

<style lang="scss" scoped>

</style>