<template>
    <div class="sidebar">
        <div class="sidebar-main">
            <div class="sidebar-main-wrap-logo">
                <div class="sidebar-main-logo">
                    <a href="/" class="sidebar-logo__link">
                        <img src="../../assets/images/logo.svg" alt="">
                    </a>
                </div>

                <div @click="openMenu" class="sidebar-main-mobile__menu">
                    <span :class="{'opened': opened}" class="sidebar-main-mobile__menu-span span_first"></span>
                    <span :class="{'opened': opened}" class="sidebar-main-mobile__menu-span span_middle"></span>
                    <span :class="{'opened': opened}" class="sidebar-main-mobile__menu-span span_last"></span>
                </div>

                <div ref="mobile_menu" :class="{'opened': opened}" class="mobile-menu">
                    <menuPanel @openedChild="openChildMenu" :panel-body="true">
                        <template v-slot:header>Мой кабинет</template>
                        <template v-slot:body>
                            <ul class="sidebar-main__ul">
                                <li class="sidebar-main__li">Test link 1</li>
                                <li class="sidebar-main__li">Test link 2</li>
                                <li class="sidebar-main__li">Test link 3</li>
                            </ul>
                        </template>
                    </menuPanel>
                    <menuPanel @openedChild="openChildMenu" :panel-body="true">
                        <template v-slot:header>Обучение</template>
                        <template v-slot:body>
                            <ul class="sidebar-main__ul">
                                <li class="sidebar-main__li">Семинары и курсы</li>
                                <li class="sidebar-main__li">Вебинары</li>
                                <li class="sidebar-main__li">Самообучение</li>
                                <li class="sidebar-main__li">Тьютор</li>
                            </ul>
                        </template>
                    </menuPanel>
                    <menuPanel>
                        <template v-slot:header>Чат</template>
                    </menuPanel>
                    <menuPanel>
                        <template v-slot:header>Конкурсы</template>
                    </menuPanel>
                    <menuPanel>
                        <template v-slot:header>Онлайн преподавание</template>
                    </menuPanel>
                    <menuPanel>
                        <template v-slot:header>Маркет</template>
                    </menuPanel>
                    <menuPanel>
                        <template v-slot:header>Правила</template>
                    </menuPanel>
                    <menuPanel>
                        <template v-slot:header>Представители</template>
                    </menuPanel>
                </div>
            </div>

            <div class="sidebar-menu-desktop">
                <menuPanel :panel-body="true">
                    <template v-slot:header>Мой кабинет</template>
                    <template v-slot:body>
                        <ul class="sidebar-main__ul">
                            <li class="sidebar-main__li">Test link 1</li>
                            <li class="sidebar-main__li">Test link 2</li>
                            <li class="sidebar-main__li">Test link 3</li>
                        </ul>
                    </template>
                </menuPanel>
                <menuPanel :panel-body="true">
                    <template v-slot:header>Обучение</template>
                    <template v-slot:body>
                        <ul class="sidebar-main__ul">
                            <li class="sidebar-main__li">Семинары и курсы</li>
                            <li class="sidebar-main__li">Вебинары</li>
                            <li class="sidebar-main__li">Самообучение</li>
                            <li class="sidebar-main__li">Тьютор</li>
                        </ul>
                    </template>
                </menuPanel>
                <menuPanel>
                    <template v-slot:header>Чат</template>
                </menuPanel>
                <menuPanel>
                    <template v-slot:header>Конкурсы</template>
                </menuPanel>
                <menuPanel>
                    <template v-slot:header>Онлайн преподавание</template>
                </menuPanel>
                <menuPanel>
                    <template v-slot:header>Маркет</template>
                </menuPanel>
                <menuPanel>
                    <template v-slot:header>Правила</template>
                </menuPanel>
                <menuPanel>
                    <template v-slot:header>Представители</template>
                </menuPanel>
            </div>

        </div>

        <div class="sidebar-footer">
            <div class="sidebar-footer-image">
                <img src="../../assets/images/photo.jpg" alt="">
            </div>
            <div class="sidebar-footer-content">
                <h5 class="sidebar-footer-content__name">Екатерина Иванова</h5>
                <button class="sidebar-footer-content__btn">2 458 ⌘</button>
            </div>
        </div>
    </div>
