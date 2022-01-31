<template>
    <div class="panel">
        <a @click="openedBody" href="#" class="panel__link">
            <slot name="header"></slot>
            <img v-if="panelBody" src="../../assets/images/icons/arrow-next.svg" alt="" :class="{'opened': opened}" class="icon__arrow">
        </a>
        <div ref="panelBody" v-if="panelBody" class="panel-body">
            <slot name="body"></slot>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        panelBody: {
            type: Boolean,
            default: false
        }  
    },
    name: "menuPanel",
    data() {
        return {
            opened: false,
        }
    },
    methods: {
        openedBody() {
            let body = this.$refs.panelBody
            let heightBody = body.scrollHeight
            if(this.panelBody && !this.opened) {
                this.opened = true
                body.style.height = heightBody + 'px'
            } else {
                this.opened = false
                heightBody = 0
                body ? body.style.height = 0 : false
            }
            this.$emit('openedChild', heightBody)
        },
    },
}
</script>

<style lang="scss" scoped>
.panel {
    &__link {
        display: flex;
        justify-content: space-between;
        font-size: 1rem;
        line-height: 1.5rem;
        font-family: 'Inter-Bold', sans-serif;
        color: #191919;
        margin-bottom: 0.5rem;
        &:last-child {
            margin-bottom: 0;
        }
        .icon__arrow {
            transition: 0.2s;
            &.opened {
                transform: rotate(90deg);
            }
        }
    }
    &-body {
        margin-left: -2rem;
        margin-right: -3rem;
        height: 0;
        overflow: hidden;
        transition: 0.2s;
    }
}
@media (max-width: 1200px) {
    .panel-body {
        margin-right: -2rem;
    }
}
</style>