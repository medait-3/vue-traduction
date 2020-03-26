<template>  
  <div id="app">
    <h1 style="color: green">Translate Online</h1>
  
    <TranslateForm v-on:formSubmit="textTranslate"></TranslateForm>
    <br>
    <TranslateOutput style="border: 1px solid green;width:40%;padding: 1%;margin-left: 30%" v-text="translatedText"></TranslateOutput>
  </div>
</template>

<script>
import TranslateForm from './components/TranslateForm'
import TranslateOutput from './components/TranslateOutput'
export default {
  name: 'App',
  data:function(){
    return {
      translatedText:''
    }
  },
  components:{
    TranslateForm,
    TranslateOutput
  },
  methods:{
    textTranslate: function(text, language){
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20191023T041315Z.38a463b02eff9e3d.662f966205410571b5e42f58d43c13d6f138ef22&lang='+language+'&text='+text).then((res)=>{
        this.translatedText = res.body['text'][0];
      });
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#app h1{
  position: relative;
  text-align: center;
  padding-bottom: 30px;
}
#app h1::before{
    position: absolute;
    content: '';
    background: #cccccc;
    width: 130px;
    height: 2px;
    left: 0px;
    bottom: 0px;
    left: 50%;
    -webkit-transform: translateX(-50%);
    -ms-transform: translateX(-50%);
    transform: translateX(-50%);
}
#app h1::after{
    position: absolute;
    content: '';
    background: #336699;
    width: 45px;
    width: 45px;
    height: 8px;
    left: 0px;
    bottom: -3px;
    -webkit-mask-image: -webkit-linear-gradient(165deg, rgba(244, 55, 55, 0.6) 50%, #f43737 50%, #000000 70%);
    -webkit-mask-size: 200%;
    -webkit-animation: shine 2s linear infinite;
    animation: shine 2s linear infinite;
    left: 50%;
    -webkit-transform: translateX(-50%);
    -ms-transform: translateX(-50%);
    transform: translateX(-50%);
}

@-webkit-keyframes shine {
  from {
    -webkit-mask-position: 150%;
  }
  
  to {
    -webkit-mask-position: -50%;
  }
}

</style>
