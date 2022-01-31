<template>
    <div v-if="cardsData && typeCard" :class="typeCard" class="card">
        <div class="card-content">
            <h3 class="card-content-title">{{ cardsData.title }}</h3>
            <p class="card-content__type card__prgf">
                <span class="icon__type"></span>
                {{ cardsData.type }}
            </p>
            <p v-if="cardsData.duration" class="card-content__duration card__prgf">
                <span class="icon__time"></span>
                {{ cardsData.duration }}
            </p>
            <p class="card-content__start card__prgf">
                <span class="icon__calendar"></span>
                Сессия
                {{ setDate(cardsData.dateStart) }}
            </p>

            <p class="card-content-description">{{ cardsData.description }}</p>
            <p v-for="(curator, key) in cardsData.curators" :key="'c' + key" class="card-content-description">
                Куратор:
                <span v-if="curator">{{ curator }}</span>
            </p>
            <p v-for="(methodist, key) in cardsData.methodists" :key="'m' + key" class="card-content-description">
                Методист:
                <span v-if="methodist">{{ methodist }}</span>
            </p>
        </div>

        <a v-if="cardsData.price"
           :href="cardsData.link"
           target="_blank"
           class="card-btn">
            {{ cardsData.price }} ₽
        </a>
        <a v-else
           :href="cardsData.link"
           target="_blank" class="card-btn">Выбрать тариф</a>
    </div>
</template>
<!--dateStart: "2022-12-24"-->
<!--description: ""-->
<!--id: 6-->
<!--link: "/seminars/6"-->
<!--price: 12499-->
<!--title: "I Can Sing"-->
<!--type: "seminar"-->

<script>
import moment from "moment";

export default {
    props: {
        cardsData: Object,
        typeCard: {
            type: String,
            default: ''
        },
    },
    name: "card",
    data() {
        return {

        }
    },
    methods: {
        setDate(date) {
            if(moment(date) !== 'Invalid date') {
                return moment(date).format('DD MMMM')
            } else {
                return date
            }
        },
    },
    computed: {

    },
    mounted() {

    },
    filters: {

    }
}
</script>

<style lang="scss" scoped>
$radiusCard: 8px;
$shadowCard: 0px 6px 8px rgba(0, 0, 0, 0.03);
$borderCard: 1px solid #EDEDED;
$padding: 20px 16px 16px;
$fontSize: 1.125rem;
$lineHeight: 1.5rem;
$heightCard: 320px;
@mixin maskSettings {
    mask-size: cover;
    -webkit-mask-size: cover;
    mask-position: center;
    -webkit-mask-position: center;
}
@mixin maskUrl($url) {
    -webkit-mask-image: url('../../../src/assets/images/icons/' + $url);
    mask-image: url('../../../src/assets/images/icons/' + $url);
}

.card {
    display: flex;
    flex-direction: column;
    justify-content: space-between;

    background-color: #fff;
    -webkit-border-radius: $radiusCard;
    -moz-border-radius: $radiusCard;
    border-radius: $radiusCard;
    box-shadow: $shadowCard;
    border: $borderCard;
    padding: $padding;
    min-height: $heightCard;
    margin-bottom: 1.5rem;
    width: calc(25% - 1rem);
    &-content {
        font-size: 0.875rem;
        &-title {
            font-size: $fontSize;
            line-height: $lineHeight;
            margin-bottom: 0.25rem;
        }
        .icon__type,
        .icon__time,
        .icon__calendar {
            width: 12px;
            height: 12px;
            @include maskSettings;
            margin-right: 0.625rem;
        }
        .icon__type {
            @include maskUrl('icon-traning.svg');
        }
        .icon__time {
            @include maskUrl('icon-time.svg');
            background: #C4C4C4;
            width: 13px;
            height: 13px;
        }
        .icon__calendar {
            @include maskUrl('icon-calendar.svg');
            background: #C4C4C4;
            height: 13px;
        }
        &-description {
            margin-top: 0.5rem;
            font-size: 0.75rem;
        }
    }
    &.seminar {
        .icon__type {
            background: #FBAD00;
        }
        .card-btn {
            background: #FBAD00;
            &:hover {
                background: darken(#FBAD00, 10%);
            }
        }
    }
    &.training {
        .icon__type {
            background: #007FF4;
        }
        .card-btn {
            background: #007FF4;
            &:hover {
                background: darken(#007FF4, 10%);
            }
        }
    }
    &__prgf {
        display: flex;
        text-transform: capitalize;
        align-items: center;
        margin-bottom: 0.25rem;
    }
    &-btn {
        font-family: 'Inter-Bold', sans-serif;
        padding: 0.5rem 1rem;
        font-size: 0.875rem;
        -webkit-border-radius: 8px;
        -moz-border-radius: 8px;
        border-radius: 8px;
        cursor: pointer;
        display: inline-block;
        margin-left: auto;
        color: #fff;
    }
}
@media (max-width: 1360px) {
    .card {
        width: 30%;
        max-width: 290px;
    }
}
@media (max-width: 1200px) {
    .card {
        width: 100%;
    }
}
@media (max-width: 992px) {
    .card {
        width: 32%;
        margin-right: 0;
    }
}
@media (max-width: 768px) {
    .card {
        width: 48%;
    }
}
@media (max-width: 576px) {
    .card {
        width: 100%;
    }
}
</style>