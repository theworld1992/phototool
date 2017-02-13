<template>
  <div id="core">
    <header>
      <a  class="file">上传图片
        <input type="file" id="file"  accept="image/png,image/jpeg"  @change="readFile($event)" >
      </a>
      <input type="text" class="save" v-model="savename" placeholder="请输入保存的文件名" v-if="download">
      <a  @click="save" :href="saveDataURI" :download="savename" class="download" v-if="download" >下载</a>
      <a class="remove" v-if="download" @click="remove">删除图片</a>
      <a v-if="download" @click="reset" class="reset">重置</a>
    </header>
    <div id="box" >
      <img :src="dataURI" id="img" >
    </div>
    <footer id="footer" v-if="download">
 <div class="swiper-container" v-if="download">
        <div class="swiper-wrapper">
            <div class="swiper-slide" style="background-image:url(/)" @click="lome">Lome</div>
            <div class="swiper-slide" style="background-image:url(https://drscdn.500px.org/photo/197858439/m%3D1170_k%3D1/a2d8681688e797c643ea16704778ab39)" @click="vintage">Vintage</div>
            <div class="swiper-slide" style="background-image:url(https://drscdn.500px.org/photo/197858439/m%3D1170_k%3D1/a2d8681688e797c643ea16704778ab39)" @click="clarity">Clarity</div>
            <div class="swiper-slide" style="background-image:url(https://drscdn.500px.org/photo/197858439/m%3D1170_k%3D1/a2d8681688e797c643ea16704778ab39)" @click="sinCity">SinCity</div>
            <div class="swiper-slide" style="background-image:url(https://drscdn.500px.org/photo/197858439/m%3D1170_k%3D1/a2d8681688e797c643ea16704778ab39)" @click="sunrise">Sunrise</div>
            <div class="swiper-slide" style="background-image:url(https://drscdn.500px.org/photo/197858439/m%3D1170_k%3D1/a2d8681688e797c643ea16704778ab39)" @click="corssProcess">CorssProcess</div>
            <div class="swiper-slide" style="background-image:url(https://drscdn.500px.org/photo/197858439/m%3D1170_k%3D1/a2d8681688e797c643ea16704778ab39)"></div>
            <div class="swiper-slide" style="background-image:url(https://drscdn.500px.org/photo/197858439/m%3D1170_k%3D1/a2d8681688e797c643ea16704778ab39)"></div>
            <div class="swiper-slide" style="background-image:url(https://drscdn.500px.org/photo/197858439/m%3D1170_k%3D1/a2d8681688e797c643ea16704778ab39)"></div>
            <div class="swiper-slide" style="background-image:url(/0)"></div>
        </div>
        <!-- Add Pagination -->
        <div class="swiper-pagination"></div>
        <div class="swiper-button-next"></div>
        <div class="swiper-button-prev"></div>
    </div>
    </footer>
  </div>
</template>

<script>

