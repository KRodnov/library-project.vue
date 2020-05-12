<template>
    <div class="form">
        <fieldset>
            <legend class="newbook">Добавление новой книги</legend>
            <label for="nameBook">Название книги</label>
            <input v-model:value="nameBook" id="nameBook" type="text" placeholder="Введите название книги">
            <br>
            <fieldset>
                <legend>Автор книги</legend>
                <label for="authorNameBook">Имя автора</label>
                <input v-model:value="authorNameBook" id="authorNameBook" type="text" placeholder="Введите имя автора">
                <label for="authorSurnameBook">Фамилия автора</label>
                <input v-model:value="authorSurnameBook" id="authorSurnameBook" type="text" placeholder="Введите фамилию автора">
            </fieldset>
            <br>
            <label for="yearBook">Год издания</label>
            <input v-model:value="yearBook" id="yearBook" type="number" placeholder="Введите год издания">
            <br>
            <label for="genreBook">Жанр</label>
            <select name="" v-model:value="genreBook" id="genreBook">
                <option value="Детективы">Детективы</option>
                <option value="Фантастика">Фантастика</option>
                <option value="Триллер">Триллер</option>
                <option value="Роман">Роман</option>
                <option value="Проза">Проза</option>
                <option value="Классика">Классика</option>
                <option value="Комиксы">Комиксы</option>
            </select>
            <br>
            <br>
            <button v-if="item === null" v-on:click="addButtonClicked" id="addNewBook">Добавить книгу</button>
            <div v-else>
                <button v-on:click="saveButtonClicked">Сохранить редактирование</button>
                <button v-on:click="backButtonClicked">Отменить редактирование</button>
            </div>
        </fieldset>



    </div>
</template>

<script>
    export default {
        data: function () {
            return {
                nameBook:null,
                authorNameBook:null,
                authorSurnameBook:null,
                yearBook:null,
                genreBook:null
            }
        },
        props: ['item'],

        watch: {
            item: function (val) {
                if (this.item !==null) {
                    this.nameBook = this.item.nameBook;
                    this.authorNameBook = this.item.authorNameBook;
                   this.authorSurnameBook = this.item.authorSurnameBook;
                    this.yearBook = this.item.yearBook;
                    this.genreBook = this.item.genreBook;
                } else {
                    this.nameBook = null,
                        this.authorNameBook = null,
                        this.authorSurnameBook = null,
                        this.yearBook = null,
                        this.genreBook = null
                }
            }
        },
        methods: {
            addButtonClicked: function () {
            this.$emit('addTodo', {nameBook:this.nameBook, authorNameBook:this.authorNameBook, authorSurnameBook:this.authorSurnameBook,
            yearBook:this.yearBook, genreBook:this.genreBook});
            this.nameBook = null;
                this.authorNameBook = null;
                this.authorSurnameBook = null;
                this.yearBook = null;
                this.genreBook = null;
            },
            saveButtonClicked: function () {
                this.$emit('updateTodo', {id:this.item.id, nameBook:this.nameBook, authorNameBook:this.authorNameBook, authorSurnameBook:this.authorSurnameBook,
                    yearBook:this.yearBook, genreBook:this.genreBook, status:this.item.status});
                this.nameBook = null;
                this.authorNameBook = null;
                this.authorSurnameBook = null;
                this.yearBook = null;
                this.genreBook = null;
            },
            backButtonClicked: function () {
                this.$emit('back', {id:this.item.id, nameBook:this.nameBook, authorNameBook:this.authorNameBook, authorSurnameBook:this.authorSurnameBook,
                    yearBook:this.yearBook, genreBook:this.genreBook, status:this.item.status});
                editingBook = null;
            }

        }
    }
</script>

<style scoped>

input {
    margin: 10px;
}
</style>