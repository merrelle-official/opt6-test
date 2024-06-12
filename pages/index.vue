<template>
    <div class="main">
        <section id="check_fine">
            <form class="check_form">
                <h1>Проверьте штрафы и<br>зарегестрируйтесь в 1 клик</h1>
                <div class="first_row">
                    <div class="number">
                        <label for="carNumber">Номер автомобиля</label>
                        <input type="text" name="carNumber" id="carNumber" @input="handleInput" :class="inputsIsEmpty ? 'empty' : ''" >
                    </div>
                    <div class="area">
                        <label for="area">Регион</label>
                        <input type="text" name="area" id="area" @input="handleInput" :class="inputsIsEmpty ? 'empty' : ''">
                    </div>
                </div>
                <div class="second_row">
                    <label for="registration">Свидетельство о регистрации ТС</label>
                    <input type="text" name="registration" id="registration" @input="handleInput" :class="inputsIsEmpty ? 'empty' : ''">
                </div>
                <div class="form_buttons">
                    <button class="submit" @click="submitForm">Проверить штрафы</button>
                    <button class="about" @click="showPopup">О сервисе<span>(1 мин. 20 сек)</span></button>
                </div>
                <p class="warning_text">Нажимая «Проверить штрафы» вы соглашаетесь с политикой обработки персональных данных и принимаете оферту</p>
            </form>
            <img src="/images/banner_img.png" alt="">
        </section>

        <section id="advantages">
            <h2>Плюсы использования сервиса «Компас» для анализа штрафов</h2>
            <div class="advantages_cards">
                <AdvantagesCard v-for="(item, index) in advantages" :key="index" :src="item.src" :title="item.title" :text="item.text" />
            </div>
        </section>

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

        <div class="sended" v-if="formSended">
            <h3>Данные отправлены</h3>
            <img src="/images/check.svg" alt="">
        </div>

        <Popup :isPopupVisible="isPopupVisible" @close-popup="hidePopup"/>

    </div>
</template>

