<script setup>
import { ref } from 'vue'
import router from '../../router/router'
import 'animate.css'

const isApp = router.currentRoute.value.name.includes('app')
</script>

<template>
    <n-layout class="container">
        <n-layout-header v-if="!isApp" class="header">
            <n-flex :align="'center'" :justify="'space-between'">
                <n-flex :align="'center'" class="logo animate__animated animate__fadeInDown"
                    @click="router.push({ name: 'home' })">
                    <n-avatar :width="24" style="border-radius: 8px;"
                        src="./tutorial/logo/apple-touch-icon.png"></n-avatar>
                    <b>
                        Tutorial
                        <span class="primaryColor">App</span>
                    </b>
                </n-flex>
                <n-flex :size="24">
                    <n-button class="animate__animated animate__fadeInDown show1" text
                        @click="router.push({ name: 'mission' })">
                        Design Detail
                    </n-button>
                    <n-button class="animate__animated animate__fadeInDown show2" text
                        @click="router.push({ name: 'development' })">
                        Development History
                    </n-button>
                    <n-button class="animate__animated animate__fadeInDown show3" text
                        @click="router.push({ name: 'about' })">
                        About
                    </n-button>
                </n-flex>
            </n-flex>
        </n-layout-header>
        <router-view />
        <n-layout-footer v-if="!isApp">
            <n-flex :justify="'right'">
                <div>2024 Copyright © <span class="primaryColor">Magnet</span>. All rights reserved.</div>
            </n-flex>
        </n-layout-footer>
    </n-layout>
</template>

<style lang='less' scoped>
@import 'animate.css';

.container {
    min-height: 100vh;

    .header {
        padding: 24px;
    }

    .logo {
        font-size: 24px;
        cursor: pointer;
        transition: all 0.2s;

        &:hover {
            opacity: 0.8;
        }
    }

    .n-layout-footer {
        background: rgba(224, 224, 224, 0.2);
        padding: 24px;

        .copyright {
            color: var(--primary-color)
        }
    }
}

.show1 {
    --animate-duration: 1s;
}

.show2 {
    --animate-duration: 2s;
}

.show3 {
    --animate-duration: 3s;
}
</style>