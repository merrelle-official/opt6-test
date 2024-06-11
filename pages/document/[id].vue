<template>
    <div class="main">
        <nav>
            <ul>
                <li><NuxtLink to="/">Главная страница</NuxtLink></li>
                <li><NuxtLink to="/document">Документы</NuxtLink></li>
                <li><NuxtLink :to="`/document/${document.id}`">{{ document.title }}</NuxtLink></li>
            </ul>
        </nav>
        <h1 class="doc_name"> {{ document.title }}</h1>
        <div v-for="(item, index) in document.content" :key="index" class="content">
            <h2>{{ item.title }}</h2>
            <p v-html="item.text"></p>
        </div>
    </div>
</template>

<script setup>
const { id } = useRoute().params
import {documents} from "../data/datafile"

const document = documents.find(doc => doc.id == id);

console.log(document)

</script>

<style lang="scss" scoped>
    .main{
        margin: 0 auto;
        width: 60.7%;
        display: flex;
        flex-direction: column;
        *{
            transition: all 0.2s ease-in-out;
        }

        ul{
            display: flex;
            gap: 25px;
            margin: 20px 0;

            *{
                font-size: 13px;
            }

            >:first-child{
                list-style: none;
            }
            >:last-child>*{
                color: #8F8F8F;
            }
        }
    }

    .doc_name{
        font-size: 41px;
        margin-bottom: 40px;
    }
    
    .content{
        margin-bottom: 25px;
        h2{
            font-size: 41px;
            color: #383838;
            margin-bottom: 25px;
        }
    }

    @media (max-width: 360px){

        .main{
            width: 80%;

            ul{
                display: flex;
                width: 100%;
                justify-content: start;
                flex-wrap: wrap;
                *{
                    font-size: 10px;
                    text-wrap: nowrap;
                }
            }
        }
        .doc_name{
            font-size: 36px;
        }

        .content{
            margin-bottom: 25px;
            h2{
                font-size: 36px;
                color: #383838;
                margin-bottom: 25px;
            }
        }
    }
</style>