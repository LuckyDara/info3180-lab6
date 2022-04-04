<script>
import NewsList from '@/components/NewsList.vue'
    export default {
        data() {
            return {};
        },
        components: { NewsList }
    };
</script>
<template>
    <div class="news container">
        <h2>News</h2>
        <NewsList />
    </div>
</template>

<style>
.news {
    font-family: Georgia, 'Times New Roman', Times, serif;
    text-align: center;
}
.news h2{
    font-family: Georgia, 'Times New Roman', Times, serif;
    text-align: left;
    margin: 15px;
    font-weight: 500;
}
</style>