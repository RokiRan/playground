<script setup lang="ts">
interface Test {
  name: string
  age: number
}
const person: Test = {
  name: 'Jack',
  age: 18,
}
Object.keys(person).forEach((key) => {
  console.log((<any>person)[key])
})
</script>

<template>
  <div>
    <h3>CSS技巧</h3>
    <section class="btnClass">
      <h4>旋转效果</h4>
      <button>
        <a href="#">Button</a>
      </button>
    </section>
  </div>
</template>

<style scoped lang="less">
.btnClass3{
    button{
        background-color: #182848;
        padding: 2rem 3rem;
        margin: 0;
        box-sizing: border-box;
        a{
            text-decoration: none;
            font-size: clamp(1.5rem, 2.5vw,2.5rem);
            background: linear-gradient(-45deg,#ff00c1,#00fff9);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transform;
        }
    }
    button::after,button::before{
        content: "";
        position: absolute;
        background: linear-gradient(
            var(--rotate),
            #ff00c1 0%,
            #9600ff 25%,
            #4900ff 50%,
            #00b8ff 80%,
            #00fff9 100%
        );
        width: 105%;
        height: 110%;
        left: -2.5%;
        top: -5%;
        border-radius: 10px;
        z-index: -1;
        transition: --rotate 9999s linear;
    }
    button:hover::after,button:hover::before{
        --rotate: 36000deg;
        transition:  --rotate 20s linear;
    }
    button:hover::before{
        animation: fade 1.2s;
    }
    @property --rotate{
        syntax: "<angle>";
        inital-value: 130deg;
        inherits: false;
    }
    @keyframes fade {
        0%{
            opacity: 1;
            transform: scale(1);
            filter: blur(10px);
        }
        100%{
            opacity: 0;
            transform: scale(1.4);
            filter: blur(10px);
        }
    }
}
*,
*::after,
*::before{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
// body{
//     width: 100%;
//     min-height: 100vh;
//     color: #efe;
//     background: #182848;
//     display: flex;
//     justify-content: center;
//     align-items: center;
// }
button{
    border: none;
    position: relative;
    border-radius: 10px;
    cursor: pointer;
    background: #182848;
    padding: 2em 4em;
    font-family: sans-serif;
}
a{
    text-decoration: none; // 文字装饰
    font-size: clamp(1.5rem, 2.5vw, 2.5rem);
    background: linear-gradient(-45deg, #ff00c1, #00fff9);
    background-clip: text;
    color: transparent;
    -webkit-background-clip: text; //  设置元素的背景（背景图片或颜色）是否延伸到边框、内边距盒子、内容盒子下面。
    // -webkit-text-fill-color: transparent; // 非标准属性 不建议使用
}
button::after,
button::before{
    content: '';
    position: absolute;
    background: linear-gradient(
        var(--rotate),
        #ff00c1 0%,
        #9600ff 25%,
        #4900ff 50%,
        #00b8ff 80%,
        #00fff9 100%
    );
    width: 105%;
    height: 110%;
    left: -2.5%;
    top: -5%;
    border-radius: 10px;
    z-index: -1;
    transition: --rotate 9999s linear;
}
button:hover::after,
button:hover::before{
    --rotate: 3600deg;
    transition: --rotate 20s linear;
}
button:hover::before{
    animation: fade 1.2s;
}
@property --rotate{
    syntax: '<angle>';
    initial-value: 130deg;
    inherits: false;
}
@keyframes fade{
    0%{
        opacity: 1;
        transform: scale(1);
        filter: blur(10px);
    }
    100%{
        opacity: 0;
        transform: scale(1.4);
        filter: blur(10px);
    }
}
</style>