<script setup>
    import {documents, advantages} from "../data/datafile"
    import { ref } from 'vue';

    const slider_length = ref(0)
    const currentSlide = ref(0)
    const checkData = ref({carNumber: "", area: "", registration: ""})
    const inputsIsEmpty = ref(false)
    const formSended = ref(false)
    const isPopupVisible = ref(false)

    const handleResize = () => {
        if( window.innerWidth <= 600 ) slider_length.value = documents.length
        else if( window.innerWidth <= 1000 ) slider_length.value = documents.length / 2
        else slider_length.value = documents.length / 3
        
    };

    onMounted(() => {
        if( window.innerWidth <= 600 ) slider_length.value = documents.length
        else if( window.innerWidth <= 1000 ) slider_length.value = documents.length / 2
        else slider_length.value = documents.length / 3
        window.addEventListener('resize', handleResize);
    });

    onUnmounted(() => {
        window.removeEventListener('resize', handleResize);
    });

    function setFieldRed(){
        inputsIsEmpty.value = true
        setTimeout(() => {
            inputsIsEmpty.value = false
        }, 2000)
    }

    const nextClick = () =>{
        if( currentSlide.value != slider_length.value - 1 )
        currentSlide.value++
    }

    const prevClick = () =>{
        if(currentSlide.value != 0){
            currentSlide.value--
        }

    }

    const handleInput = (e) => {
        checkData.value = { ...checkData.value, [e.target.name]: e.target.value };
    };

    const submitForm = (e) => {
        e.preventDefault()
        for(let key in checkData.value) {
            if(checkData.value[key] === "" && key !== '') {
                setFieldRed()
                return
            }
        }   
        formSended.value = true;
        setTimeout(() => {
            formSended.value = false;
        }, 2000)

    }

    const showPopup = (e) => {
        e.preventDefault()
        isPopupVisible.value = true;
        console.log(isPopupVisible.value)
    }

    const hidePopup = () => {
        isPopupVisible.value = false;
        console.log(isPopupVisible.value)
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
    }

    #check_fine{
        display: flex;
        margin-top: 79px;
        gap: 40px;

        >img{
            height: 335px;
            width: 532.18px;
        }
    }

    .check_form{
        display: flex;
        flex-direction: column;
        flex-basis: 563px;
        >h1{
            font-size: 41px;
            line-height: 120%;
            margin-bottom: 25px;
        }
    }

    .first_row{
        display: flex;
        gap: 30px;
        width: 100%;
        margin-bottom: 14px;

        >div{
            display: flex;
            flex-direction: column;
            gap: 5px;
        };

        .number{
            width: 320px;
        };

        .area{
            width: 213px;
        };
    }

    .second_row{
        display: flex;
        flex-direction: column;
        gap: 5px;
        margin-bottom: 15px;
    }

    .form_buttons{
        display: flex;
        gap: 21px;
        margin-bottom: 17px
    }

    button{
        border-radius: 7px;
        padding: 11px 20px;
        font-size: 18px;
        height: 45px;
        display: flex;
        align-items: center;
    }

    .submit{
        background-color: #0584FE;
        color: white;
        &::after{
            content: "";
            display: inline-block;
            width: 14.01px;
            height: 12.27px;
            background: url('/images/submit.svg') no-repeat center center;
            background-size: contain;
            margin-left: 4px;
        }

        &:hover{
            background-color: lighten(#0584fe, 10%)
        }
    }

    .about{
        border: 1px solid #0584FE;

        span{
            color: #1253A2;
            font-size: 15px;
            margin-left: 4px
        }

        &:hover{
            background-color: darken($color: white, $amount: 10%)
        }

        &::before{
            content: "";
            display: inline-block;
            width: 32.25px;
            height: 23px; 
            background: url('/images/about.svg') no-repeat center center;
            background-size: contain;
            margin-right: 5.59px;
        }
    }

    .warning_text{
        color: #8F8F8F;
        font-size: 13px;
        line-height: 120%;
    }


    #advantages{
        width: 98.1%;
        display: flex;
        flex-direction: column;
        text-align: center;
        margin-top: 101px;

        >h2{
            font-size: 34px;
            font-weight: bold;
        }
    }

    .advantages_cards{
        margin-top: 35px;
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        grid-template-rows: 1fr 1fr;
        gap: 35px;
        justify-content: space-between
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

    .empty{
        border-color: red;
    }

    .sended{
        position: fixed;
        bottom: 0;
        right: 0;
        padding: 10px 30px;
        margin: 40px;
        background-color: white;
        border: 1px solid #61DE56;
        border-radius: 7px;
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 20px;
        box-shadow: 0px 0px 20px 2px rgba(97, 222, 86, 1);
        img{
            height: 30px;
            width: 30px;
        }
    }
    
    @media (max-width: 1600px) {
        .main{
            width: 80%;
        }

        #check_fine{
            width: 100%;
            align-items: center;
            >img{
                
                width: 50%;
                height: auto;
            }
        }

        .check_form{
            flex-basis: auto;
            >h1{
                font-size: 30px;
            }
        }

        .first_row{
            .number{
                flex-basis: 70%;
            };
            .area{
                flex: 1;
            };
        }

        .second_row{
            margin-bottom: 20px;
        }

        .form_buttons{
            >*{
                display: flex;
                justify-content: center;
                flex: 1;
            }
        }

        #advantages{
            width: 100%;
            >h2{
                font-size: 28px;
            }
        }

        #documents{
            width: 100%;
            
            >h2{
                font-size: 28px;
                text-align: center;
            }
        }

    }

    @media (max-width: 1280px) {

        #check_fine{
            >img{
                width: 40%;
            }
        }

        .advantages_cards{
            grid-template-columns: 1fr 1fr;
            grid-template-rows: 1fr 1fr 1fr;
            justify-items: center;
        }

    }

    @media (max-width: 1000px) {

        #check_fine{
            flex-direction: column;
            align-items: center;
            >img{
                width: 50%;
            }
        }

        .check_form{
            flex-basis: auto;
            >h1{
                text-align: center;
                font-size: 30px;
            }
        }

        #advantages{
            width: 100%;
            >h2{
                font-size: 28px;
            }
        }

        .advantages_cards{
            grid-template-columns: 1fr 1fr;
            grid-template-rows: 1fr 1fr 1fr;
            justify-items: center;
        }

    }

    @media (max-width: 830px) {

        .first_row{
            flex-direction: column;
            gap: 14px;
            .number{
                width: 100%;
            };
            .area{
                width: 100%;
            };
        }


        .advantages_cards{
            gap: 15px;
        }

        #documents{
            text-align: start;
        }

    }

    @media (max-width: 768px) {
        .form_buttons{
            flex-direction: column;
            >*{
                display: flex;
                justify-content: center;
            }
        }

        .advantages_cards{
            display: flex;
            flex-direction: column;
            
        }
    }




    
</style>