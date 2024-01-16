<template>
  <Navbar />
        <Box/>
        <Copyright/>
</template>

<script>
import Navbar from "./components/Navbar.vue"
import Box from "./components/Box.vue"
import Loader from "./components/Loader.vue"
import Copyright from "./components/Copyright.vue"
export default {
    components: {
        Navbar,
        Box,
        Loader,
        Copyright,
    }
}
</script>

<style scoped>

</style>
