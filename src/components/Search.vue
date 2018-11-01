<template>
    <div class="row justify-content-center">
        <div class="text-center">
            <div class="form-group">
                <input type="text" class="form-control col-12" placeholder="Title" v-model="searchFilter">
                <button class="btn btn-primary col-6 mt-2" @click="fetchVideos">Search</button>
            </div>
        </div>
        <div class="container">
            <div class="row">
                <div class="col-md-4" v-for="(video, index) in videos" :key="video.id">
                    <Video :data="video"></Video>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    import Video from './Video';

    export default {
        name: 'Search',
        components: {
            Video
        },
        data() {
            return {
                searchFilter: '',
                videos: []
            }
        },
        methods: {
            fetchVideos() {
                axios.get('https://cors-escape.herokuapp.com/http://sbfunapi.cc/api/serials/tv_list/?query=' + this.searchFilter).then(response => {
                    this.videos = response.data;
                });
            }
        }
    }
</script>