<template>
    <div v-if="author" class="author">
        <div class="author-content-desktop">
            <div class="author-content">
                <h3 class="author-content-topic">{{ author.topic }}</h3>
                <h2 class="author-content-name">{{ author.name }}</h2>

                <p class="author-content-description">{{ author.description }}</p>
            </div>
            <div class="author-image">
                <img :src="author.avatar" alt="">
            </div>
        </div>


        <div class="author-content-mobile">
            <div class="author-content-mobile-wrap">
                <div class="wrap__text">
                    <h3 class="author-content-topic">{{ author.topic }}</h3>
                    <h2 class="author-content-name">{{ author.name }}</h2>
                </div>
                <div class="author-image">
                    <img :src="author.avatar" alt="">
                </div>
            </div>

            <p class="author-content-description">{{ author.description }}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        author: Object
    },
    name: "author",
}
</script>

<style lang="scss" scoped>
.author {
    &-content {
        margin-right: 1rem;
        &-desktop {
            display: flex;
            margin-bottom: 1.5rem;
        }
        &-mobile {
            display: none;
            margin-bottom: 1.5rem;
        }
        &-topic {
            font-size: 0.75rem;
            line-height: 1rem;
            text-transform: uppercase;
        }
        &-name {
            font-size: 1.5rem;
            line-height: 2rem;
            margin-bottom: 0.5rem;
        }
        &-description {
            font-size: 1rem;
            line-height: 1.5rem;
            max-width: 470px;
        }
    }

    &-image {
        width: 120px;
        height: 120px;
        overflow: hidden;
        -webkit-border-radius: 50%;
        -moz-border-radius: 50%;
        border-radius: 50%;
        flex-shrink: 0;
        img {
            display: block;
            width: 100%;
        }
    }
}
@media (max-width: 768px) {
    .author {
        &-content {
            &-desktop {
                display: none;
            }
            &-mobile {
                display: block;
                width: 100%;
                &-wrap {
                    display: flex;
                    justify-content: space-between;
                    margin-bottom: 0.5rem;
                }
            }
            &-topic {
                margin-bottom: 0.5rem;
            }
            &-name {
                font-size: 1.25rem;
                line-height: 1.5rem;
            }
        }
    }
}
</style>