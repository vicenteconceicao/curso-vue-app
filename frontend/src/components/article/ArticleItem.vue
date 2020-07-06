<template>
    <div class="article-item">
        <router-link :to="{ name: 'articleById', params: { id: article.id }}">
            <div class="article-item-image d-none d-sm-block">
                <img :src="article.imageUrl ? article.imageUrl : '@assets/article.png'" height="150" width="150" alt="Article">
            </div>
            <div class="article-item-info">
                <h2> {{ article.name }} </h2>
                <p> {{ article.description }} </p>
                <span class="article-item-author">
                    <strong>Autor: <strong> {{ article.author }} </strong></strong>
                </span>
            </div>
        </router-link>
    </div>
</template>

<script>
export default {
    name: 'articleItem',
    props: ['article']
}
</script>

<style>
    .article-item{
        border-radius: 8px;
        margin-bottom: 20px;
        background-color: #FFF;
        padding: 20px;
        border: 1px solid rgba(0,0,0, .2);
    }

    .article-item a{
        display: flex;
        align-items: flex-start;
        text-decoration: none;
        color: black;
    }

    .article-item-info h2{
        font-size: 1.7rem;
    }

    .article-item-image{
        padding-right: 20px;
        margin-right: 20px;
        border-right: solid 1px #eee;
    }

    .article-item-image img{
       border-radius: 5px;
    }

    .article-item-info{
         display: flex;
         align-self: stretch;
        flex-direction: column;
    }

    .article-item-info p{
        flex: 1;
        color: #424242;
        font-size: 1.1rem;
    }
</style>