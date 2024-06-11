<template>
    <div class="card_main">
        <div class="card_content">
            <h2>{{ props.title }}</h2>
            <p>{{ props.text }}</p>
        </div>
        <NuxtLink :to="`/document/${props.index}`" class="goto">Перейти</NuxtLink>
    </div>
</template>

<script setup>
import { defineProps } from 'vue'

const props = defineProps({
  title: {
    type: String,
    required: true
  },
  text: {
    type: String,
    required: true
  },
  index:{
    type: Number,
    required: true
  }
})
</script>

<style lang="scss" scoped>
.card_main{
    width: 30%;
    height: 450px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 25px;
    text-align: start;
    box-shadow: 0px 0px 20px 0px rgba(0, 0, 0, 0.12);
}

.card_content{
    h2{
        color: #1253A2;
        font-size: 31px;
        font-weight: bold;
        line-height: 120%;
        margin-bottom: 15px;
    }

    p{
        font-size: 18px;
        line-height: 120%;
    }
}

.goto{
    width: 100%;
    padding: 11px 110px;
    font-size: 18px;
    background-color: #0584FE;
    border-radius: 7px;
    color: white;

    &:hover{
        background-color: lighten(#0584fe, 10%)
    }
}


@media (max-width: 360px){
    .card_main{
        width: 100%;
    }

    .card_content{
    h2{
        font-size: 26px;
    }

    p{
        font-size: 16px;
    }
}
    .goto{
        display: flex;
        justify-content: center;
    }
}
</style>