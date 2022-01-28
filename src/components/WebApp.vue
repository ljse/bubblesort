<template>
    <div>
        <form @submit.prevent="submit" class="form">
            <div class="form__group">
                <label for="numbers" class="form__label">Numbers</label>
                <input type="text" class="form__input" :class="{'form__input--error' : error}" v-model="numbers">
                <span class="form__error" v-if="error">Oops! Ony number separated by spaces is allowed!</span>
            </div>
            <div class="form__group">
                <button type='submit' class="form__btn">Submit</button>
            </div>
        </form>
        <div class="result" v-if="result.length > 0">
            <h2 class="result__header">Result:</h2>
            <ul class="result__list">
                <li class="result__item" v-for="(number, index) in result" :key="index">
                    {{ number }}
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            numbers: '',
            number_array: [],
            result: [],
            error: false
        }
    },
    methods: {
        submit() {
            var done = false;
            if (!this.error) {
                while (!done) {
                    done = true;
                    for (let i = 0; i < this.number_array.length; i++) {
                        if (this.number_array[i] > this.number_array[i + 1]) {
                            done = false;
                            var tmp = this.number_array[i]
                            this.number_array[i] = this.number_array[i + 1]
                            this.number_array[i + 1] = tmp
                        }
                    }
                }
                this.result = this.number_array;
            }
        }
    },

    watch: {
        numbers() {
            this.number_array = this.numbers.split(' ').map(Number);
            if (this.number_array.length > 0) {
                for (let index = 0; index < this.number_array.length; index++) {
                    if (isNaN(this.number_array[index])) {
                        return this.error = true;
                    }
                    this.error = false;
                }
            }
        },
    }
}
</script>

<style lang="scss" scoped>
    .form {
        @include flex ($justify: center, $align: center, $direction: column);
        &__group {
            @include flex ($justify: center, $align: start, $direction: column);
            padding: 10px 15px;
        }
        &__label {
            font-size: .9rem;
        }
        &__input {
            width: 100%;
            padding: 5px 15px;
            margin: 8px 0;
            box-sizing: border-box;
            &--error {
                border-color: $red;
            }
        }
        &__error {
            font-size: .9rem;
            color: $red;
        }
        &__btn {
            background: $green;
            border: none;
            padding: 5px 15px;
            color: $white;
            cursor: pointer;
        }
    }
    .result {
        @include flex ($justify: center, $align: center, $direction: column);
        width: 300px;
        margin: auto;

        &__header {
            font-size: 1.2rem;
        }
        &__list {
            list-style: none;
            padding: 0;
        }
        &__item {
            font-size: .9rem;
        }
    }
</style>