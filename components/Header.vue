<template>
    <div class="header">
        <div class="header_container">
            <nav>
                <NuxtLink to="/"><img src="/images/header_logo.svg" alt="logo"></NuxtLink>
                <NuxtLink to="/tariffs">Тарифы</NuxtLink>
                <NuxtLink to="/contacts">Контакты</NuxtLink>
            </nav>
            <nav>
                <p class="phone">+7 495 118-44-22</p>
                <button class="signin">Вход</button>
                <button class="signup">Регистрация</button>
            </nav>
        </div>
    </div>
</template>

<script setup>

</script>

<style lang="scss" scoped>
    .header{
        width: 100%;
        height: 60px;
        background: linear-gradient(90deg, #000000 30%, #1C2734 73%);
        
        *{
            color: white;
            transition: all 0.2s ease-in-out;
        }
    }
    .header_container{
        height: 100%;
        margin: 0 auto;
        width: 60.7%;
        display: flex;
        align-items: center;
        justify-content: space-between;

        
        
        nav{
            display: flex;
            align-items: center;

            *{
                font-size: 18px
            };

            .signup{
                padding: 9px 18px;
                border-radius: 7px;
                background-color: #0584fe;
                font-size: 15px;

                &:hover{
                    background-color: lighten(#0584fe, 10%)
                }

            }

            .signin{
                padding: 7px 18px;
                border-radius: 7px;
                &:hover{
                    background-color: rgba($color: white, $alpha: 0.2)
                }
            }

            .phone{
                font-weight: bold;
            }
        }
        :first-child{
            
            gap:6px;
            img{
                margin-right: 12px
            }

            >:not(:first-child){
                padding: 7px 12px;
                border-radius: 7px;
            }

            >:not(:first-child):hover{
                background-color: rgba($color: white, $alpha: 0.2)
            }
        }
        :last-child{
            gap: 12px;
        }
    }

    @media (max-width: 360px) {
        .header{
            height: auto;
        }

        .header_container{
            flex-direction: column;
            align-items: center;
            width: 80%;
            >:last-child{
                flex-wrap: wrap;
                justify-content: center;
                margin: 10px 0;
            }

            >:last-child>p{
                flex-basis: 100%;
                text-align: center
            }
        }

    }

</style>