<template>
<div class="container">

    <header>
        <h1 style="text-align:center; background-color:lightblue">Home Page</h1>

    </header>

    <section style="background-color:beige">

        <div>
            <div class="row d-flex justify-content-center align-items-center">

                <transition name="modal">
                    <div class="modal-mask" v-if="showModal" :visible="true">

                        <AddForm @add-list="addhome($event)" @close-modal-event="closeModal" />
                    </div>

                </transition>
                <transition name="modal">
                    <div class="modal-mask" v-if="showEditModal" :visible="true">

                        <EditForm :editlist="editdata" @update-list="updatehome()" @close-editmodal-event="closeEditModal" />
                    </div>
                </transition>
                <div class="col-md-12 col-xl-10">

                    <div class="card">
                        <div class="card-header p-5">
                            <h3>Students Details <button type="button" style="float:right;" class="btn btn-info" @click="showModal = true">Register Here</button></h3>

                        </div>
                        <div class="card-body" data-mdb-perfect-scrollbar="true" style="position: relative; ">
                            <table class="table">
                                <tr>
                                    <th scope="col" style="font-size:20px">StudentId</th>
                                    <th scope="col" style="font-size:20px">FirstName</th>
                                    <th scope="col" style="font-size:20px">LastName</th>
                                    <th scope="col" style="font-size:20px">Course</th>
                                    <th scope="col" style="font-size:20px">Gender</th>
                                    <th scope="col" style="font-size:20px">Hobby</th>
                                    <th scope="col" style="font-size:20px">Phone</th>
                                    <th scope="col" style="font-size:20px">Address</th>
                                    <th scope="col" style="font-size:20px">Email-Address</th>
                                    <th scope="col" style="font-size:20px">Actions</th>

                                </tr>

                                <tbody>
                                    <tr class="fw-normal" v-for="student in students" :key="student.id">
                                        <th scope="row">{{ student.id }}</th>
                                        <td>{{ student.firstname }}</td>
                                        <td>{{ student.lastname }}</td>
                                        <td>{{ student.course }}</td>
                                        <td>{{ student.gender }}</td>
                                        <td>
                                            <p v-for="hobbie in student.hobbies" :key="hobbie.id">
                                                {{ hobbie }}
                                            </p>
                                        </td>

                                        <td>{{ student.phone}}</td>
                                        <td>{{ student.address}}</td>
                                        <td>{{ student.email}}</td>
                                        <td class="align-middle">
                                          
                                            <button class="btn btn-primary" @click="editModal(student)">EDIT</button>&nbsp;

                                            <button id="delete" class="btn btn-secondary" v-on:click="removeTask(student.id)">DELETE</button>
                                        </td>
                                    </tr>
                                </tbody>

                            </table>

                        </div>

                    </div>
                </div>
            </div>
        </div>

    </section>

</div>
</template>

<script>
import axios from 'axios'
import AddForm from './components/AddForm.vue'
import EditForm from './components/EditForm.vue'
// import { EventBus } from '@/EventBus.js';
export default {
    name: 'App',
    data() {
        return {
            students: [],
            showModal: false,
            editdata: {},
            editbutton: false,
            showEditModal: false
        }
    },
    components: {
        AddForm,
        EditForm,

    },
    async created() {
        try {
            const res = await axios.get(`http://localhost:3000/students`);
            this.students = res.data;
            console.log(this.students);
        } catch (error) {
            console.log(error);
        }
    },
    methods: {
        addhome(value) {

            alert('Congratulations!!! You Registered Successfully');
            console.log(value, 'value');
            this.students.push(value);

        },
        async updatehome() {
            alert('Congratulations!!! You Updated Successfully');
            try {
                const res = await axios.get(`http://localhost:3000/students`);
                this.students = res.data;
            } catch (error) {
                console.log(error);
            }
            console.log(this.students);
        },
        
        closeModal() {

            this.showModal = false;
        },
        closeEditModal() {
            this.showEditModal = false;
        },
        removeTask(id) {
            axios.delete(`http://localhost:3000/students/${id}`);
            this.students = this.students.filter((student) => student.id !== id);
        },
        editModal(student) {
            //alert('rerereere');
            console.log(student);
            this.showEditModal = true;
            console.log(student);
            this.editdata = student;
            console.log(this.editdata, 'editdata');
        },
        // mounted() {
        //     EventBus.$on("update-list", () => {
        //         this.updatehome();
        //     });
        // },
        created() {
            this.updatehome();
        },
        // destroyed() {
        //     EventBus.$off("update-list");
        // },

    },

}
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
