<template>
    <input
        :type="useTextInputs ? 'text' : 'time'"
        class="form-control form-input form-input-bordered"
        :class="{ 'border-danger': !isValid }"
        v-model.lazy="time"
        minlength="5"
        maxlength="5"
        required
    >
</template>

<script>
import {useTextInputsProp} from "../src/props";

export default {
    props:  {
        timeProp: String,
        ...useTextInputsProp,
    },

    emits: ['updateTime'],

    data: function () {
        return {
            time: this.timeProp,
        }
    },

    computed: {
        isValid: function () {
            const re = /([0-9]|0[0-9]|1[0-9]|2[0-3]):[0-5][0-9]/;
            // console.log(this.time, re.test(this.time))
            return re.test(this.time);
        }
    },

    watch: {
        time(value) {
            this.$emit('updateTime', value)
        },
    },
}
</script>

<style scoped>
input[type="text"] {
    width: 75px;
}
</style>
