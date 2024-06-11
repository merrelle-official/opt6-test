<template>
    <div class="main">
        <nav>
            <ul>
                <li><NuxtLink to="/">Главная страница</NuxtLink></li>
                <li><NuxtLink to="/document">Документы</NuxtLink></li>
            </ul>
        </nav>
        <h1>Документы</h1>
        <section id="documents">
            <h2>Документы</h2>
            <div class="document_container">
                <button class="prev_slide" @click="prevClick"><img src="/images/slider_arrow.svg" alt="Предыдущий слайд"  /></button>
                <div class="slider">
                    <div class="container_inner" :style="{ transform: `translateX(-${currentSlide * 100 + currentSlide * 5}%)` }">
                        <DocumentCard v-for="(item, index) in documents" :key="index" :title="item.title" :text="item.text" :index="item.id" />
                    </div>
                </div>
                <button class="next_slide" @click="nextClick"><img src="/images/slider_arrow.svg" alt="Следующий слайд" ></button>
            </div>
            <div class="slider_pages">
                <div v-for="(item, index) in slider_length" :key="index" :class="['slider_page', { active: index === currentSlide }]"></div>
            </div>
        </section>
    </div>
</template>

<script setup>
    import {documents} from "../data/datafile"
    let slider_length = documents.length / 3;
    const currentSlide = ref(0)

    const nextClick = () =>{
         currentSlide.value++
    }

    const prevClick = () =>{
        currentSlide.value--
    }
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
    #documents{
        width: 98.1%;
        display: flex;
        flex-direction: column;
        text-align: center;
        margin-top: 85px;
        margin-bottom: 473px;
        >h2{
            font-size: 34px;
            font-weight: bold;
        }
    }

    .document_container{
        margin-top: 40px;

        position: relative;
        
        .prev_slide{
            width: 40px;
            height: 80px;
            position: absolute;
            background-color: rgba(166, 183, 212, 0.471);
            border-radius: 0 40px 40px 0;
            display: flex;
            justify-content: center;
            align-items: center;
            top: 50%;
            transform: translateY(-50%);
            z-index: 1;
        }

        .next_slide{
            width: 40px;
            height: 80px;
            position: absolute;
            background-color: rgba(166, 183, 212, 0.471);
            border-radius: 0 40px 40px 0;
            display: flex;
            justify-content: center;
            align-items: center;
            top: 50%;
            right: 0;
            transform: translateY(-50%) rotate(180deg);
            z-index: 1;
        }
    }

    .slider{
        overflow: hidden;
        margin: 0 2.6%;
    }

    .container_inner{
        display: flex;
        flex-wrap: nowrap;
        gap: 5%;
        position: relative;
    }

    .slider_pages{
        display: flex;
        justify-content: center;
        gap:5px;
    }

    .slider_page{
        display: inline-block;
        border-radius: 50%;
        background-color: #D9D9D9;
        height: 7px;
        width: 7px;
    }

    .active{
        background-color: #007AFF;
            height: 10px;
            width: 10px;
    }

    @media (max-width: 360px){

        .main{
            width: 80%;
        }

        #documents{
            width: 100%;
            text-align: start;
            >h2{
                font-size: 28px;
            }
        }
    }

</style>