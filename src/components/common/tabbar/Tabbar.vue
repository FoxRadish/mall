<template>
    <div>
        <router-view></router-view>
        <mintabbar></mintabbar>
    </div>
</template>

<script>
import MintabbarVue from '../../comment/Mintabbar.vue'

export default {
    components: {
        mintabbar:MintabbarVue
    }
}
</script>

<style>

</style>