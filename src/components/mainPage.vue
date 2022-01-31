<template>
    <div class="main">
        <div class="main-sidebar">
            <sidebar/>
        </div>
        <div class="main-content">
            <div class="main-content-head">
                <h1 class="main-content-title">Витрина <span>Семинары и курсы</span></h1>
                <a href="#" class="main-content__link">Моё обучение</a>
            </div>

            <author :author="data.author"/>

            <div v-if="cards" class="main-content-seminar">
                <card v-for="(card, key) in cards.seminar" :key="'s' + key"
                      :cards-data="card"
                      :type-card="'seminar'" class="card-seminar"/>
            </div>
            <div v-if="cards" class="main-content-training">
                <card v-for="(card, key) in cards.training" :key="'t' + key"
                      :cards-data="card"
                      :type-card="'training'" class="card-training"/>
            </div>
        </div>
    </div>
</template>

<script>
import sidebar from "@/components/sidebar/sidebar";
import card from "@/components/cards/card";
import author from "@/components/author";

export default {
    name: "mainPage",
    components: {
        sidebar,
        card,
        author,
    },
    data() {
        return {
            data: {},
            cards: {
                seminar: [],
                training: [],
            },
        }
    },
    methods: {
        async getData(url) {
            return fetch(url)
                .then(
                    function (res) {
                        if (res.status !== 200) {
                            // console.log(res.status);
                            return;
                        }

                        return res.json();
                    }
                )
        },
        setTypeCard() {
            this.data.seminars.forEach(item => {
                item.type === 'seminar' ? this.cards.seminar.push(item) : this.cards.training.push(item)
            })
            // console.log('cards', this.cards)
        },
    },
    async mounted() {
        const urlData = 'https://eg-cdn.s3.eu-central-1.amazonaws.com/static/fe-test/seminars-test-data.json';
        this.data = await this.getData(urlData)
        // console.log('this.data', this.data)

        this.setTypeCard()
    }
}
</script>

<style lang="scss" scoped>
.main {
    display: flex;
    &-sidebar {
        width: 25%;
        max-width: 320px;
    }
    &-content {
        padding: 32px 64px 8px 32px;
        width: 75%;
        &-head {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 2rem;
        }
        &-title {
            font-size: 2.25rem;
            line-height: 3rem;
            margin-right: 1rem;
            span {
                color: #C4C4C4;
                display: inline-block;
            }
        }
        &__link {
            font-family: 'Inter-Bold', sans-serif;
            font-size: 1rem;
            color: #007FF4;
            flex-shrink: 0;
        }
        &-seminar,
        &-training {
            display: flex;
            flex-wrap: wrap;
        }
        .card-seminar,
        .card-training {
            margin-right: 1.33rem;
            &:last-child {
                margin-right: 0;
            }
        }
    }
}

@media (max-width: 992px) {
    .main {
        flex-direction: column;
        &-sidebar {
            width: 100%;
            max-width: none;
        }
        &-content {
            width: 100%;
            padding: 32px 32px 8px 32px;

            &-title {
                font-size: 1.75rem;
                line-height: 2.5rem;
            }
            &-seminar,
            &-training {
                justify-content: space-between;
            }
            .card-seminar,
            .card-training {
                margin-right: 0;
            }
        }
    }
}
@media (max-width: 768px) {
    .main-content {
        padding-top: 0.5rem;
        &-head {
            align-items: flex-start;
        }
        &-title {
            font-size: 1.5rem;
            line-height: 2rem;
        }
    }
}
@media (max-width: 576px) {
    .main-content {
        padding: 0.5rem 1rem;
        &-title {
            display: flex;
            flex-direction: column;
            span {
                font-size: 1rem;
                line-height: 1.5rem;
            }
        }
        &-seminar,
        &-training {
            justify-content: center;
        }
    }
}
</style>