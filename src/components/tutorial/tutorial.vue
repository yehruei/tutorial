<script lang='ts' setup>
import { ref, onMounted, reactive } from 'vue'
import { Application } from '@splinetool/runtime';
import { gsap } from 'gsap';
import {
    SplitText,
    ScrollSmoother,
    ScrollTrigger
} from 'gsap/all';

// template ref
const canvas = ref(null)
const readyRender = ref(false);
const smoother = ref(null);
const scroller = ref(null);

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
    gsap.registerPlugin(SplitText, ScrollTrigger, ScrollSmoother);

    smoother.value = ScrollSmoother.create({
        smooth: 1,
        smoothTouch: 0.1,
        effects: true,
    })

    gsap.to(".box-c", {
        scrollTrigger: {
            trigger: ".box-c",
            pin: true,
            start: "top center",
            end: "+=300",
            scrub: 3,
            markers: true,
        },
        x: "20rem",
        rotation: 360,
        duration: 3
    });

    let split = SplitText.create(".text", {
        type: "words"
    });
    gsap.from(split.words, {
        y: 100,
        autoAlpha: 0,
        stagger: 0.05
    })
})

function handleJump() {
    smoother.value.scrollTo(".box-c", true, "top center");
}
</script>

<template>
    <div class="Container">
        <div>
            <div class="tag-box">
                <div class="tag" @click="handleJump">Let's JUMP to C</div>
            </div>
            <h1 class="text">{{ "Tutorial Page" }}</h1>
            <!-- <canvas ref="canvas"></canvas> -->
            <div class="rollingBox graident-green"></div>
            <div class="box box-a color-a" data-speed="clamp(0.5)">
                <b>a</b>
            </div>
            <div class="box box-b color-b" data-speed="clamp(0.8)">
                <b>b</b>
            </div>
            <div class="box box-c color-c" data-speed="1.5">
                <b>c</b>
            </div>
        </div>
    </div>
</template>

<style lang='less' scoped>
.Container {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    padding: 24px;
    // min-height: calc(100vh - 86.4px);
    height: 4000px;
    background: black;
    background-image:
        linear-gradient(rgba(255, 255, 255, .07) 2px, transparent 2px),
        linear-gradient(90deg, rgba(255, 255, 255, .07) 2px, transparent 2px),
        linear-gradient(rgba(255, 255, 255, .06) 1px, transparent 1px),
        linear-gradient(90deg, rgba(255, 255, 255, .06) 1px, transparent 1px);
    background-size: 100px 100px, 100px 100px, 20px 20px, 20px 20px;
    background-position: -2px -2px, -2px -2px, -1px -1px, -1px -1px;
}

.text {
    color: #fff;
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

.rollingBox {
    width: 5rem;
    height: 5rem;
    background: var(--gradient-emerald-city);
    border-radius: 0.5rem;
}

.box {
    width: 5rem;
    height: 5rem;
    border-radius: 0.5rem;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 24px;
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    z-index: 100;
    line-height: 100px;
    text-align: center;
    will-change: transform;
}

.box-a {
    top: 12rem;
}

.box-b {
    top: 36rem;
}

.box-c {
    top: 72rem;
}

.color-a {
    background: var(--gradient-macha), url(/tutorial/tutorial/noise-e82662fe.png);
    background-blend-mode: color-dodge
}

.color-b {
    background: var(--gradient-summer-fair);
    background-blend-mode: color-dodge
}

.color-c {
    background: var(--gradient-lipstick), url(/tutorial/tutorial/noise-e82662fe.png);
    background-blend-mode: color-dodge
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
    color: #a56ed8;
}
</style>