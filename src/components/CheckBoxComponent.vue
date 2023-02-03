<template>
<div>

    Select Your Hobbies: &nbsp;<label>Reading Books</label>
    <input type="checkbox" value="reading Books" id="reading" v-model="hobbies" @change="checkboxchange">&nbsp;
    <label>Listening Music</label>
    <input type="checkbox" value="listening music" id="listeningmusic" v-model="hobbies" @change="checkboxchange">&nbsp;
    <label>Travel</label>
    <input type="checkbox" value="travelling" id="travelling" v-model="hobbies" @change="checkboxchange">&nbsp;
    <label>Sports</label>
    <input type="checkbox" value="sports" id="sports" v-model="hobbies" @change="checkboxchange">
    <ul>
        <li v-for="hobby in hobbies" :key="hobby.id">
            {{ hobby }}
        </li>
    </ul>

</div>
</template>

<script>
export default {
    data() {
        return {
            hobbies: this.checkboxprop
        }

    },
    props: {
        checkboxprop: {
            type: Array,
            default: function () {
                return [];
            }
        }},


        methods: {
            checkboxchange() {
                this.$nextTick(() => {
                    this.$emit('checkbox-event', this.hobbies);

                });

            }
        }

    }

</script>

<style lang="scss" scoped>

</style>
