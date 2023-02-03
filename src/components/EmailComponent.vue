<template>
    <div>
        <div class="form-group">
            <label>E-mail</label>
            <input 
                type="email" 
                placeholder="Enter Email" 
                name="email" 
                required v-model="email"
                @input="emaildata">
        </div><br>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                email:this.emailprops,
            }
        },
        props:{
            emailprops: String
        },
        methods:{
            emaildata(){
                this.$emit('email-event',this.email);
            }
        }

    }
</script>

<style lang="scss" scoped>

</style>