<template>
    <div class="message-body">
        <div class="message-author">
            <p>{{ author }}</p>
        </div>
        <div class="message-text">
            <p>{{ text }}</p>
            <div class="message-time">
                <p>{{ time }}</p>
            </div>
        </div>
        <div class="message-close" v-on:click="delMessage(id)" v-bind:id="id">
            <svg width="11" height="12" viewBox="0 0 11 12" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M6.70499 6L10.85 1.855C10.9319 1.75935 10.9747 1.63631 10.9698 1.51047C10.965 1.38464 10.9128 1.26527 10.8238 1.17622C10.7347 1.08717 10.6154 1.03501 10.4895 1.03015C10.3637 1.02528 10.2406 1.06809 10.145 1.15L5.99999 5.295L1.85499 1.145C1.76083 1.05085 1.63314 0.997955 1.49999 0.997955C1.36684 0.997955 1.23914 1.05085 1.14499 1.145C1.05083 1.23915 0.997941 1.36685 0.997941 1.5C0.997941 1.63315 1.05083 1.76085 1.14499 1.855L5.29499 6L1.14499 10.145C1.09265 10.1898 1.05014 10.245 1.02012 10.307C0.990112 10.369 0.973247 10.4366 0.970587 10.5055C0.967928 10.5743 0.97953 10.643 1.00467 10.7072C1.0298 10.7713 1.06793 10.8296 1.11666 10.8783C1.16539 10.9271 1.22366 10.9652 1.28783 10.9903C1.35199 11.0155 1.42065 11.0271 1.48951 11.0244C1.55837 11.0217 1.62594 11.0049 1.68797 10.9749C1.75 10.9449 1.80516 10.9023 1.84999 10.85L5.99999 6.705L10.145 10.85C10.2406 10.9319 10.3637 10.9747 10.4895 10.9699C10.6154 10.965 10.7347 10.9128 10.8238 10.8238C10.9128 10.7347 10.965 10.6154 10.9698 10.4895C10.9747 10.3637 10.9319 10.2407 10.85 10.145L6.70499 6Z" fill="#969696"/>
            </svg>
        </div>
    </div>
</template>

<script>
    export default{
        name: 'MessageComponent',
        props: ['author', 'text', 'time', 'id', 'delMessage'],
        data (){
            return{
                
            }
        }
    }
</script>

<style>
    .message-body{
        position: relative;
        margin-left: 32px;
        margin-bottom: 24px;
        max-width: 329px;
    }

    .message-author{
        margin-bottom: 6px;
    }

    .message-author p{
        font-family: 'Roboto';
        font-style: normal;
        font-weight: 400;
        font-size: 16px;
        line-height: 19px;
        color: #5E5E5E;
    }

    .message-text{
        position: relative;
        width: 329px;
        min-height: 52px;
        height: auto;
        background: #F5F5F8;
        border-radius: 8px;
    }
    
    .message-text p{
        font-family: 'Roboto';
        font-style: normal;
        font-weight: 400;
        font-size: 16px;
        line-height: 19px;
        color: #222222;
        margin-left: 17px;
        margin-bottom: 17px;
        margin-top: 16px;
        white-space: pre-line;
    }

    .message-time{
        position: absolute;
        right: 6px;
        bottom: 6px;
        height: 15px;
        width: 33px;
    }

    .message-time p{
        font-family: 'Roboto';
        font-style: normal;
        font-weight: 400;
        font-size: 13px;
        line-height: 15px;
        color: #969696;
    }

    .message-close{
        position: absolute;
        top: 25px;
        right: -7px;
        cursor: pointer;
        width: 18px;
        height: 18px;
        display: flex;
        align-items: center;
        justify-content: center;
    }
</style>