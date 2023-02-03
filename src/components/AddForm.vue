<template>
<div class="container">
    <div class="modal-dialog modal-dialog-centered modal-dialog-scrollable">
        <div class="modal-content">
            <div class="modal-header">
                <h5>Add Data</h5>
            </div>
            <div class="modal-body">
                <text-component 
                    @text-event-first="firstnamevalue($event)"
                    @text-event-last="lastnamevalue($event)">
                </text-component>

                <select-component 
                    
                    v-bind:selectallcourse="selectcourse" 
                    @select-event="selectvalue($event)">
                </select-component>

                <radio-button-component 
                    
                    v-model="gender" 
                    :options="options"
                    @radio-button-event="radiobuttonvalue($event)">
                </radio-button-component>

                <check-box-component 
                   
                    v-model="hobbies" 
                    @checkbox-event="checkboxvalue($event)">
                </check-box-component>

                <phone-number-component 
                   
                    @phone-number-event="phonenumbervalue($event)">

                </phone-number-component>

                <textarea-component 
                    
                    @textarea-event="textareavalue($event)">
                </textarea-component>

                <email-component 
                    
                    @email-event="emaileventvalue($event)">
                </email-component>
                <!-- <li>{{ editlist }}</li> -->
            </div>
            <div class="modal-footer">

                <button class="btn btn-success" v-on:click="onClick()">

                    Save

                </button>
                

                <button class="btn btn-secondary" @click="handleClose">

                    Close

                </button>

            </div>

        </div>

    </div>
  </div>
</template>

<script>
import axios from 'axios';
import TextComponent from './TextComponent.vue';
import TextareaComponent from './TextareaComponent.vue';
import PhoneNumberComponent from './PhoneNumberComponent.vue';
import RadioButtonComponent from './RadioButtonComponent.vue';
import SelectComponent from './SelectComponent.vue';
import EmailComponent from './EmailComponent.vue';
import CheckBoxComponent from './CheckBoxComponent.vue';

export default {
    components: {
        'text-component': TextComponent,
        TextareaComponent,
        PhoneNumberComponent,
        RadioButtonComponent,
        SelectComponent,
        EmailComponent,
        CheckBoxComponent
    },
    name: "App",
    data() {
        return {

            students: [],
            firstname: "",
            lastname: "",
            course: "",
            selectcourse: ["BCA", "B.Sc(IT)", "MCA", "M.Sc(IT)"],
            gender: "",
            hobbies:[],
            phone: '',
            address: "",
            email: "",
            options: ['Male', 'Female', 'Other'],
            Openclose: this.visible,

        }
    },
    props: {
        visible: Boolean,
        variant: String,
       // editlist: Object,
       
    },

    methods: {

        async onClick() {
            // console.log(editdata);
            try {
                const userdata = await axios.post(`http://localhost:3000/students/`, {
                    firstname: this.firstname,
                    lastname: this.lastname,
                    course: this.course,
                    gender: this.gender,
                    hobbies:this.hobbies,
                    phone: this.phone,
                    address: this.address,
                    email: this.email

                });
                // console.log(userdata.data);
                this.$emit("add-list", userdata.data);
                this.OpenClose = !this.OpenClose;
                this.$emit("close-modal-event");
            } catch (e) {
                console.log(e);
            }
            this.OpenClose = !this.OpenClose;
            this.$emit("close-modal-event");
        },

        handleClose() {
            this.Openclose = !this.Openclose;
            this.$emit('close-modal-event');

        },
        firstnamevalue(value) {
            //  alert('dsdsdsdsdsd');
            this.firstname = value;
        },
        lastnamevalue(value) {
            this.lastname = value;
        },
        textareavalue(value) {
            this.address = value;
        },
        phonenumbervalue(value) {
            this.phone = value;
        },
        radiobuttonvalue(value) {
            this.gender = value;
        },
        checkboxvalue(value){
            this.hobbies=value;
        },
        selectvalue(value) {
            this.course = value;
        },
        emaileventvalue(value) {
            this.email = value;
        }

    }
}
</script>

<style scoped>

</style>
