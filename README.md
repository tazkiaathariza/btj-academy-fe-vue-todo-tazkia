# JavaScript Framework (VueJS) - To Do App - Tazkia
Folder ini merupakan task pertama dari materi JavaScript Framework. JavaScript framework yang digunakan adalah VueJS, sementara untuk styling digunakan CSS framework yaitu Bootstrap. 

## Getting started
1. Download atau clone repository ini :
```
git clone https://github.com/tazkiaathariza/btj-academy-fe-vue-todo-tazkia
```
2. Install seluruh dependencies yang diperlukan.
2. Jalankan `npm run dev`
3. Buka di browser lokal `http://127.0.0.1:5173/`

## Building
1. Menerapkan two-way binding dengan `v-model`
2. Melakukan rendering list dengan `v-for`
3. Class binding untuk mengatur style warna berdasarkan prioritas.
4. Menggunakan attribute binding lainnya seperti `v-on:submit` atau `@submit` dan `v-on:click` atau `@click`
5. Computed properties : untuk menghitung jumlah task berdasarkan prioritas secara dinamis.
6. Method : berisi fungsi-fungsi untuk menambahkan task, memindahkan task ke 'done', melakukan 'undone', menghapus data dari kolom 'todo' maupun 'done'

## What you can do in this TODO App
1. Menambahkan task baru yang akan disimpan di dalam local storage.
2. Menampilkan seluruh task yang belum selesai pada kolom 'TODO'.
3. Menandai task yang sudah selesai dengan tombol 'Done'.
4. Menampilan seluruh task yang sudah selesai pada kolom 'DONE'.
5. Menghapus task dari list 'TODO' maupun 'DONE'.
6. Melakukan 'Undone'.
7. Menghitung jumlah task dengan priority 'medium', 'high', 'low', dan'pending'.

Hasil :

![hasil](/public/ss.png)