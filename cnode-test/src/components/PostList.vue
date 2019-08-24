<template>
    <div>
        <div class="loading" v-if="isLoading">
            <img src="../assets/loading.gif" alt="">
        </div>
        <div>
            <ul>
                <li></li>
            </ul>
        </div>
    </div>
</template>    

<script>
export default {
    name: "PostList",
    data() {
        return {
            isLoading: false
        }
    }
}
</script>

<style lang="stylus" scoped>

</style>