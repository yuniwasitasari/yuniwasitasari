## Pemrograman Berbasis Framework
Nama : Yuni Wasita Sari<br>
Kelas : TI 2D<br>
Nim : 220302096<br>

CodeIgniter4

1. **Apa itu CodeIgniter?**
  Codeigniter adalah salah satu framework untuk membuat website dengan bahasa pemrograman PHP. Codeigniter terkenal dengan konsep MVC-nya. MVC merupakan singkatan dari Model-View-Controller.<br>
  Apa itu Framework?
  framework dalam bahasa indonesi artinya kerangka kerja.
  PHP dan Ekstensi yang diperlukan<br>
   memerlukan PHP versi 7.4 dengan esktensi PHP berikut diaktifkan :<br>
   - internasional<br>
   - mbstring<br>
   - json<br>

   Database yang digunakan<br>
   - MySQL<br>
   - PostgreSQL<br>
   - SQLite3<br>
   - SQLSRV<br>
   - Oracle Database melalui OCI8<br>

2. **Installation**
   Codeigniter memiliki dua metode instalasi yang didukung : download manual atau menggunakan composer.<br>
   **a. Manual<br>**
   kunjungi sistus resmi www.codeigniter.com<br>
   ![image](https://github.com/yuniwasitasari/yuniwasitasari/assets/134575605/8e727eea-4de2-43ed-948f-6ec12748907e)
   ekstrak file ZIP Codeigniter ke htdocs.<br>
   
   **b. composer<br>**
   untuk menginstal CI4 dengn composer ketikkan perintah berikut ini :
   ```
   _composer create-project codeigniter4/appstarter project-root_.<br>
   ```
   ![image](https://github.com/yuniwasitasari/yuniwasitasari/assets/134575605/21d87cb9-0eae-4d44-9e79-c7bc34873c12)<br>
   ada beberapa argumen yang kita berikan pada perintah ini :<br>
   -_create-project_ adalah perintah untuk membuat proyek baru dengan komposer.<br>
   -_codeigniter4/appstarter_ adalah file CI yang akan di-download.<br>
   -_project-root_ adalah nama proyek yang akan dibuat. <br>
   setelah prosesnya selesai, kita akan mendapatkan folder baru dengan nama _project-root_.<br>
   buka folder yang sudah didownload menggunakan VS Code.<br>
   buka terminal lalu ketikkan ```_php spark serve_```.<br>
   ![image](https://github.com/yuniwasitasari/yuniwasitasari/assets/134575605/828f250d-6685-4697-be9b-577924d75c3a)<br>
   perintah ini akan menjalankan server CI4 pada port 8080, lalu buka web beowser dan ketikkan alamat http://localhost:8080<br>

   **c. Atur ke metode development**<br>
   pada file .env ubah #CI_environment = production menjadi development agar semua eror akan ditampilkan.<br>
   ```
   CI_ENVIRONMENT = development
   ```
   **d. atur baseURL**<br>
   diganti dengan alamat dari website kita.<br>
   ```
   app.baseURL = 'http://localhost:8080'
   ```
3. **Build Your Application**<br>
   a.) Static Pages. buka file rute yang terletak di **app/config/Routes.php**<br>
```
<?php

use CodeIgniter\Router\RouteCollection;

/**
 * @var RouteCollection $routes
 */
$routes->get('/', 'Home::index');
```
tambahkan baris berikut, setelah arahan rute untuk '/'<br>
```
use App\Controllers\Pages;

$routes->get('pages', [Pages::class, 'index']);
$routes->get('(:segment)', [Pages::class, 'view']);
```
- buat controller page. Buat file di **app/Controllers/Pages.php** dengan kode seperti dibawah ini.<br>
```
<?php

namespace App\Controllers;

class Pages extends BaseController
{
    public function index()
    {
        return view('welcome_message');
       
    }

    public function view($page = 'home')
    {
  // ....
    }

}
```
- Views<br>
  buat header di **app/Views/templates/header.php** lalu tambahkan kode seperti dibawah ini.
```
<!doctype html>
<html>
<head>
    <title>CodeIgniter Tutorial</title>
</head>
<body>

    <h1><?= esc($title) ?></h1>
```
  buat footer di **app/Views/templates/footer.php** lalu tambahkan kode seperti dibawah ini.
```
<em>&copy; 2022</em>
</body>
</html>
```
- adding logic to the controller<br>
Buat home.php dan about.php di **app/View/pages**. di dalam file tersebut isikan beberapa teks misalkan Hello World!!.<br>
![image](https://github.com/yuniwasitasari/yuniwasitasari/assets/134575605/63b06bea-c334-4adb-b34d-ad8e0e425be1)







  
   
   
   
   















### Hi there 👋

<!--
**yuniwasitasari/yuniwasitasari** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
