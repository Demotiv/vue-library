<template>
    <div class="book">
        <div class="book__info">
            <div class="book__header">
                <h3>{{ staff }}</h3>
                <div></div>
            </div>
            <section class="book__body">
                <div class="book__title-n-author">
                    <h4 class="book__title">{{ book.title }}</h4>
                    <p class="book__author">By {{ book.author }}</p>
                </div>
                <div class="book__text">
                    <p>{{ book.p }}</p>
                </div>
                <button 
                    class="book__button"
                    @click="handleClick">{{ selectedBook ? 'Own' : 'Buy' }}</button>
            </section>
        </div>
        <img 
            class="book__img" 
            :src="img.src" 
            :alt="img.alt">
    </div>
</template>

<script>
import { addBooks, hasUserBankInfo } from '@/storage'

export default {
    props: {
        staff: {
            type: String,
            required: true
        },
        book: {
            type: Object,
            required: true
        },
        img: {
            type: Object,
            required: true
        },
        userIn: {
            type: Boolean,
            default: false
        },
        userId: {
            type: Object,
            default: () => ({})
        },
        currentSeason: {
            type: String,
            required: true
        },
    },
    data() {
        return {
            selectedBook: false
        }
    },
    methods: {
        /*
        changeSelectedBook() {
            this.selectedBook = !this.selectedBook
        },
        */
        handleClick() {
            if (!this.userIn) {
                console.log('click')
                this.$emit('open-login')
            } else if (hasUserBankInfo(this.userId.email)) {
                const updatedUserId = addBooks(this.userId.email, this.book.title, this.book.author)

                /*
                let result = updatedUserId.selectedBooks.map(function(val) {
                    return Object.keys(val).map(function(key) {
                        return val[key]
                    })
                })
                
                if (result.find(book => book[0] === this.book.title && book[1] === this.book.author)) {
                    this.changeSelectedBook()
                }
                */

                /*
                const book = updatedUserId?.selectedBooks?.find(
                book => book.title === this.book.title && book.author === this.book.author
                )

                if (book) {
                    this.selectedBook = true
                }
                */ 

               /*
                this.selectedBook = !this.selectedBook
                */

                this.$emit('update-new-user-id', updatedUserId)
            } else {
                this.$emit('open-buy-card')
            }
        }
    }
}
</script>

<style lang="scss" scoped>
.book {
    position: relative;
    display: flex;
    flex-direction: column;
    width: 590px;
    height: max-content;

    &__info {
        display: flex;
        flex-direction: column;
        width: 550px;
        min-height: 555px;
        border: 1px solid $black;
    }

    &__header {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        margin: 14px 0 0 19px;

        & h3 {
            font-family: $forum;
            font-weight: 400;
            font-size: 20px;
            line-height: 200%;
            letter-spacing: 0.1em;
            text-transform: capitalize;
            color: $black;
        }

        & div {
            border: 1px solid $sand;
            width: 60px;
            height: 0px; 
        }
    }

    &__body {
        margin: 20px 0 0 19px;
        display: flex;
        flex-direction: column;
    }

    &__title-n-author {
        font-family: $inter;
        font-weight: 700;
        font-size: 15px;
        line-height: 267%;
        letter-spacing: 0.13em;
        color: $black;

        & h4 {
            text-transform: uppercase;
        }

        & p {
            text-transform: capitalize;
        }
    }

    &__text {
        margin-top: 20px;
        max-width: 355px;

        & p {
            font-family: $inter;
            font-size: 15px;
            line-height: 267%;
            letter-spacing: 0.13em;
            color: $black;
            min-height: 320px;
            text-transform: capitalize;
        }
    }

    &__button {
        margin-top: 15px;
        margin-bottom: 14px;
        width: 75px;
        height: 30px;
        font-family: $inter;
        font-weight: bold;
        font-size: 10px;
        letter-spacing: 0.1em;
        color: $dark;
        background-color: $white;
        border: 1px solid $dark;
        border-radius: 2px;
        cursor: pointer;
        transition: background-color 0.3s ease-in-out;

        &:hover {
            background-color: $sand;
        }
    }

    &__img {
        position: absolute;
        right: 0%;
        bottom: 0%;
        width: 200px;
        height: 300px;
    }
}
</style>