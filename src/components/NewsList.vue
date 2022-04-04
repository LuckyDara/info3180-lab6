<template>
    <ul class="news__list">
          <li v-for="article in articles" class="news__item">
              <div class="card" style="width:18 rem">
                  <img class="card-img-top" :src='article.urlToImage' alt="Card image cap"/>
                  <div class="card-body">
                      <h5 class="card-title" style="font-weight:600">{{ article.title }}</h5>
                      <p class="card-text">{{ article.description }}</p>
                    </div>
                </div>
            </li>
    </ul>
</template>
<script>
    export default {
        data() {
            return {
                articles:[]
            };
        },
        created() {
            let self = this;
            fetch('https://newsapi.org/v2/top-headlines?country=us',
            {
                headers: {
                    'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
                    }
            })
            .then(function(response) {
                 return response.json();
            })
            .then(function(data) {
                console.log(data);
                self.articles = data.articles;
            });
        }
    };
</script>

<style>
.news__item img{
    width: 100% !important;
}
.news__item{
    width: 30% !important;
    
}
.card{
    border-style: none;
    border-bottom: 3px solid lightseagreen;
    height: 500px;
    margin-bottom: 10%;
    box-shadow: 0px -3px 10px 3px rgb(196, 196, 196);
}
.card-body{
    text-align: left;
}
.news__list{
    list-style:none;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
    margin-top: 10%;
}
</style>