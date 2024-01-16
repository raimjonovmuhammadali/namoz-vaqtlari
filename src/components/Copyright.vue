<template>
    <div class="container copy" style="height: 60px; display: flex; justify-content: space-between; align-items: center; padding: 0;">
        <p>PrayerTimes &copy;2024</p>
        <p>Developer by: <a href="" style="color: green;">Raimjonov Muhammadali</a></p>
    </div>
</template>
<script>
export default {
    
}
</script>
<style>
    .copy p {
        margin-bottom: 0;
    }

    @media screen and (max-width: 447px){
        .copy{
            display: flex;
            flex-direction: column;
            gap: 0;
            margin: 5px 0;
            padding: 0;
        }

        .copy p {
            margin: 0;
            padding: 0;
        }
}
</style>