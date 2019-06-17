<template>
  <div>
    <p>vw:容器适配/文本的适配/大于1px的边框、圆角、阴影/内距和外距</p>
    <div class="box">
      居中文字
    </div>
    <div class="box1 ignore">
      居中文字
    </div>
    <p>postcss-aspect-ratio-mini 处理元素容器宽高比</p>
    <div aspectratio class="box2">
        <div aspectratio-content>
          内容
        </div>
    </div>
    <p>
      postcss-write-svg插件<br/>
      主要用来处理移动端1px的解决方案。<br/>
      该插件主要使用的是border-image和background来做1px的相关处理。</p>
    <div class="box3"></div>
    <div class="box4"></div>
    <p>CSS Modules <a href="https://github.com/css-modules/css-modules">github</a><a href="https://github.com/css-modules/css-modules">github</a></p>
    <div class="box" :class="$style.red">
      居中文字
    </div>
    <p>cssnext <a href="https://cssnext.github.io/features/#automatic-vendor-prefixes">github</a></p>
    <div class="box5">
       <a href="https://cssnext.github.io/features/#automatic-vendor-prefixes">github</a>
    </div>
    <div class="box6">
      居中文字
    </div>
    <div class="box7">
       居中文字
    </div>
  </div>
</template>

<script>
import {className} from './style.css'
export default {
  created () {
    console.log(this.$style)
    // -> "red_1VyoJ-uZ"
    // an identifier generated based on filename and className.
  },
  mounted () {
    console.log(className)
  }
}
</script>
<style module>
.red {
  color: red;
}
</style>
<style scoped>
  /* 但是content也会引起一定的副作用。比如img和伪元素::before(:before)或::after（:after）。在img中content会引起部分浏览器下，图片不会显示 */
  img {
      content: normal !important;
  }

  body{
    text-align: center;
  }
  .box{
    width: 200px;
    height: 100px;
    text-align: center;
    line-height: 100px;
    font-size: 25px;
    margin: 0 auto 10px;
    background: #ccc;
  }
  .box1.ignore {
    width: 200px;
    height: 100px;
    text-align: center;
    line-height: 100px;
    font-size: 25px;
    margin: 0 auto 10px;
    background: #ccc;
  }

  [aspectratio] {
      position: relative;
  }
  [aspectratio]::before {
      content: '';
      display: block;
      width: 1px;
      margin-left: -1px;
      height: 0;
  }

  [aspectratio-content] {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      width: 100%;
      height: 100%;
  }

  .box2{
    margin: 0 auto 10px;
    width: 188px;
    background: #ccc;
  }
  /* aspect-ratio属性不能和其他属性写在一起，否则编译出来的属性只会留下aspect-ratio的值  */
  .box2{
    aspect-ratio: '4:3';
  }

  /* border-image 支持度不够友好 */
  @svg 1px-border {
      height: 2px;
      @rect {
          fill: var(--color, black);
          width: 100%;
          height: 50%;
      }
  }
  .box3{
    margin: 20px auto;
     border: 1px solid transparent;
    border-image: svg(1px-border param(--color #00b1ff)) 2 2 stretch;
  }
  @svg square {
      @rect {
          fill: var(--color, black);
          width: 100%;
          height: 100%;
      }
  }
  .box4{
    margin: 20px auto;
    height: 1px;
    background: white svg(square param(--color #00b1ff));
  }

  :root {
    --mainColor: red;
    --danger-theme: {
      color: white;
      background-color: red;
    }
    --fontSize: 1rem;
  }

  .box5 a {
    color: var(--mainColor);
  }
  .box6 {
    width: 200px;
    height: 100px;
    text-align: center;
    line-height: 100px;
    font-size: 25px;
    margin: 0 auto 10px;

    @apply --danger-theme;
  }
  .box7{
    font-size: calc(var(--fontSize) * 2);
  }

  @custom-media --only-medium-screen (width >= 500px) and (width <= 1200px);
  @media (--only-medium-screen) {
    body{
      background: red;
    }
  }
</style>
