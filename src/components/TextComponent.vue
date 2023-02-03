 <template>
<div>
    <div class="form-group">
        <label for="title">Enter Student FirstName</label>
        <input type="text" id="firstname" class="form-control" v-model="firstname" @input="textfirst" value="textdata" required />
    </div><br>
    <div class="form-group">
        <label for="title">Enter Student LastName</label>
        <input type="text" id="firstname" class="form-control" v-model="lastname" @input="textlast" value="textvalue" required />
    </div>

    <!-- {{ textdata.firstname }} -->
</div>
</template> 

<script>
export default {
    props: {
        textdata: String,
        textvalue: String
    },
    data() {
        return {
            firstname: this.textdata,
            lastname: this.textvalue
        }
    },
    methods: {

        textfirst() {
            //console.log(this.firstname);
            this.$emit('text-event-first', this.firstname);
        },
        textlast() {

            this.$emit('text-event-last', this.lastname);
        }
    }

}
</script>

<style lang="scss" scoped>

</style>
