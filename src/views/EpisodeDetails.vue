<template>
    <div class="container justify-content-center">
    <div class="row justify-content-center">
        <div class="col-4">
            <div class="card">
                <div class="card-header">
                    {{ data.title }}
                </div>
                <ul class="list-group list-group-flush">
                    <li class="list-group-item">Season: <b>{{ data.season }}</b></li>
                    <li class="list-group-item">Episode: <b>{{ data.episode }}</b></li>
                    <li class="list-group-item">Runtime: <b>{{ data.runtime }}</b></li>
                    <li class="list-group-item">{{ data.synopsis }}</li>
                </ul>
            </div>
        </div>
        <div class="col-8">
            <div class="card">
                <div class="card-header">
                    Featured
                </div>
                <ul class="list-group list-group-flush">
                    <li class="list-group-item" v-for="item in data.items">
                        <a :href="item.torrent_magnet">
                            {{ item.file }} |
                            {{ item.quality}} |
                            {{ item.size_bytes}} |
                            {{ item.torrent_seeds }} / {{ item.torrent_peers }}
                        </a>
                    </li>
                </ul>
            </div>
        </div>
    </div>
    </div>
</template>

<script>
    import axios from 'axios'
    export default {
        name: "EpisodeDetails",
        data() {
            return {
                imdbid: this.$route.params.imdbid,
                season: this.$route.params.season,
                episode: this.$route.params.episode,
                data: {}
            }
        },
        methods: {
            fetchData() {
                let allData = {};
                if(localStorage.getItem(this.imdbid)) {
                    allData = JSON.parse(localStorage.getItem(this.imdbid));
                    this.data = allData[this.season][this.episode-1];
                }
                else {
                    axios.get('https://cors-escape.herokuapp.com/http://api.ukfrnlge.com/show?imdb=' + this.imdbid).then(({data}) => {
                        allData = data;
                        localStorage.setItem(this.imdbid, JSON.stringify(data));
                        this.data = allData[this.season][this.episode-1];
                    });
                }
            },
            /*torrentHealth(seeds, peers) {
                let c = Math.max(seeds / peers, 1) * 70 + 10;

                return 'border-left: solid hsl('+c+', 100%, 50%)';
            }*/
        },
        created() {
            this.fetchData();
        }
    }
</script>

<style scoped>

</style>