<template>
    <div>
        

        <div class="form-group">
            <label for="title">Enter Student Course</label>
            <select 
                v-model="course"
                class="form-select"
                @change="selectchange"
                >

                <option selected>Course</option>
                <option v-for="selectdata in selectallcourse" :key="selectdata">
                    {{ selectdata }}
                  </option>
            </select>
        </div><br>
    </div>
</template>

<script>
    export default {
        data(){
         return{
            course:this.selectprop,
         }
        },
        props: {
         selectallcourse: Array,
        
         selectprop : String,
         },
        methods:{
            selectchange() {
            this.$emit("select-event", this.course);
    },
        }
    }
</script>

<style lang="scss" scoped>

</style>