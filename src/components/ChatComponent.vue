<template>
    <div class="frame">
        <div class="left-block">
            <div class="head"></div>
            <div class="messages">
                <MessageComponent
                    v-for="msg in messages"
                    :key="msg.id"
                    v-bind:author="msg.author"
                    v-bind:text="msg.text"
                    v-bind:time="msg.time"
                    v-bind:id="msg.id"
                    v-bind:delMessage="deleteMessage"
                ></MessageComponent>
            </div>
            <div class="message-send">
                <div class="message-send-inner input-group">
                    <input type="text" name="message" v-model="messageText" :placeholder="input_holder">
                    <div class="send-btn" v-on:click="sendMessage">
                        <svg width="22" height="22" viewBox="0 0 22 22" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <path d="M21.0187 10.2213L1.76874 0.596256C1.61786 0.520801 1.44839 0.490569 1.28073 0.509197C1.11307 0.527826 0.954373 0.594523 0.82374 0.701255C0.698987 0.805812 0.605871 0.943094 0.554861 1.09767C0.503851 1.25224 0.49697 1.41798 0.53499 1.57626L3.12499 11L0.49999 20.3975C0.464314 20.5297 0.460149 20.6684 0.487832 20.8025C0.515514 20.9365 0.574272 21.0622 0.65938 21.1695C0.744487 21.2767 0.85357 21.3625 0.977857 21.4199C1.10214 21.4773 1.23817 21.5047 1.37499 21.5C1.51197 21.4992 1.64683 21.4662 1.76874 21.4038L21.0187 11.7788C21.1621 11.7053 21.2823 11.5938 21.3663 11.4564C21.4503 11.319 21.4948 11.161 21.4948 11C21.4948 10.839 21.4503 10.681 21.3663 10.5436C21.2823 10.4062 21.1621 10.2947 21.0187 10.2213V10.2213ZM2.73124 18.9713L4.66499 11.875H12.75V10.125H4.66499L2.73124 3.02876L18.665 11L2.73124 18.9713Z" fill="#0047FF"/>
                        </svg>
                    </div>
                </div>
            </div>
        </div>
        <div class="right-block">
            <div class="login-form">
                <label for="login-input">{{ label_text }}</label>
                <div class="input-group">
                    <input type="text" v-model="userName" id="login-input">
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import MessageComponent from './MessageComponent.vue'

    export default {
        name: 'ChatComponent',
        components: {
            MessageComponent,
        },
        data (){
            return{
                messageText: '',
                label_text: 'Введите логин',
                userName: '',
                input_holder: 'Сообщение',
                messages: [],
                maxIdMsg: 0
            }
        },
        mounted() {
            if (localStorage.getItem('messages')) {
                try {
                    this.messages = JSON.parse(localStorage.getItem('messages'));
                } catch(e) {
                    localStorage.removeItem('messages');
                }
            }
        },
        methods: {
            sendMessage: function(){
                if (this.messageText.length > 0 && this.messageText.trim() != '' && this.userName.length > 0 && this.messageText.trim() != ''){
                    let clearText = ''
                    let is_not_prob = false
                    for (let i = 0; i < this.messageText.length; i++){
                        if (this.messageText[i] != ' '){
                            is_not_prob = true
                            clearText += this.messageText[i]
                            continue
                        }
                        if (is_not_prob){
                            clearText += this.messageText[i]
                        }
                    }
                    this.messageText = ''
                    this.maxIdMsg += 1
                    let time_h = new Date().getHours()
                    let time_m = new Date().getMinutes()
                    if (time_h < 10){
                        time_h = `0${time_h}`
                    }
                    if (time_m < 10){
                        time_m = `0${time_m}`
                    }
                    let time = `${time_h}:${time_m}`
                    let message = {id: this.maxIdMsg, author: this.userName, text: clearText, time: time}
                    this.messages.push(message)
                    this.saveMessage()
                    document.querySelector('.messages').scrollTop = 30000
                }
                else{
                    console.log('Неправильно')
                }
            },
            deleteMessage: function(id){
                for(let i = 0; i < this.messages.length;i++){
                    if (this.messages[i].id == id){
                        this.messages.splice(this.messages.indexOf(this.messages[i]), 1)
                    }
                }
                this.saveMessage()
            },
            saveMessage: function(){
                const messages_parsed = JSON.stringify(this.messages)
                localStorage.setItem('messages', messages_parsed)
            }
        }
    }
</script>

<style>
    .frame{
        position: relative;
        width: 1520px;
        height: 828px;
        background: #FAFBFF;
    }
    .right-block{
        box-sizing: border-box;
        position: absolute;
        width: 370px;
        height: 169px;
        left: 875px;
        top: 97px;
        background: #FFFFFF;
        border: 1px solid rgba(35, 44, 94, 0.21);
        box-shadow: 0px 6px 25px rgba(19, 35, 68, 0.1);
        border-radius: 8px;
    }
    .login-form{
        width: calc(100% - 30px);
        height: calc(100% - 38px);
        margin-left: 30px;
        margin-top: 38px;
    }

    .login-form label{
        font-family: 'Roboto';
        font-style: normal;
        font-weight: 400;
        font-size: 16px;
        line-height: 19px;
        color: #5E5E5E;
    }

    .login-form .input-group{
        margin-top: 6px;
    }

    .login-form input{
        box-sizing: border-box;
        width: 309.72px;
        height: 54px;
        outline: 0;
        border: 0;
        background: #FFFFFF;
        border: 1px solid #232C5E;
        border-radius: 8px;
        padding-left: 18.71px;
        padding-top: 18px;
        padding-bottom: 17px;
    }

    .left-block{
        box-sizing: border-box;
        position: absolute;
        width: 570px;
        height: 628px;
        left: 175px;
        top: 76px;
        background: #FFFFFF;
        border: 1px solid rgba(35, 44, 94, 0.21);
        box-shadow: 0px 6px 25px rgba(19, 35, 68, 0.1);
        border-radius: 8px;
    }

    .head{
        position: absolute;
        top: 0;
        width: 568px;
        height: 31px;
        background: #F5F5F8;
        border-radius: 7px 7px 0px 0px;
        border-bottom: 1px solid rgba(35, 44, 94, 0.13);
    }

    .messages{
        position: absolute;
        top: 63px;
        width: 100%;
        bottom: 125px;
        overflow: auto;
    }

    .messages::-webkit-scrollbar{
        width: 5px;
    }

    .messages::-webkit-scrollbar-thumb{
        border-radius: 5px;
        background: rgba(35, 44, 94, 0.12);
    }

    .message-send{
        position: absolute;
        width: 570px;
        height: 125px;
        bottom: 0;
        background: rgba(11, 17, 69, 0.04);
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .input-group{
        box-sizing: border-box;
        position: absolute;
        background: #FFFFFF;
        border: 1px solid rgba(35, 44, 94, 0.21);
        border-radius: 8px;
    }

    .message-send-inner{
        display: flex;
        align-items: center;
        width: 506px;
        height: 54px;
    }

    .message-send-inner input{
        width: calc(100% - 70.5px);
        height: 100%;
        border: 0;
        outline: 0;
        border-radius: 8px;
        padding-left: 18px;
        position: absolute;
        font-family: 'Roboto';
        font-style: normal;
        font-weight: 400;
        font-size: 16px;
        line-height: 19px;
        color: #222222;
    }

    .send-btn{
        width: 28px;
        height: 28px;
        display: flex;
        align-items: center;
        justify-content: center;
        position: absolute;
        right: 16.5px;
        z-index: 1;
        cursor: pointer;
    }
</style>