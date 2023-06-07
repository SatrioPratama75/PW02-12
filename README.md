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

 ```php
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
```

![Pagination-1](https://github.com/SatrioPratama75/PW02-12/assets/92651803/7f604b7e-bc39-4561-82f1-bfeedecb458e)

Kemudian buka file views/artikel/admin_index.php dan tambahkan kode berikut
dibawah deklarasi tabel data.
```php
<?= $pager->links(); ?>
```
![pagination-2](https://github.com/SatrioPratama75/PW02-12/assets/92651803/a4e80ff8-e55c-4718-95c5-0f944c765eee)

Selanjutnya buka kembali menu daftar artikel, tambahkan data lagi untuk melihat
hasilnya.
![Result-pagination](https://github.com/SatrioPratama75/PW02-12/assets/92651803/0549a9c5-7133-45ff-81f5-f3bcb7f17baf)

#### Membuat Pencarian
Pencarian data digunakan untuk memfilter data.
Untuk membuat pencarian data, buka kembali Controller Artikel, pada method
admin_index ubah kodenya seperti berikut.
```php
    public function admin_index()
    {
        $title = 'Daftar Artikel';
        $q = $this->request->getVar('q') ?? '';
        $model = new ArtikelModel();
        $data = [
            'title' => $title,
            'q' => $q,
            'artikel' => $model->like('judul', $q)->paginate(2), # data dibatasi 10 record per halaman
            'pager' => $model->pager,
        ];
        return view('artikel/admin_index', $data);
    }
```
![Search-1](https://github.com/SatrioPratama75/PW02-12/assets/92651803/935d7142-63b4-43d8-976c-e55337149b82)

Kemudian buka kembali file views/artikel/admin_index.php dan tambahkan form
pencarian sebelum deklarasi tabel seperti berikut:
```php
<form method="get" class="form-search">
  <input type="text" name="q" value="<?= $q; ?>" class="text-search" placeholder="Cari data">
  <input type="submit" value="Cari" class="btn btn-primary submit-search">
</form>
```
![Search-3](https://github.com/SatrioPratama75/PW02-12/assets/92651803/1ee46030-f99a-45a3-8f89-2eb3d311f23c)

Dan pada link pager ubah seperti berikut.
```php
<?= $pager->only(['q'])->links(); ?>
```

Selanjutnya ujicoba dengan membuka kembali halaman admin artikel, masukkan kata
kunci tertentu pada form pencarian.

![Search-Result](https://github.com/SatrioPratama75/PW02-12/assets/92651803/b57532a8-708d-42d4-afc3-59d15a34a9a9)

# Terima kasih

