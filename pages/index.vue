<template>
  <div class="container">
    <h1>Manajemen Perpustakaan</h1>
    <div class="form-container">
      <form @submit.prevent="handleSubmit">
        <label for="title">Judul Buku:</label>
        <input v-model="title" type="text" id="title" required>

        <label for="author">Penulis:</label>
        <input v-model="author" type="text" id="author" required>

        <label for="genre">Genre:</label>
        <input v-model="genre" type="text" id="genre" required>

        <label for="publishedYear">Tahun Terbit:</label>
        <input v-model="publishedYear" type="number" id="publishedYear" required>

        <div class="buttons">
          <button type="submit">{{ editingIndex === null ? 'Tambah' : 'Simpan' }}</button>
          <button type="button" @click="clearForm">Bersihkan</button>
        </div>
      </form>
    </div>

    <div class="book-list">
      <div v-for="(book, index) in bookList" :key="index" class="book">
        <p><strong>Judul Buku:</strong> {{ book.title }}</p>
        <p><strong>Penulis:</strong> {{ book.author }}</p>
        <p><strong>Genre:</strong> {{ book.genre }}</p>
        <p><strong>Tahun Terbit:</strong> {{ book.publishedYear }}</p>
        <div class="book-buttons">
          <button @click="editBook(index)">Edit</button>
          <button @click="deleteBook(index)">Delete</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      author: '',
      genre: '',
      publishedYear: '',
      bookList: [],
      editingIndex: null,
    };
  },
  methods: {
    handleSubmit() {
      if (this.editingIndex === null) {
        // Tambah buku baru jika tidak sedang mengedit
        const newBook = {
          title: this.title,
          author: this.author,
          genre: this.genre,
          publishedYear: this.publishedYear,
        };
        this.bookList.push(newBook);
      } else {
        // Simpan perubahan jika sedang mengedit
        const editedBook = {
          title: this.title,
          author: this.author,
          genre: this.genre,
          publishedYear: this.publishedYear,
        };
        this.$set(this.bookList, this.editingIndex, editedBook);
        this.editingIndex = null;
      }

      this.clearForm();
    },
    editBook(index) {
      const book = this.bookList[index];
      this.title = book.title;
      this.author = book.author;
      this.genre = book.genre;
      this.publishedYear = book.publishedYear;
      this.editingIndex = index;
    },
    deleteBook(index) {
      this.bookList.splice(index, 1);
      this.clearForm();
    },
    clearForm() {
      this.title = '';
      this.author = '';
      this.genre = '';
      this.publishedYear = '';
      this.editingIndex = null;
    },
  },
};
</script>

<style scoped>
.container {
  background-color: #f8f9fa;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  width: 400px;
  margin: 20px auto;
}

h1 {
  text-align: center;
  color: #007bff;
}

.form-container {
  margin-bottom: 20px;
}

form {
  display: flex;
  flex-direction: column;
}

label {
  margin-bottom: 5px;
}

input {
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.buttons {
  display: flex;
  justify-content: space-between;
}

button {
  flex: 1;
  padding: 10px;
  cursor: pointer;
  border: none;
  border-radius: 4px;
}

button:first-child {
  margin-right: 10px;
}

.book-list {
  border-top: 1px solid #ddd;
  padding-top: 20px;
}

.book {
  margin-bottom: 20px;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.book-buttons {
  display: flex;
  justify-content: space-between;
}

button {
  padding: 10px 15px;
  cursor: pointer;
  border: none;
  border-radius: 4px;
  background-color: #007bff; /* Default blue background color */
  color: white;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #0056b3; /* Darker blue on hover */
}

button:nth-child(1) {
  background-color: #4caf50; /* Green */
  color: white;
}

button:nth-child(1):hover {
  background-color: #1d3ec4;
}

button:nth-child(2) {
  background-color: #f44336; /* Red */
  color: white;
}

button:nth-child(2):hover {
  background-color: #d32f97; /* Darker red on hover */
}
</style>