</template>

<script>
import menuPanel from "@/components/sidebar/menuPanel";

export default {
    name: "sidebar",
    components: {
        menuPanel,
    },
    data() {
        return {
            opened: false,
            heightMenu: 0,
            menu: null
        }
    },
    methods: {
        openMenu() {
            // let menu = this.$refs.mobile_menu
            this.opened = !this.opened
            if(this.opened) {
                this.heightMenu = this.menu.scrollHeight + 64
                this.menu.style.height = this.heightMenu + 'px'
            } else {
                this.menu.style.height = 0
            }
        },
        openChildMenu(val) {
            if(val) {
                this.menu.style.height = this.heightMenu + val + 'px'
            } else {
                this.menu.style.height = this.heightMenu + val + 'px'
            }
        }
    },
    mounted() {
        this.menu = this.$refs.mobile_menu
    }
}
</script>

<style lang="scss" scoped>
.sidebar {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    background: #F5F5F5;
    height: 100%;

    &-main {
        padding: 1.5rem 3rem 2rem 2rem;

        &-wrap-logo {
            position: relative;
            display: flex;
            justify-content: space-between;
            align-items: center;
            .mobile-menu {
                position: absolute;
                background: #F5F5F5;
                display: none;
                width: 300px;
                padding: 0 2rem;
                top: 100%;
                right: 0;
                box-shadow: 0px 6px 8px rgba(0, 0, 0, 0.2);
                overflow: hidden;
                z-index: -1;
                height: 0;
                transition: 0.3s;
                &.opened {
                    padding: 2rem;
                    z-index: 5;
                }
            }
        }

        &-mobile__menu {
            display: none;
            flex-direction: column;
            justify-content: space-between;
            height: 12px;

            &-span {
                background: #000000;
                width: 18px;
                height: 2px;
                transition: 0.2s;
            }
            .span_first,
            .span_last {
                transition: 0.5s;
            }
            .span_first.opened {
                transform: rotate(-45deg) translate(-4px, 4px);
            }
            .span_middle.opened {
                width: 0;
            }
            .span_last.opened {
                transform: rotate(45deg) translate(-3px, -3px);
            }
        }

        &-logo {
            margin-bottom: 1.75rem;

            img {
                width: 100%;
            }
        }

        &__ul {
            margin-bottom: 0.5rem;
        }

        &__li {
            padding: 0.25rem 0 0.25rem 3.5rem;
            font-size: 1rem;
            line-height: 1.5rem;
            cursor: pointer;

            &:hover {
                background: #FACB64;
            }
        }
    }

    &-footer {
        display: flex;
        align-items: center;
        border-top: 2px solid #dadada;
        padding: 1rem 2rem;

        &-image {
            width: 48px;
            height: 48px;
            border-radius: 8px;
            margin-right: 0.5rem;
            overflow: hidden;

            img {
                width: 100%;
            }
        }

        &-content {
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            align-items: flex-start;

            &__name {
                font-size: 0.875rem;
                line-height: 1rem;
                margin-bottom: 0.5rem;
            }

            &__btn {
                font-size: 0.75rem;
                line-height: 1rem;
                padding: 0.25rem 0.5rem;
                background: #FACB64;
                border-radius: 8px;
            }
        }
    }
}
@media (max-width: 1200px) {
    .sidebar-main {
        padding-right: 2rem;
    }
}

@media (max-width: 992px) {
    .sidebar {
        background: #fff;

        &-menu-desktop {
            display: none;
        }

        &-main {
            padding: 1.5rem 2rem;
            .mobile-menu {
                display: block;

            }
            &-mobile__menu {
                display: flex;
                cursor: pointer;
                transition: 0.2s;

                &:hover {
                    transform: scale(1.2);
                }
            }

            &-logo {
                max-width: 220px;
                margin: 0;
            }
        }
    }
    .sidebar-footer {
        display: none;
    }
}

@media (max-width: 576px) {
    .sidebar-main {
        padding: 1.5rem 1rem;

        &-logo {
            width: 50%;
        }
    }
}
</style>