<script lang='ts' setup>
import { ref, onMounted, reactive } from 'vue'
import { Application } from '@splinetool/runtime';
import { gsap } from 'gsap/dist/gsap';
import { SplitText } from 'gsap/SplitText';

// template ref
const canvas = ref(null)
const readyRender = ref(false);

// spline state
const state = reactive({
    spline: {
        scene: "https://prod.spline.design/fxCt6CZRd9RCliBZ/scene.splinecode",
        app: null,
        isLoaded: false,
    },
});

onMounted(async () => {
    // const app = new Application(canvas.value);
    // await app.load(state.spline.scene)
    // state.spline.app = app;
    // state.spline.isLoaded = true;
    gsap.to(".box", {
        x: 200,
        rotation: 360,
        duration: 3
    });
    gsap.registerPlugin(SplitText);
    let split = SplitText.create(".text", {
        type: "words"
    });
    gsap.from(split.words, {
        y: 100,
        autoAlpha: 0,
        stagger: 0.05
    })
})
</script>

<template>
    <div class="Container">
        <div class="tag-box">
            <div class="tag">This is a test!</div>
        </div>
        <h1 class="text">{{ "Tutorial APP" }}</h1>
        <!-- <canvas ref="canvas"></canvas> -->
        <div class="box graident-green"></div>
    </div>
</template>

<style lang='less' scoped>
.Container {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    padding: 24px;
    min-height: calc(100vh - 86.4px);
}

.image-gradient {
    position: absolute;
    top: 0;
    right: 0;
    opacity: 0.5;
}

.layer-blur {
    height: 0;
    width: 30rem;
    position: absolute;
    top: 20%;
    right: 20%;
    box-shadow: 0 0 700px 1;
    rotate: -30deg;
}

.tag-box {
    position: relative;
    width: 20rem;
    height: 3rem;
    border-radius: 50px;
    border-radius: 50px;
    background: linear-gradient(to right, #fff, #7f42a7, #6600c5, #5300a0, #fff);
    background-size: 200%;
    animation: animationGradient 2.5s linear infinite;
    box-shadow: var(--boxShadow-light);
}

@keyframes animationGradient {
    to {
        background-position: 200%;
    }
}

.box {
    width: 30px;
    height: 30px;
    background: #000;
}

.tag-box .tag {
    position: absolute;
    inset: 5px;
    background-color: #000;
    border-radius: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: 0.5s ease;
    cursor: pointer;
}

.tag {
    color: #fff;
}

.tag-box .tag:hover {
    color: #9851da;
}
</style>