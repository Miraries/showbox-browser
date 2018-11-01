<template>
    <div>
              <div class="card mb-4 box-shadow">
                <img class="card-img-top" :src="poster_url" alt="Card image cap">
                <div class="card-body">
                  <p class="card-text">{{ title }}</p>
                </div>
              </div>
            </div>
</template>
<script>
    export default {
        name: 'Video',
        props: ['data'],
        data() {
            return {
                id: this.data.id,
                title: this.data.title,
                poster_url: this.data.poster
            }
        }
    }
</script>
