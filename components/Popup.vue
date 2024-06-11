<template>
    <div v-if="isPopupVisible" class="popup-overlay" @click="closePopup">
      <div class="popup-content">
        <button class="close-button" @click="closePopup"><img src="/images/close_popup.svg" alt=""></button>
        <iframe class="responsive_iframe"
          width="960"
          height="532"
          :src="videos"
          frameborder="0"
          allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
          allowfullscreen
        ></iframe>
      </div>
    </div>
  </template>
  
  <script setup>
    import { ref, defineProps } from 'vue'
    const emit = defineEmits(['inFocus', 'submit'])
    const props = defineProps({
        isPopupVisible: Boolean
    });
  
    const videos = 'https://www.youtube.com/embed/9xK_UHpWbsY';
    
    function closePopup() {
        emit('close-popup');
    }
  </script>
  
  <style scoped>
  .popup-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.7);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
  }
  
  .popup-content {
    position: relative;
    background: white;
    padding: 0;
    border-radius: 8px;
    background: none;
  }
  
  .close-button {
    margin-left: auto;
    margin-bottom: 8px;
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  @media (max-width: 360px){
 .responsive_iframe{
        width: 100%;
        height:250px;
    }
  }
 
  </style>
  