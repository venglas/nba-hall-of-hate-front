<template>
 <div class="alert alert-danger modal--error" role="alert" v-if="$store.state.errors.error.isVisible">
    {{$store.state.errors.error.content}}
    <button class="btn close" @click="$store.commit('hideError')">
        x
    </button>
</div>
</template>
 
<script>
export default {
name: 'Error-modal',
components: {},
data() {
    return {}
},
props: {},
computed: {},
watch: {},
mounted() {},
created() {
    this.autoRemoveError();
},
methods: {
    autoRemoveError() {
        setTimeout(() => {
            this.$store.commit("hideError")    
        }, 1000 * 15);
    }
}
}
</script>

<style lang='scss'>
.modal {
    &--error {
        position: sticky;
        top: 65px;
        z-index: $zMax;
    }
}
</style>