export default {
  data:function(){
    return {
      download: false,
      dataURI:'',
      hadDataURI:false,
      saveDataURI:'',
      savename:""
    }
  },
  mounted:function(){
  // 使用钩子，在创建dom时，创建swiper 
    
  },
  methods:{
    readFile:function(event){
         var file = event.target
         var fileData = file.files[0]
         if($("#canvas")){$("#canvas").remove()}
         return new Promise(function(resolve,reject){
           var reader = new FileReader()
           reader.readAsDataURL(fileData,"UTF8")
           reader.addEventListener("load",function(){
             console.log("ok")
             resolve(reader.result)
           })
         }).then(dataURI=>{
              this.dataURI = dataURI
              this.hadDataURI = true
            },rej=>{
             console.log("error") 
            }).then(res=>{           
            //将图片转换为canvas
            var canvas = document.createElement("canvas")
            $(canvas).attr({id:"canvas",width:$("#content").width(),height:$("#content").height()})
              $("#box").append($(canvas))
              var cx = $("#canvas")[0].getContext("2d")
              var img = $("#img")[0]
              cx.drawImage(img,10,10,$("#img")[0].width>800?800:$("#img")[0].width,$("#img")[0].height>600?600:$("#img")[0].height)
            this.download = true

            }).then(resolve=>{
              // 初始化Swiper
              new Swiper('.swiper-container', {
                pagination: '.swiper-pagination',
                effect: 'coverflow',
                grabCursor: true,
                nextButton: '.swiper-button-next',
                prevButton: '.swiper-button-prev',
                centeredSlides: true,
                slidesPerView: 'auto',
                loop:true,
                coverflow: {
                    rotate: 50,
                    stretch: 0,
                    depth: 100,
                    modifier: 1,
                    slideShadows : true,
                }
              })
            }) //异步结束

      },
      save:function(){
        this.saveDataURI = $("#canvas")[0].toDataURL("image/png")
      },
      remove:function(){
        this.download = false
        this.dataURI = ''
        this.hadDataURI = false
        $("#canvas").remove()
        $("#file")[0].value = ""
      },
      reset:function(){
        if($("#canvas")){$("#canvas").remove()}
        var img = $("#img")[0]
        var canvas = document.createElement("canvas")
        $(canvas).attr({id:"canvas",width:$("#content").width(),height:$("#content").height()})
        $("#box").append($(canvas))
        var cx = $("#canvas")[0].getContext("2d")
        cx.drawImage(img,10,10,$("#img")[0].width>800?800:$("#img")[0].width,$("#img")[0].height>600?600:$("#img")[0].height) 
      },
      lome:function(){
        Caman('#canvas', function () {
          this.brightness(15);
          this.exposure(15);
          this.curves("rgb", [0, 0], [200, 0], [155, 255], [255, 255]);
          this.saturation(-20);
          this.gamma(1.8);
          this.render()
        })
      },
      vintage:function(){
        Caman('#canvas', function () {
          this.greyscale();
          this.contrast(5);
          this.noise(3);
          this.sepia(100);
          this.channels({
            red: 8,
            blue: 2,
            green: 4
          });
          this.gamma(0.87);
          this.render()
        })
      },
      clarity:function(){
        Caman('#canvas', function () {
          this.vibrance(20);
          this.curves("rgb", [5, 0], [130, 150], [190, 220], [250, 255]);
          // this.sharpen(15);
          // this.vignette("45%", 20);
          this.greyscale();
          this.contrast(4)
          this.render()
        })
      },
      sinCity:function(){
        Caman('#canvas', function () {
          this.contrast(30);
          this.brightness(15);
          this.exposure(10);
          // this.posterize(80);
          this.clip(30);
          this.render()
        })
      },
      sunrise:function(){
        Caman('#canvas', function () {
          this.exposure(3.5);
          this.saturation(-5);
          this.vibrance(50);
          this.sepia(60);
          this.colorize("#e87b22", 10);
          this.channels({
            red: 8,
            blue: 8
          });
          this.contrast(5);
          this.gamma(1.2);
          this.render()
        })
      },
      corssProcess:function(){
        Caman('#canvas', function () {
          this.exposure(5);
          this.colorize("#e87b22", 4);
          this.sepia(20);
          this.channels({
            blue: 8,
            red: 3
          });
          this.curves("b", [0, 0], [100, 150], [180, 180], [255, 255]);
          this.contrast(15);
          this.vibrance(75);
          this.render()
        })
      }

  }
}



    // var swiper = new Swiper('.swiper-container', {
    //     pagination: '.swiper-pagination',
    //     effect: 'coverflow',
    //     grabCursor: true,
    //     centeredSlides: true,
    //     slidesPerView: 'auto',
    //     coverflow: {
    //         rotate: 50,
    //         stretch: 0,
    //         depth: 100,
    //         modifier: 1,
    //         slideShadows : true
    //     }
    // });





</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    #core {
      height: 100%;
      display: flex;
      flex-direction: column;
    }
    #box {
      width: 100%;
      height: 74%;
      display: flex;
    }
    #img {
      width: 400px;
      display: none;
    }
    header {
      display: flex;
      justify-content: flex-start;
      width: 100%;
      height: 30px;
      border-bottom: 2px solid rgb(209,209,209);
      padding: 10px;
      border-radius: 5px;
    }
    .file {
      position: relative;
      display: inline-block;
      background: rgb(72, 159, 223);
      border: 1px solid #99D3F5;
      border-radius: 4px;
      padding: 4px 12px;
      overflow: hidden;
      color: #FFF;
      text-decoration: none;
      text-indent: 0;
      line-height: 20px;
  }
  .file input {
      position: absolute;
      font-size: 100px;
      right: 0;
      top: 0;
      opacity: 0;
      cursor: pointer;
  }
  .file:hover,.download:hover,.remove:hover,.reset:hover {
      border-color: #78C3F3;
      color: #ff6700;
      text-decoration: none;
      cursor: pointer;
  }
  .download,.remove,.reset,.save{
      display: inline-block;
      background: rgb(72, 159, 223);
      border: 1px solid #99D3F5;
      border-radius: 4px;
      padding: 4px 12px;
      overflow: hidden;
      color: #FFF;
      text-decoration: none;
      text-indent: 0;
      line-height: 20px;
      margin-left: 10px;
  }
  .save {
    outline: none;
  }
  #footer {
    /*background-color: green;*/
    width: 100%;
    height: 20%;
    border-top: 5px solid rgb(222,222,222);
  }


  /*swiper样式*/
    .swiper-container {
        width: 100%;
    }
    .swiper-slide {
        background-position: center;
        background-size: cover;
        width: 200px;
        height: 130px;
    }
</style>
