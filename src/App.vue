<template>
  <div id="app">
<forms v-bind:item="editingBook" v-on:back="editingBook = null" v-on:addTodo="addTodoListener" v-on:updateTodo="updateTodoListener" />
    <book v-for="book in books"  v-bind:item="book" v-on:finishBook="finishBookListener" v-on:editBook="editBookListener" v-on:deleteBook="deleteBookListener" />
  </div>

</template>

<script>
import book from './components/book.vue'
import forms from './components/forms.vue'

export default {
  data: function () {
    return {
      editingBook:null,
      books : [
        {id: 1, nameBook: 'Происхождение', authorNameBook: 'Дэн', authorSurnameBook: 'Браун', yearBook: 2017, genreBook: 'Фантастика', status: "finished"},
        {id: 2, nameBook: 'Текст', authorNameBook: 'Дмитрий', authorSurnameBook: 'Глуховский', yearBook: 2015, genreBook: 'Детектив', status: "pending"},
        {id: 3, nameBook: 'Мертвая зона', authorNameBook: 'Стивен', authorSurnameBook: 'Кинг', yearBook: 1979, genreBook: 'Триллер', status: "pending"},
        {id: 4, nameBook: 'Война и Мир', authorNameBook: 'Лев', authorSurnameBook: 'Толстой', yearBook: 1865, genreBook: 'Классика', status: "finished"},
        {id: 5, nameBook: 'Отцы и дети', authorNameBook: 'Иван', authorSurnameBook: 'Тургенев', yearBook: 1861, genreBook: 'Классика', status: "pending"},
        {id: 6, nameBook: 'Мир глазами кота Боба', authorNameBook: 'Джеймс', authorSurnameBook: 'Боуэн', yearBook: 2013, genreBook: 'Роман', status: "finished"},
        {id: 7, nameBook: 'Домовой', authorNameBook: 'Олег', authorSurnameBook: 'Рой', yearBook: 2020, genreBook: 'Проза', status: "finished"},
        {id: 8, nameBook: 'The Sipmsons', authorNameBook: 'Мэтт', authorSurnameBook: 'Грёнинг', yearBook: 2010, genreBook: 'Комиксы', status: "finished"},
      ]
    }
  },
  name: 'App',
  components: {
    book:book,
    forms:forms
  },

  methods: {
    updateTodoListener: function (item) {
      let todoIndex = this.books.findIndex((el) => el.id === item.id);
      if (todoIndex >= 0) {
        this.books.splice(todoIndex, 1, item);
        this.editingCard = null;
      }
    },

    editBookListener: function (id) {
      let todoIndex = this.books.findIndex((el) => el.id === id);
      if (todoIndex >= 0) {
        this.editingBook = this.books[todoIndex];
      }
    },

    deleteBookListener: function (id) {
      let todoIndex = this.books.findIndex((el) => el.id === id);
      if (todoIndex >= 0) {
        this.books.splice(todoIndex, 1);
      }
    },
    addTodoListener: function (item) {
      item.id = this.fetchMaxId() + 1;
      item.status = 'pending';
      this.books.push(item);
    },

    finishBookListener: function (id) {
      let finishedTodo = this.books.find((el) => el.id === id);
      if (finishedTodo) {
        finishedTodo.status = 'finished';
      }
    },
    fetchMaxId: function () {
      return Math.max.apply(Math, this.books.map((o) => o.id
      ))
    },

  }



}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  /*color: #2c3e50;*/
    margin-top: 25px;

}
</style>
