<template>
    <div class="card_main">
        <img :src="props.src" alt="">
        <div class="card_content">
            <h3>{{ props.title }}</h3>
            <p>{{ props.text }}</p>
        </div>
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
  src: {
    type: String,
    required: true
  }
})


</script>

<style lang="scss" scoped>
    .card_main{
        border-radius: 10px;
        background-color: #FBFCFD;
        border: 1px solid #EEEFF1;
        width: 362px;
        height: 151px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        text-align: start;
        padding: 41px 20.11px 42px 20.11px;
    }

    .card_content{
        display: flex;
        flex-direction: column;
        gap: 10px;
        width: 247.37px;
        h3{
            font-size: 18px;
            font-weight: bold;
            line-height: 120%;
            color: #1253A2
        }

        p{
            font-size: 15px;
            line-height: 120%;
        }
    }

    @media (max-width: 360px) {
      .card_main{
        height: 120px;
        width: 100%;
        gap: 10px;
        padding: 0;
        >img{
          transform: scale(0.8)
        }
      }

      .card_content{
        h3{
            font-size: 16px;
            font-weight: bold;
            line-height: 120%;
            color: #1253A2
        }

        p{
            font-size: 13px;
            line-height: 120%;
        }
      }
    }
</style>