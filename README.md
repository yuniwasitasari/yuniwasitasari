## Pemrograman Berbasis Framework
Nama : Yuni Wasita Sari<br>
Kelas : TI 2D<br>
Nim : 220302096<br>

CodeIgniter4 <br>
**1.Apa itu CodeIgniter?**
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

**2. Installation**
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
   
**3. Build Your Application**<br>
**a.) Static Pages.** buka file rute yang terletak di **app/config/Routes.php**<br>
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
![image](https://github.com/yuniwasitasari/yuniwasitasari/assets/134575605/63b06bea-c334-4adb-b34d-ad8e0e425be1)<br>
![image](https://github.com/yuniwasitasari/yuniwasitasari/assets/134575605/b667b221-9592-4407-8281-4079d2fd9dee)<br>
- Lengkapi method view pada controller Pages<br>
```
<?php

namespace App\Controllers;

use CodeIgniter\Exceptions\PageNotFoundException;

class Pages extends BaseController
{
    public function index()
    {
        return view('welcome_message');
       
    }

    public function view($page = 'home')
    {
        if (! is_file(APPPATH . 'Views/pages/' . $page . '.php')) {
            // Whoops, we don't have a page for that!
            throw new PageNotFoundException($page);
        }

        $data['title'] = ucfirst($page); // Capitalize the first letter

        return view('templates/header', $data)
            . view('pages/' . $page)
            . view('templates/footer');
    }

}
```
- Running the app<br>
kunjungi localhost:8080/home untuk mengecek apakah berhasil atau tidak.<br>
![image](https://github.com/yuniwasitasari/yuniwasitasari/assets/134575605/8e9d4297-b91c-477e-a0d1-748ca66bba58)<br>
**b.) News Section**
- buat database dan tabel pada phpmyadmin nama database ci4tutorial.
```
CREATE TABLE news (
    id INT UNSIGNED NOT NULL AUTO_INCREMENT,
    title VARCHAR(128) NOT NULL,
    slug VARCHAR(128) NOT NULL,
    body TEXT NOT NULL,
    PRIMARY KEY (id),
    UNIQUE slug (slug)
);
```
isikan dengan data berikut<br>
```INSERT INTO news VALUES
(1,'Elvis sighted','elvis-sighted','Elvis was sighted at the Podunk internet cafe. It looked like he was writing a CodeIgniter app.'),
(2,'Say it isn\'t so!','say-it-isnt-so','Scientists conclude that some programmers have a sense of humor.'),
(3,'Caffeination, Yes!','caffeination-yes','World\'s largest coffee shop open onsite nested coffee shop for staff only.');
```
- pada file.env bagian database hapus tanda **'#'** dan ganti nama database menjadi **'ci4tutorial'** dan pada bagian password dikosongkan.<br>
![image](https://github.com/yuniwasitasari/yuniwasitasari/assets/134575605/988d5e73-9b45-462c-a99d-1db550223b43)<br>
- buat NewsModels<Br>
buka **app/Models** lalu buat file baru bernama **NewsModel.php** dan ketikkan kode di bawah ini.<br>
```
<?php

namespace App\Models;

use CodeIgniter\Model;

class NewsModel extends Model
{
    protected $table = 'news';
}
```
pada method getNews di model NewsModel tambahkan kode berikut:<br>
```
public function getNews($slug = false)
    {
        if ($slug === false) {
            return $this->findAll();
        }

        return $this->where(['slug' => $slug])->first();
    }
```
- menambahkan perintah routing di **app/Config/Routes.php**<br>
```
$routes->get('news', [News::class, 'index']);           
$routes->get('news/(:segment)', [News::class, 'show']); 
```
- membuat controller baru di **app/Controllers/News.php**<br>
```
<?php

namespace App\Controllers;

use App\Models\NewsModel;

class News extends BaseController
{
    public function index()
    {
        $model = model(NewsModel::class);

        $data['news'] = $model->getNews();
    }

    public function show($slug = null)
    {
        $model = model(NewsModel::class);

        $data['news'] = $model->getNews($slug);
    }
}
```
- melengkapi controller News pada method index<br>
```
<?php

namespace App\Controllers;

use App\Models\NewsModel;

class News extends BaseController
{
    public function index()
    {
        $model = model(NewsModel::class);

        $data = [
            'news'  => $model->getNews(),
            'title' => 'News archive',
        ];

        return view('templates/header', $data)
            . view('news/index')
            . view('templates/footer');
    }

    // ...
}
```
- buat file pada **app/Views/news/index.php** dan tambahkan kode berikut:<br>
```
<h2><?= esc($title) ?></h2>

<?php if (! empty($news) && is_array($news)): ?>

    <?php foreach ($news as $news_item): ?>

        <h3><?= esc($news_item['title']) ?></h3>

        <div class="main">
            <?= esc($news_item['body']) ?>
        </div>
        <p><a href="/news/<?= esc($news_item['slug'], 'url') ?>">View article</a></p>

    <?php endforeach ?>

<?php else: ?>

    <h3>No News</h3>

    <p>Unable to find any news for you.</p>

<?php endif ?>
```
- lengkapi controller News pada method show<br>
```
<?php

namespace App\Controllers;

use App\Models\NewsModel;
use CodeIgniter\Exceptions\PageNotFoundException;

class News extends BaseController
{
    // ...

    public function show($slug = null)
    {
        $model = model(NewsModel::class);

        $data['news'] = $model->getNews($slug);

        if (empty($data['news'])) {
            throw new PageNotFoundException('Cannot find the news item: ' . $slug);
        }

        $data['title'] = $data['news']['title'];

        return view('templates/header', $data)
            . view('news/view')
            . view('templates/footer');
    }
}
```
- buat tampilan atau view di **app/Views/news/view.php**<br>
```
<h2><?= esc($news['title']) ?></h2>
<p><?= esc($news['body']) ?></p>
```
- pada browser ketikkan **localhost:8080/news**<br>
![image](https://github.com/yuniwasitasari/yuniwasitasari/assets/134575605/04845ff1-fac8-4357-9dcf-2899471a4e40)<br>

**c.) Create News Section**
- aktifkan filter CSRF di file app/Config/Filter.php<br>
```
<?php

namespace Config;

use CodeIgniter\Config\BaseConfig;

class Filters extends BaseConfig
{
    // ...

    public $methods = [
        'post' => ['csrf'],
    ];

    // ...
}
```
- menambahkan perintah routing di **app/Config/Routes.php**<br>
```
<?php

// ...

use App\Controllers\News;
use App\Controllers\Pages;

$routes->get('news', [News::class, 'index']);
$routes->get('news/new', [News::class, 'new']); // Add this line
$routes->post('news', [News::class, 'create']); // Add this line
$routes->get('news/(:segment)', [News::class, 'show']);

$routes->get('pages', [Pages::class, 'index']);
$routes->get('(:segment)', [Pages::class, 'view']);
```
- create a form di app/Views/news/create.php<br>
```
<h2><?= esc($title) ?></h2>

<?= session()->getFlashdata('error') ?>
<?= validation_list_errors() ?>

<form action="/news" method="post">
    <?= csrf_field() ?>

    <label for="title">Title</label>
    <input type="input" name="title" value="<?= set_value('title') ?>">
    <br>

    <label for="body">Text</label>
    <textarea name="body" cols="45" rows="4"><?= set_value('body') ?></textarea>
    <br>

    <input type="submit" name="submit" value="Create news item">
</form>
```
- pada controller News tambahkan method new untuk menampilkan formulir<br>
```
<?php

namespace App\Controllers;

use App\Models\NewsModel;
use CodeIgniter\Exceptions\PageNotFoundException;

class News extends BaseController
{
    // ...

    public function new()
    {
        helper('form');

        return view('templates/header', ['title' => 'Create a news item'])
            . view('news/create')
            . view('templates/footer');
    }
}
```
- tambahkan method create pada controller News<br>
```
<?php

namespace App\Controllers;

use App\Models\NewsModel;
use CodeIgniter\Exceptions\PageNotFoundException;

class News extends BaseController
{
    // ...

    public function create()
    {
        helper('form');

        $data = $this->request->getPost(['title', 'body']);

        // Checks whether the submitted data passed the validation rules.
        if (! $this->validateData($data, [
            'title' => 'required|max_length[255]|min_length[3]',
            'body'  => 'required|max_length[5000]|min_length[10]',
        ])) {
            // The validation fails, so returns the form.
            return $this->new();
        }

        // Gets the validated data.
        $post = $this->validator->getValidated();

        $model = model(NewsModel::class);

        $model->save([
            'title' => $post['title'],
            'slug'  => url_title($post['title'], '-', true),
            'body'  => $post['body'],
        ]);

        return view('templates/header', ['title' => 'Create a news item'])
            . view('news/success')
            . view('templates/footer');
    }
}
```
- membuat halaman seccess di **app/Views/news/success.php**<br>
```
<p>News item created successfully.</p>
```
- pada **app/models/newsmodels.php** tambahkan kode berikut :<br>
```
<?php

namespace App\Models;

use CodeIgniter\Model;

class NewsModel extends Model
{
    protected $table = 'news';

    protected $allowedFields = ['title', 'slug', 'body'];
}
```
- pada browser ketikkan **localhost:8080/news/new**<br>
![image](https://github.com/yuniwasitasari/yuniwasitasari/assets/134575605/794a6590-ea40-4222-9881-f9ee04c23c27)<br>

**4.Codeigniter4 Overview**
a.)**Model, View, and Controller**<br>
- model mengelola data aplikasi dan membantu menegakkan aturan bisnis khusus yang mungkin diperlukan aplikasi.<br>
- view adalah file sederhana dengan sedikit atau tanpa logika, yang menampilkan informasi kepada pengguna.<br>
- controller bertindak sebagai kode perekat menyusun data bolak balik antara tampilan dan penyimpanan data.<br>
- komponen<br>
**view**<br>
view umumnya disimpan di **app/Views**<br>
**model**<br>
model biasanya disimpan di **app/Models**<br>
**Controller**<br>
controller biasanya disimpan di **app/controllers**<br>
b.)**konfigirasi**<br>
konfigurasi awal dilakukan di **app/Config/Autoload.php** berikut kodenya:<br>
```
<?php

namespace Config;

use CodeIgniter\Config\AutoloadConfig;

class Autoload extends AutoloadConfig
{
    // ...
    public $psr4 = [
        APP_NAMESPACE => APPPATH, // For custom app namespace
        'Config'      => APPPATH . 'Config',
    ];

    // ...
}
```
- **Application Namespace**
- mengubah namespace dengan mengedit file **app/Config/Constants.php**<br>
```
defined('APP_NAMESPACE') || define('APP_NAMESPACE', 'App');
```
- **Classmap**<br>
dapat menggunakan classmap untuk menautkan ke perpustakaan pihak ketiga yang tidak diberi spasi nama<br>
```
<?php

namespace Config;

use CodeIgniter\Config\AutoloadConfig;

class Autoload extends AutoloadConfig
{
    // ...
    public $classmap = [
        'Markdown' => APPPATH . 'ThirdParty/markdown.php',
    ];

    // ...
}
```


  








  
   
   
   
   















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
