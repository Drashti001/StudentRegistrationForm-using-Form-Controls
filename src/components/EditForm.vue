<template>
    <div class="container">
        <div class="modal-dialog modal-dialog-centered modal-dialog-scrollable">
            <div class="modal-content">
                <div class="modal-header">
                    <h5>Edit Data</h5>
                </div>
                <div class="modal-body">
                    <text-component 
                        :textdata="editlist.firstname"
                        :textvalue="editlist.lastname"
                        @text-event-first="firstnamevalue($event)"
                        @text-event-last="lastnamevalue($event)"   
                    >
                    </text-component>
                   <select-component 
                        :selectprop="editlist.course" 
                        v-bind:selectallcourse="selectcourse" 
                        @select-event="selectvalue($event)"
                       >
                    </select-component> 
  
                      <radio-button-component 
                        :radiodata="editlist.gender" 
                        :options="options"
                        @radio-button-event="radiobuttonvalue($event)"
                        >
                    </radio-button-component>
     
                  <check-box-component 
                        :checkboxprop="editlist.hobbies"
                        
                        @checkbox-event="checkboxvalue($event)">
                    </check-box-component>
    
                    <phone-number-component 
                        :phonenumberdata="editlist.phone" 
                        @phone-number-event="phonenumbervalue($event)">
    
                    </phone-number-component>
    
                    <textarea-component 
                        :textareadata="editlist.address" 
                        @textarea-event="textareavalue($event)">
                    </textarea-component>
    
                    <email-component 
                        :emailprops="editlist.email" 
                        @email-event="emaileventvalue($event)">
                    </email-component> 
                    <!-- <li>{{ editlist }}</li> -->
                </div>
                <div class="modal-footer">
    
                   
                    <button class="btn btn-success"  v-on:click="onEditClick(edit)">
                        Edit
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
   //import { EventBus } from '@/EventBus.js';
    
    export default {
        components: {
            TextComponent,
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
                efirstname: "",
                elastname: "",
                ecourse: "",
                selectcourse: ["BCA", "B.Sc(IT)", "MCA", "M.Sc(IT)"],
                egender: "",
                ehobbies:[],
                ephone: '',
                eaddress: "",
                eemail: "",
                options: ['Male', 'Female', 'Other'],
                Openclose: this.visible,
                edit:this.editlist
    
            }
        },
        props: {
            visible: Boolean,
            variant: String,
            editlist: Object,
            
        },
      
        methods: {
    
            async onEditClick(edit) {
                // console.log(editdata);
                //console.log(edit.id);
                //console.log(edit.firstname);
                try {
                    const userdata = await axios.put(`http://localhost:3000/students/` + edit.id,
                     {
                        firstname: this.efirstname == "" ? edit.firstname : this.efirstname,
                        
                       
                        lastname: this.elastname == "" ? edit.lastname : this.elastname,
                        course: this.ecourse == "" ? edit.course : this.ecourse,
                        gender: this.egender == ""? edit.gender : this.egender,
                        hobbies: this.ehobbies == "" ? edit.hobbies : this.ehobbies,
                        phone: this.ephone == "" ? edit.phone : this.ephone,
                        address: this.eaddress == "" ? edit.address : this.eaddress,
                        email: this.eemail == "" ? edit.email : this.eemail
    
                    });
                     console.log(userdata.data,'getting userdata');
                     //EventBus.$emit("update-list");
                    this.$emit("update-list");
                    this.OpenClose = !this.OpenClose;
                    this.$emit("close-editmodal-event");
                } catch (e) {
                    console.log(e);
                }
                this.OpenClose = !this.OpenClose;
                this.$emit("close-editmodal-event");
            },
    
    
            handleClose() {
                this.Openclose = !this.Openclose;
                this.$emit('close-editmodal-event');
    
            },
            firstnamevalue(value) {
                // alert('dsdsdsdsdsd');
                this.efirstname = value;
            },
            lastnamevalue(value) {
                this.elastname = value;
            },
            textareavalue(value) {
                this.eaddress = value;
            },
            phonenumbervalue(value) {
                this.ephone = value;
            },
            radiobuttonvalue(value) {
                this.egender = value;
            },
            checkboxvalue(value){
                this.ehobbies=value;
            },
            selectvalue(value) {
                this.ecourse = value;
            },
            emaileventvalue(value) {
                this.eemail = value;
            }
    
        }
    }
    </script>
    
    <style scoped>
    
    </style>
    