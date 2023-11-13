<template>
  <div>
    <div class="chatBox">
      <div v-for="(chat, i) in chatLists" :key="symbol(i)">
        <userchatbox>
          {{ chat.request }}
        </userchatbox>
        <responsechatbox>
          <li v-for="(item, index) in chat.response" :key="chat.response">
            {{ item }}
          </li>
        </responsechatbox>
      </div>
    </div>


    <Input @seed="getMessage" :isInput="isinput" />
    <tip :type="tipState" v-show="tipShow">
      {{ tipData }}
    </tip>
  </div>
</template>
<style scoped></style>

<script setup>
import axios from 'axios'
import userchatbox from './components/userchatbox.vue';
import responsechatbox from './components/responsechatbox.vue';
import Input from './components/input.vue'
import tip from './components/tip.vue'
import { reactive, ref, watch } from 'vue';


//聊天框数据
const chatLists = reactive([{ 'request': '孙悟空', 'response': ["1.《孙悟空：无尽的英雄传说》", "2.《猴王》", "3.《猿王传》"] }])

//是否允许输入
const isinput = ref(true)

//tip是否展示
const tipShow = ref(false)
const tipState = ref('')
//报错信息
const tipData = ref('')

//将message发送到api并获取返回的数据
axios.defaults.timeout = 5000;
const getMessage = (data) => {
  //字符小于6才发送请求
  if (data.length < 6) {
    //在发送数据时，禁止再次发送数据
    isinput.value = false

    //保存聊天框中一组数据的request
    let chat = reactive({ "request": data, 'response': [] })
    let text = reactive([]) //暂时存储response的数据
    chatLists.push(chat)
    //记录访问次数
    let __try = 0;

    //每2000ms访问一次，获取数据
    let getData
    getData = setInterval(() => {
      axios.post('https://wm-interview.onrender.com/send', { message: data }).then(function (response) {
        var list = response.data.content
        if (list !== 'undefined') {
          text.push(`${chat.response.length + 1}.${list}`)
          chat['response'].push('')
        }
        //得到3次数据则停止访问
        if (chat.response.length >= 3) {
          console.log("over");
          //允许再次输入数据
          isinput.value = true
          clearInterval(getData)
        }
      }).catch(function (e) {
        //捕获429和500异常
        if (e.message.includes('429') || e.message.includes('500')) {
          __try++
          console.log(__try);
        }
      })

      //访问次数过多则获取失败
      if (__try >= 10) {
        console.log('网络或服务器异常');
        tipState.value = 'error'
        tipData.value = '网络或服务器异常,请重新发起请求'
        tipShow.value = true
        setTimeout(() => tipShow.value = false, 2000)
        isinput.value = true
        //若chat中没有一条数据，则删除最后一条
        if (chat.response.length === 0) {
          chatLists.splice(chatLists.length - 1, 1)
        }
        clearInterval(getData)
      }
    }, 2000)

    watch(() => chat.response.length, val => {
      //模拟 /chat 的数据
      /**
       * 模拟打字机数据
       * @param {String} context 
       */
      const addTxt = function (context) {
        let i = 0;
        let interval;
        let str = ""
        if (i > context.length) {
          clearInterval(interval);
        } else {
          interval = setInterval(() => {
            i++;
            str = context.substring(0, i);
            if (i >= context.length) {
              chatLists[chatLists.length - 1].response[val - 1] = str
              clearInterval(interval)
            } else {
              chatLists[chatLists.length - 1].response[val - 1] = str
            }
          }, 100)
        }
      }
      
      addTxt(text[val - 1])
    })
  }
  else {
    tipState.value = 'error'
    tipData.value = '不得输入大于等于6个字符'
    tipShow.value = true
    setTimeout(() => tipShow.value = false, 2000)
  }
}
const symbol = (i) => Symbol(i)
</script>

<style scoped>
li {
  list-style-type: none;
}
</style>
<style>
body {
  padding: 0;
  margin: 0;
}
:root{
  --userBac:#00AAFF;
  --shadow:#ccc;
  --response:#26b100;
}
html {
  margin-bottom: 4vh;
}
</style>