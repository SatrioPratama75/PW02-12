#PEMROGRAMAN WEB 02 - PERTEMUAN 12
## Tugas : Pagination dan Pencarian

### Langkah-langkah Praktikum
#### Membuat Pagination
Pagination merupakan proses yang digunakan untuk membatasi tampilan yang panjang
dari data yang banyak pada sebuah website. Fungsi pagination adalah memecah tampilan
menjadi beberapa halaman tergantung banyaknya data yang akan ditampilkan pada
setiap halaman.
Pada Codeigniter 4, fungsi pagination sudah tersedia pada Library sehingga cukup mudah
menggunakannya.
Untuk membuat pagination, buka Kembali Controller Artikel, kemudian modifikasi kode
pada method admin_index seperti berikut.
'''php
    public function admin_index()
    {
        $title = 'Daftar Artikel';
        $model = new ArtikelModel();
        $data = [
            'title' => $title,
            'artikel' => $model->paginate(10), #data dibatasi 10 record per halaman
            'pager' => $model->pager,
        ];
        return view('artikel/admin_index', $data);
    }
 '''
![Pagination-1](https://github.com/SatrioPratama75/PW02-12/assets/92651803/7f604b7e-bc39-4561-82f1-bfeedecb458e)

Kemudian buka file views/artikel/admin_index.php dan tambahkan kode berikut
dibawah deklarasi tabel data.

![pagination-2](https://github.com/SatrioPratama75/PW02-12/assets/92651803/a4e80ff8-e55c-4718-95c5-0f944c765eee)
