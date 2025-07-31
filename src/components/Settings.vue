
<template>
    <div class="modal" v-if="isSet" @click.self="closeModal">
      <div class="modal-content">
        <button class="close" @click="closeModal" style="border-radius: 15px; border: none"><img src="../../src/assets/img/no.png" alt="cross"></button>
        <p ><strong>SYNOPSIS:</strong> <br> </p>
        <p ><strong>AGE LIMIT:</strong> </p> 
        <p ><strong>GENRE: </strong></p>
        <p ><strong>AIRING:</strong> </p> 
        <p ><strong>STATUS:</strong> </p> 
      </div>
    </div>
  </template>
  
  <script>
  
  export default {
    props: {
      isSet: {
        type: Boolean,
        required: true,
      }
    },
    methods: {
      closeModal() {
        this.$emit('close');
      },
    }
};
  </script>
  
  <style scoped>
  .modal {
    display: flex;
    justify-content: center;
    align-items: center;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(59, 29, 56, 0.3);
    z-index: 200;
    color: #9074A8;
  }
  .modal-content {
    background-color: rgb(255 209 220 / .95);
    padding: 20px;
    border-radius: 8px;
    height: 650px;
    width: 600px;
	align-items: center;
	justify-content: center;
	text-align: center;
    margin-top: 65px;
    overflow: scroll;
    font-family: Lora;
    font-size: 14px;
  }

  .modal-content li {
    text-align: justify;
  }

  .modal-content h2 {
    margin-bottom: 5px;
  }
  .modal-content p {
    text-align: justify;
    margin-bottom: 5px;
  }

.image_inner {
    width: 200px;
	height: 200px;
    border-radius: 8px;
    margin-top: -47px;
    margin-bottom: 7px;
  }
  .close {
    display: block;
    cursor: pointer;
    background-color: rgb(255 209 220 / .95);
  }
  .close img {
    width: 50px;
    height: 50px;
  }
  </style>
  