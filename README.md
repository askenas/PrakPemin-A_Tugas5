# PrakPemin-A_Tugas5
1. Dynamic Route
Dynamic route adalah route yang dapat berubah-ubah, contohnya pada saat kita membuka
suatu halaman web, kadang kita melihat /users/1 atau /users/2 , hal ini yang dinamakan
dynamic routes.
Untuk menambahkan dynamic routes pada aplikasi lumen kita, kita dapat menggunakan
syntax berikut,![Screenshot 2023-10-11 151319](https://github.com/askenas/PrakPemin-A_Tugas5/assets/134838656/bfc5459a-ddd5-4637-a47c-252a33a43392)
Saat menambahkan parameter pada routes, kita tidak terbatas pada 1 variable saja, namun
kita dapat menambahkan sebanyak yang diperlukan seperti kode berikut,
$router->get('/post/{postId}/comments/{commentId}', function ($postId, $commentId) {
return 'Post ID = ' . $postId . ' Comments ID = ' . $commentId;
});

Pada dynamic routes kita juga bisa menambahkan optional routes, yang mana optional
routes tidak mengharuskan kita untuk memberi variable pada endpoint kita, namun saat kita
memanggil endpoint, dapat menggunakan parameter variable ataupun tidak, seperti pada
kode dibawah ini,

$router->get('/users[/{userId}]', function ($userId = null) {
return $userId === null ? 'Data semua users' : 'Data user dengan id ' . $userId;
});

2. Aliases Route
Aliases Route digunakan untuk memberi nama pada route yang telah kita buat, hal ini dapat
membantu kita, saat kita ingin memanggil route tersebut pada aplikasi kita. Berikut syntax
untuk menambahkan aliases route

$router->get('/auth/login', ['as' => 'route.auth.login', function (...) {...}])
...
$router->get('/profile', function (Request $request) {
if ($request->isLoggedIn) {
return redirect()->route('route.auth.login');
}
});

3. Group Route
Pada lumen, kita juga dapat memberikan grouping pada routes kita agar lebih mudah pada
saat penulisan route pada web.php kita. Kita dapat melakukan grouping dengan
menggunakan syntax berikut,

$router->group(['prefix' => 'users'], function () use ($router) {
$router->get('/', function () { // menjadi /users/, /users => prefix, / => path
return "GET /users";
});
});
![Screenshot 2023-10-11 151611](https://github.com/askenas/PrakPemin-A_Tugas5/assets/134838656/1d1fc40b-d512-44ac-b858-70fefd0dcf8f)

4. Middleware
Middleware adalah penengah antara komunikasi aplikasi dan client. Middleware biasanya
digunakan untuk membatasi siapa yang dapat berinteraksi dengan aplikasi kita dan
semacamnya, kita dapat menambahkan middleware dengan menambahkan file pada folder

app/Http/Middleware . Pada folder tersebut terdapat file ExampleMiddleware , kita dapat men-
copy file tersebut untuk membuat middleware baru.

Pada praktikum kali ini akan dibuat middleware Age dengan isi,
![Screenshot 2023-10-11 151802](https://github.com/askenas/PrakPemin-A_Tugas5/assets/134838656/a61474d7-94e6-46b5-abc3-efb5ba59b215)
Kemudian, setelah menambahkan filter pada AgeMiddleware , kita harus mendaftarkan
AgeMiddleware pada aplikasi kita, pada file bootstrap/app.php seperti berikut ini,
![Screenshot 2023-10-11 153551](https://github.com/askenas/PrakPemin-A_Tugas5/assets/134838656/00b70580-92c5-47d6-9864-8470338206e9)
Lalu, kita dapat menambahkan middleware pada routes kita dengan menambahkan opsi
middleware pada salah satu route, contohnya,

![Screenshot 2023-10-11 154121](https://github.com/askenas/PrakPemin-A_Tugas5/assets/134838656/e9e5720e-5581-4f04-ba9b-40ef1602ba2a)
