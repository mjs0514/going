<template>
<div class="movies">
  <h1>호카게 리스트</h1>
  <div v-for="movie in movies" class="movie">
    <img v-bind:src="movie.image" class="guide-image img-fluid img-thumbnail">
    <div>
      <strong>{{movie.name}}</strong>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'Guide',
  created() {
    let config = {
      headers: {
        "Authorization": `Bearer ${sessionStorage.getItem('authToken')}`,
      }
    };

    this.$http.get('/service/auth/test', config)
      .then((res) => {
        alert('인증된 사용자임이 확인되어 올바른 데이터를 가져옵니다');
        console.log(res.data.decoded.aud);
      })
      .catch((error) => {
        alert('인증된 사용자가 아니어서 데이터를 가져오지 않습니다');
        console.log(error);
      })
    // this.$http.get('/service/movies')
    //   .then((response) => {
    //     this.movies = response.data
    //   })
  },
  data() {
    return {
      movies: []
    }
  }
}
</script>

<style>
.guide-image {
  width: 150px;
  height: 150px;
}
</style>
