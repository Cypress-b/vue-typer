<template>
  <div class="typer-wrapper">
    <div class="typer">
      <div class="typer-content">
        <p class="typer-static">I'm&nbsp;</p>
        <p class="typer-dynamic">
          <span class="cut">
            <span class="word" v-for="(letter,index) in words" :key="index">{{letter}}</span>
          </span>
          <span class="typer-cursor"></span>
        </p>
      </div>
    </div>

    
    
  </div>
</template>

<script>
export default {
  data () {
    return {
      words:[],
      letters:[],
      str:"By Punk",
      order:1,
    }
  },
  watch:{
    order(old,newV){
      if(this.order%4==1){
        this.str="By Punk!"
      }
      else if(this.order%4==2){
        this.str="looking for a job. "
      }
      else if(this.order%4==3){
        this.str="a front-end programmer."
      }
      else{
        this.str="coding the web..."
      }
      
    }
  },
  mounted(){
    this.begin()
  },
  methods:{
    begin(){
      this.letters=this.str.split("")
      for(var i=0;i<this.letters.length;i++){
        setTimeout(this.write(i),i*100);
      }
    },
    back(){
      let L=this.letters.length;
      for(var i=0;i<L;i++){
        setTimeout(this.wipe(i),i*50);
      }
    },
    write(i){
      return ()=>{
          let L=this.letters.length;
          this.words.push(this.letters[i]);
          let that=this;
          if(i==L-1){
            setTimeout(function(){
              that.back();
            },500);
            
          }
      }
    },
    wipe(i){
      return ()=>{
          this.words.pop(this.letters[i]);
          if(this.words.length==0){
             this.order++;
             let that=this;
             setTimeout(function(){
               that.begin();
             },300);
             
          }
      }
    },

  },
}
</script>

<style scoped>
*{margin: 0}
div{margin: 0}
.typer-wrapper{
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  background-color: #000;
  color: #fff;
  font-family: "微软雅黑";
  margin: 0;
  padding: 0;
  padding-left: 100px;
  box-sizing: border-box;
}
.typer{
  margin-top: 2%;
  box-sizing: border-box;
}
.typer .typer-content{
  font-weight: bold;
  font-size: 50px;
  display: flex;
  flex-direction: row;
  letter-spacing: 2px
}
.typer-dynamic{
  position: relative;
}
.cut{
  color: #e84d49;
}
.typer-cursor{
  position: absolute;
  height: 100%;
  width: 3px;
  top: 0;
  right: -10px;
  background-color: #e84d49;
  animation: flash 1.5s linear infinite;
}
</style>
