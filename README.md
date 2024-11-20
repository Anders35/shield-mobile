# Shield Mobile

## Tugas 7

### Jelaskan apa yang dimaksud dengan _stateless widget_ dan _stateful widget_, dan jelaskan perbedaan dari keduanya.

_Stateless widget_ adalah jenis _widget_ yang tidak memiliki _state_ yang dapat berubah setelah _widget_ tersebut dibuat. _Stateless widget_ bersifat statis dan tidak dapat memperbarui tampilan atau data secara dinamis. Sedangkan, _stateful widget_ adalah _widget_ yang memiliki _state_ yang dapat berubah dan dapat memperbarui tampilan dan data secara dinamis.

### Sebutkan _widget_ apa saja yang kamu gunakan pada proyek ini dan jelaskan fungsinya.

- `MaterialApp`:  mengatur tema dan rute aplikasi
- `Scaffold`: menyediakan struktur dasar untuk halaman aplikasi, termasuk `AppBar` dan `body`
- `AppBar`: menampilkan bar judul di bagian atas
- `Column`: mengatur tata letak _widget_ secara vertikal
- `Row`: mengatur tata letak _widget_ secara horizontal
- `Padding`: memberikan jarak di sekeliling _widget_
- `Text`: menampilkan teks seperti judul dan konten
- `GridView.count`: menampilkan item-item dalam bentuk grid 3 kolom
- `Card`: menampilkan informasi NPM, nama, dan kelas dalam bentuk kartu
- `Material`: memberikan efek _material_ pada elemen, seperti warna latar belakang dan sudut melengkung
- `InkWell`: menambahkan aksi ketika `ItemCard` ditekan, menampilkan pesan `SnackBar`
- `Icon`: menampilkan ikon pada setiap item
- `SnackBar`: menampilkan pesan sementara di bagian bawah layar

### Apa fungsi dari `setState()`? Jelaskan variabel apa saja yang dapat terdampak dengan fungsi tersebut.

Fungsi `setState()` digunakan untuk mengubah state dari _stateful widget_. Variabel yang dapat terdampak adalah variabel yang didefinisikan dalam kelas _state_ dari _stateful widget_.

### Jelaskan perbedaan antara `const` dengan `final`.

`const` digunakan untuk deklarasi variabel yang nilainya bersifat konstan dan harus sudah diketahui pada saat _compile time_, sedangkan `final` digunakan untuk deklarasi variabel yang nilainya tetap namun bisa diinisialisasi pada saat _runtime_.

### Implementasi Checklist

1. Merapikan berkas `main.dart` menjadi seperti berikut.
    ```dart
    import 'package:flutter/material.dart';
    import 'package:shield_mobile/menu.dart';

    void main() {
      runApp(const MyApp());
    }

    class MyApp extends StatelessWidget {
      const MyApp({super.key});

      // This widget is the root of your application.
      @override
      Widget build(BuildContext context) {
        return MaterialApp(
          title: 'Flutter Demo',
          theme: ThemeData(
            // This is the theme of your application.
            //
            // TRY THIS: Try running your application with "flutter run". You'll see
            // the application has a purple toolbar. Then, without quitting the app,
            // try changing the seedColor in the colorScheme below to Colors.green
            // and then invoke "hot reload" (save your changes or press the "hot
            // reload" button in a Flutter-supported IDE, or press "r" if you used
            // the command line to start the app).
            //
            // Notice that the counter didn't reset back to zero; the application
            // state is not lost during the reload. To reset the state, use hot
            // restart instead.
            //
            // This works for code too, not just values: Most code changes can be
            // tested with just a hot reload.
            colorScheme: ColorScheme.fromSwatch(
                  primarySwatch: Colors.deepPurple,
            ).copyWith(secondary: Colors.deepPurple[400]),
            useMaterial3: true,
          ),
          home: MyHomePage(),
        );
      }
    }
    ```
2. Memindahkan _class_ `MyHomePage` ke berkas baru bernama `menu.dart` dan mengubah sifat _Widget_ menjadi _Stateless_ seperti berikut.
    ```dart
    import 'package:flutter/material.dart';

    class MyHomePage extends StatelessWidget {
        MyHomePage({super.key});

        @override
        Widget build(BuildContext context) {
          return Scaffold(
            ...
          );
        }
    }
    ```
3. Mendeklarasikan tiga variabel yang berisi NPM, nama, dan kelas pada _class_ `MyHomePage` di berkas `menu.dart` seperti berikut.
    ```dart
    class MyHomePage extends StatelessWidget {
      final String npm = '2306201621'; // NPM
      final String name = 'Anders Willard Leo'; // Nama
      final String className = 'PBP E'; // Kelas
      
      ...
    }
    ```
4. Membuat _class_ baru bernama `InfoCard` pada berkas `menu.dart` dengan kode berikut.
    ```dart
    ...
    class InfoCard extends StatelessWidget {
      // Kartu informasi yang menampilkan title dan content.

      final String title;  // Judul kartu.
      final String content;  // Isi kartu.

      const InfoCard({super.key, required this.title, required this.content});

      @override
      Widget build(BuildContext context) {
        return Card(
          // Membuat kotak kartu dengan bayangan dibawahnya.
          elevation: 2.0,
          child: Container(
            // Mengatur ukuran dan jarak di dalam kartu.
            width: MediaQuery.of(context).size.width / 3.5, // menyesuaikan dengan lebar device yang digunakan.
            padding: const EdgeInsets.all(16.0),
            // Menyusun title dan content secara vertikal.
            child: Column(
              children: [
                Text(
                  title,
                  style: const TextStyle(fontWeight: FontWeight.bold),
                ),
                const SizedBox(height: 8.0),
                Text(content),
              ],
            ),
          ),
        );
      }
    }
    ```
5. Membuat class baru bernama `ItemHomePage` dengan kode berikut.
    ```dart
    ...
    class ItemHomepage {
      final String name;
      final IconData icon;
      final Color color;

      ItemHomepage(this.name, this.icon, this.color);
    }
    ...
    ```
6. Membuat _list of_ `ItemHomePage` pada _class_ `MyHomePage` dengan kode berikut.
    ```dart
    class MyHomePage extends StatelessWidget {  
      ...
      final List<ItemHomepage> items = [
        ItemHomepage("Lihat Daftar Produk", Icons.list, Colors.blue),
        ItemHomepage("Tambah Produk", Icons.add, Colors.green),
        ItemHomepage("Logout", Icons.logout, Colors.red),
      ];
      ...
    }
7. Membuat _class_ baru bernama `ItemCard` untuk menampilkan tombol-tombol dan tombol akan menampilkan _snackbar_ ketika ditekan dengan kode berikut.
    ```dart
    ...
    class ItemCard extends StatelessWidget {
      // Menampilkan kartu dengan ikon dan nama.

      final ItemHomepage item; 
      
      const ItemCard(this.item, {super.key}); 

      @override
      Widget build(BuildContext context) {
        return Material(
          // Menentukan warna latar belakang dari tema aplikasi.
          color: item.color,
          // Membuat sudut kartu melengkung.
          borderRadius: BorderRadius.circular(12),
          
          child: InkWell(
            // Aksi ketika kartu ditekan.
            onTap: () {
              // Menampilkan pesan SnackBar saat kartu ditekan.
              ScaffoldMessenger.of(context)
                ..hideCurrentSnackBar()
                ..showSnackBar(
                  SnackBar(content: Text("Kamu telah menekan tombol ${item.name}"))
                );
            },
            // Container untuk menyimpan Icon dan Text
            child: Container(
              padding: const EdgeInsets.all(8),
              child: Center(
                child: Column(
                  // Menyusun ikon dan teks di tengah kartu.
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: [
                    Icon(
                      item.icon,
                      color: Colors.white,
                      size: 30.0,
                    ),
                    const Padding(padding: EdgeInsets.all(3)),
                    Text(
                      item.name,
                      textAlign: TextAlign.center,
                      style: const TextStyle(color: Colors.white),
                    ),
                  ],
                ),
              ),
            ),
          ),
        );
      } 
    }
    ...
    ```
8. Mengubah bagian `Widget build()` pada _class_ `MyHomePage` dengan kode berikut.
    ```dart
    ...
    class MyHomePage extends StatelessWidget {
      ...

      @override
      Widget build(BuildContext context) {
        // Scaffold menyediakan struktur dasar halaman dengan AppBar dan body.
        return Scaffold(
          // AppBar adalah bagian atas halaman yang menampilkan judul.
          appBar: AppBar(
            // Judul aplikasi "Mental Health Tracker" dengan teks putih dan tebal.
            title: const Text(
              'Shield',
              style: TextStyle(
                color: Colors.white,
                fontWeight: FontWeight.bold,
              ),
            ),
            // Warna latar belakang AppBar diambil dari skema warna tema aplikasi.
            backgroundColor: Theme.of(context).colorScheme.primary,
          ),
          // Body halaman dengan padding di sekelilingnya.
          body: Padding(
            padding: const EdgeInsets.all(16.0),
            // Menyusun widget secara vertikal dalam sebuah kolom.
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.center,
              children: [
                // Row untuk menampilkan 3 InfoCard secara horizontal.
                Row(
                  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                  children: [
                    InfoCard(title: 'NPM', content: npm),
                    InfoCard(title: 'Name', content: name),
                    InfoCard(title: 'Class', content: className),
                  ],
                ),

                // Memberikan jarak vertikal 16 unit.
                const SizedBox(height: 16.0),

                // Menempatkan widget berikutnya di tengah halaman.
                Center(
                  child: Column(
                    // Menyusun teks dan grid item secara vertikal.

                    children: [
                      // Menampilkan teks sambutan dengan gaya tebal dan ukuran 18.
                      const Padding(
                        padding: EdgeInsets.only(top: 16.0),
                        child: Text(
                          'Welcome to Shield',
                          style: TextStyle(
                            fontWeight: FontWeight.bold,
                            fontSize: 18.0,
                          ),
                        ),
                      ),

                      // Grid untuk menampilkan ItemCard dalam bentuk grid 3 kolom.
                      GridView.count(
                        primary: true,
                        padding: const EdgeInsets.all(20),
                        crossAxisSpacing: 10,
                        mainAxisSpacing: 10,
                        crossAxisCount: 3,
                        // Agar grid menyesuaikan tinggi kontennya.
                        shrinkWrap: true,

                        // Menampilkan ItemCard untuk setiap item dalam list items.
                        children: items.map((ItemHomepage item) {
                          return ItemCard(item);
                        }).toList(),
                      ),
                    ],
                  ),
                ),
              ],
            ),
          ),
        );
      }
    }
    ...
    ```
9. Melakukan `add`-`commit`-`push` ke GitHub.

## Tugas 8

### Apa kegunaan `const` di Flutter? Jelaskan apa keuntungan ketika menggunakan `const` pada kode Flutter. Kapan sebaiknya kita menggunakan `const`, dan kapan sebaiknya tidak digunakan?

`const` digunakan untuk membuat objek yang bersifat _immutable_ dan dapat diinisialisasi pada waktu kompilasi. Keuntungan menggunakan `const` adalah efisiensi memori, karena objek yang dideklarasikan sebagai `const` hanya dibuat sekali dan dapat digunakan kembali tanpa alokasi memori tambahan. `const` sebaiknya digunakan ketika kita yakin nilai dari objek tidak akan berubah selama _runtime_ dan sebaiknya tidak digunakan ketika nilai objek dapat berubah atau dihitung ulang selama runtime.
 
### Jelaskan dan bandingkan penggunaan _Column_ dan _Row_ pada Flutter. Berikan contoh implementasi dari masing-masing layout widget ini!

_Column_ digunakan untuk menyusun widget secara vertikal, sedangkan _Row_ digunakan untuk menyusun widget secara horizontal. 

Contoh implementasi _Column_:
```dart
Column(
  children: [
    Text('Item 1'),
    Text('Item 2'),
    Text('Item 3'),
  ],
)
```

Contoh implementasi _Row_:
```dart
Row(
  children: [
    Icon(Icons.star),
    Text('Starred'),
  ],
)
```
 
### Sebutkan apa saja elemen input yang kamu gunakan pada halaman _form_ yang kamu buat pada tugas kali ini. Apakah terdapat elemen input Flutter lain yang tidak kamu gunakan pada tugas ini? Jelaskan!

Elemen input yang saya gunakan adalah `TextFormField` untuk memasukkan nama, harga, jumlah, dan deskripsi produk. Elemen input lain yang tidak digunakan adalah `Checkbox`, `Radio`, `Switch`, `Slider`, dan `DropdownButton`. 

### Bagaimana cara kamu mengatur tema (theme) dalam aplikasi Flutter agar aplikasi yang dibuat konsisten? Apakah kamu mengimplementasikan tema pada aplikasi yang kamu buat?

Untuk mengatur tema dalam aplikasi Flutter, kita dapat mendefinisikan `ThemeData` di dalam widget `MaterialApp`. Dalam aplikasi ini, saya mengimplementasikan tema dengan mengatur `colorScheme` pada `ThemeData`, yang digunakan untuk menentukan warna utama, sekunder, warna latar belakang, dan teks.
 
### Bagaimana cara kamu menangani navigasi dalam aplikasi dengan banyak halaman pada Flutter?

Saya menggunakan `Navigator` untuk menangani navigasi antar halaman dan menggunakan fungsi `pushReplacement()` untuk mengganti halaman sebelumnya dengan halaman sekarang.

## Tugas 9

### Jelaskan mengapa kita perlu membuat model untuk melakukan pengambilan ataupun pengiriman data JSON? Apakah akan terjadi error jika kita tidak membuat model terlebih dahulu?

Model diperlukan dalam penanganan data JSON untuk memastikan struktur data yang konsisten. Model membantu validasi data dan autocomplete. Tanpa model, tidak akan terjadi error tetapi akan meningkatkan risiko bug dan membuat debugging lebih sulit.

### Jelaskan fungsi dari library _http_ yang sudah kamu implementasikan pada tugas ini

Library _http_ berfungsi sebagai melakukan HTTP requests ke server. Ini memungkinkan aplikasi untuk mengirim dan menerima data dari server Django.

### Jelaskan fungsi dari _CookieRequest_ dan jelaskan mengapa _instance CookieRequest_ perlu untuk dibagikan ke semua komponen di aplikasi Flutter.

_CookieRequest_ berfungsi untuk mengelola state autentikasi dan session cookies di seluruh aplikasi. Instance _CookieRequest_ perlu dibagikan ke semua komponen agar state login dan cookies dapat diakses secara konsisten di seluruh aplikasi. 

### Jelaskan mekanisme pengiriman data mulai dari input hingga dapat ditampilkan pada Flutter.

Mekanisme pengiriman data dimulai dari user input di Flutter, data tersebut dikumpulkan dan dikonversi ke format JSON. Data terus dikirim ke Django melalui HTTP request. Server memproses request, melakukan operasi database yang diperlukan, dan mengirim response. Flutter menerima response, mengkonversi JSON ke model, dan memperbarui UI untuk menampilkan data.

### Jelaskan mekanisme autentikasi dari login, register, hingga logout. Mulai dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.

Proses autentikasi dimulai saat pengguna memasukkan credentials di form Flutter. Data dikirim ke endpoint Django melalui HTTP POST request. Django memverifikasi credentials, membuat session, dan mengirim response dengan token/cookie. Flutter menyimpan token ini di CookieRequest untuk requests selanjutnya. Untuk logout, Flutter mengirim request ke endpoint logout Django, yang menghapus session, kemudian Flutter membersihkan token lokal dan menavigasi ke halaman login.

### Implementasi Checklist

1. Membuat app baru bernama `authentication` pada project Django yang telah dibuat sebelumnya.

2. Install `django-cors-headers` dengan perintah `pip install django-cors-headers`.

3. Ubah file `settings.py` menjadi seperti berikut.
    ```python
    ...
    ALLOWED_HOSTS = [..., ..., "10.0.2.2"]
    ...
    INSTALLED_APPS = [
        ...,
        'authentication',
        'corsheaders',
    ]
    ...
    MIDDLEWARE = [
        ...,
        'corsheaders.middleware.CorsMiddleware',
    ]
    ...
    CORS_ALLOW_ALL_ORIGINS = True
    CORS_ALLOW_CREDENTIALS = True
    CSRF_COOKIE_SECURE = True
    SESSION_COOKIE_SECURE = True
    CSRF_COOKIE_SAMESITE = 'None'
    SESSION_COOKIE_SAMESITE = 'None'
    ...
    ```

4. Membuat method login, register, dan logout pada `authentication/views.py`.
    ```python
    from django.contrib.auth import authenticate, login as auth_login
    from django.http import JsonResponse
    from django.views.decorators.csrf import csrf_exempt
    from django.contrib.auth.models import User
    import json
    from django.contrib.auth import logout as auth_logout

    @csrf_exempt
    def login(request):
        username = request.POST['username']
        password = request.POST['password']
        user = authenticate(username=username, password=password)
        if user is not None:
            if user.is_active:
                auth_login(request, user)
                # Status login sukses.
                return JsonResponse({
                    "username": user.username,
                    "status": True,
                    "message": "Login sukses!"
                    # Tambahkan data lainnya jika ingin mengirim data ke Flutter.
                }, status=200)
            else:
                return JsonResponse({
                    "status": False,
                    "message": "Login gagal, akun dinonaktifkan."
                }, status=401)

        else:
            return JsonResponse({
                "status": False,
                "message": "Login gagal, periksa kembali email atau kata sandi."
            }, status=401)
            
    @csrf_exempt
    def register(request):
        if request.method == 'POST':
            data = json.loads(request.body)
            username = data['username']
            password1 = data['password1']
            password2 = data['password2']

            # Check if the passwords match
            if password1 != password2:
                return JsonResponse({
                    "status": False,
                    "message": "Passwords do not match."
                }, status=400)
            
            # Check if the username is already taken
            if User.objects.filter(username=username).exists():
                return JsonResponse({
                    "status": False,
                    "message": "Username already exists."
                }, status=400)
            
            # Create the new user
            user = User.objects.create_user(username=username, password=password1)
            user.save()
            
            return JsonResponse({
                "username": user.username,
                "status": 'success',
                "message": "User created successfully!"
            }, status=200)
        
        else:
            return JsonResponse({
                "status": False,
                "message": "Invalid request method."
            }, status=400)
            
    @csrf_exempt
    def logout(request):
        username = request.user.username

        try:
            auth_logout(request)
            return JsonResponse({
                "username": username,
                "status": True,
                "message": "Logout berhasil!"
            }, status=200)
        except:
            return JsonResponse({
            "status": False,
            "message": "Logout gagal."
            }, status=401)
    ```

5. Menambahkan URL _routing_ method-method tersebut pada file `urls.py`.

6. Install package berikut.
    ```bash
    flutter pub add provider
    flutter pub add pbp_django_auth
    flutter pub add http
    ```
  
7. Ubah file `main.dart` menjadi seperti berikut.
    ```dart
    import 'package:flutter/material.dart';
    import 'package:shield_mobile/screens/login.dart';
    import 'package:shield_mobile/screens/menu.dart';
    import 'package:pbp_django_auth/pbp_django_auth.dart';
    import 'package:provider/provider.dart';

    void main() {
      runApp(const MyApp());
    }

    class MyApp extends StatelessWidget {
      const MyApp({super.key});

      @override
      Widget build(BuildContext context) {
        return Provider(
          create: (_) {
            CookieRequest request = CookieRequest();
            return request;
          },
          child: MaterialApp(
            title: 'Shield',
            theme: ThemeData(
              useMaterial3: true,
              colorScheme: ColorScheme.fromSwatch(
                primarySwatch: Colors.deepPurple,
              ).copyWith(secondary: Colors.deepPurple[400]),
            ),
            home: const LoginPage(),
          ),
        );
      }
    }
    ```

8. Buat file `login.dart` pada folder `screens`.
    ```dart
    import 'package:shield_mobile/screens/menu.dart';
    import 'package:flutter/material.dart';
    import 'package:pbp_django_auth/pbp_django_auth.dart';
    import 'package:provider/provider.dart';
    import 'package:shield_mobile/screens/register.dart';

    void main() {
      runApp(const LoginApp());
    }

    class LoginApp extends StatelessWidget {
      const LoginApp({super.key});

      @override
      Widget build(BuildContext context) {
        return MaterialApp(
          title: 'Login',
          theme: ThemeData(
            useMaterial3: true,
            colorScheme: ColorScheme.fromSwatch(
              primarySwatch: Colors.deepPurple,
            ).copyWith(secondary: Colors.deepPurple[400]),
          ),
          home: const LoginPage(),
        );
      }
    }

    class LoginPage extends StatefulWidget {
      const LoginPage({super.key});

      @override
      State<LoginPage> createState() => _LoginPageState();
    }

    class _LoginPageState extends State<LoginPage> {
      final TextEditingController _usernameController = TextEditingController();
      final TextEditingController _passwordController = TextEditingController();

      @override
      Widget build(BuildContext context) {
        final request = context.watch<CookieRequest>();

        return Scaffold(
          appBar: AppBar(
            title: const Text('Login'),
          ),
          body: Center(
            child: SingleChildScrollView(
              padding: const EdgeInsets.all(16.0),
              child: Card(
                elevation: 8,
                shape: RoundedRectangleBorder(
                  borderRadius: BorderRadius.circular(12.0),
                ),
                child: Padding(
                  padding: const EdgeInsets.all(20.0),
                  child: Column(
                    mainAxisSize: MainAxisSize.min,
                    children: [
                      const Text(
                        'Login',
                        style: TextStyle(
                          fontSize: 24.0,
                          fontWeight: FontWeight.bold,
                        ),
                      ),
                      const SizedBox(height: 30.0),
                      TextField(
                        controller: _usernameController,
                        decoration: const InputDecoration(
                          labelText: 'Username',
                          hintText: 'Enter your username',
                          border: OutlineInputBorder(
                            borderRadius: BorderRadius.all(Radius.circular(12.0)),
                          ),
                          contentPadding:
                              EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                        ),
                      ),
                      const SizedBox(height: 12.0),
                      TextField(
                        controller: _passwordController,
                        decoration: const InputDecoration(
                          labelText: 'Password',
                          hintText: 'Enter your password',
                          border: OutlineInputBorder(
                            borderRadius: BorderRadius.all(Radius.circular(12.0)),
                          ),
                          contentPadding:
                              EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                        ),
                        obscureText: true,
                      ),
                      const SizedBox(height: 24.0),
                      ElevatedButton(
                        onPressed: () async {
                          String username = _usernameController.text;
                          String password = _passwordController.text;

                          // Cek kredensial
                          // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
                          // Untuk menyambungkan Android emulator dengan Django pada localhost,
                          // gunakan URL http://10.0.2.2/
                          final response = await request
                              .login("http://127.0.0.1:8000/auth/login/", {
                            'username': username,
                            'password': password,
                          });

                          if (request.loggedIn) {
                            String message = response['message'];
                            String uname = response['username'];
                            if (context.mounted) {
                              Navigator.pushReplacement(
                                context,
                                MaterialPageRoute(
                                    builder: (context) => MyHomePage()),
                              );
                              ScaffoldMessenger.of(context)
                                ..hideCurrentSnackBar()
                                ..showSnackBar(
                                  SnackBar(
                                      content:
                                          Text("$message Selamat datang, $uname.")),
                                );
                            }
                          } else {
                            if (context.mounted) {
                              showDialog(
                                context: context,
                                builder: (context) => AlertDialog(
                                  title: const Text('Login Gagal'),
                                  content: Text(response['message']),
                                  actions: [
                                    TextButton(
                                      child: const Text('OK'),
                                      onPressed: () {
                                        Navigator.pop(context);
                                      },
                                    ),
                                  ],
                                ),
                              );
                            }
                          }
                        },
                        style: ElevatedButton.styleFrom(
                          foregroundColor: Colors.white,
                          minimumSize: Size(double.infinity, 50),
                          backgroundColor: Theme.of(context).colorScheme.primary,
                          padding: const EdgeInsets.symmetric(vertical: 16.0),
                        ),
                        child: const Text('Login'),
                      ),
                      const SizedBox(height: 36.0),
                      GestureDetector(
                        onTap: () {
                          Navigator.push(
                            context,
                            MaterialPageRoute(
                                builder: (context) => const RegisterPage()),
                          );
                        },
                        child: Text(
                          'Don\'t have an account? Register',
                          style: TextStyle(
                            color: Theme.of(context).colorScheme.primary,
                            fontSize: 16.0,
                          ),
                        ),
                      ),
                    ],
                  ),
                ),
              ),
            ),
          ),
        );
      }
    }
    ```

9. Buat file `register.dart` pada folder `screens`.
    ```dart
    import 'dart:convert';
    import 'package:flutter/material.dart';
    import 'package:shield_mobile/screens/login.dart';
    import 'package:pbp_django_auth/pbp_django_auth.dart';
    import 'package:provider/provider.dart';

    class RegisterPage extends StatefulWidget {
      const RegisterPage({super.key});

      @override
      State<RegisterPage> createState() => _RegisterPageState();
    }

    class _RegisterPageState extends State<RegisterPage> {
      final _usernameController = TextEditingController();
      final _passwordController = TextEditingController();
      final _confirmPasswordController = TextEditingController();

      @override
      Widget build(BuildContext context) {
        final request = context.watch<CookieRequest>();
        return Scaffold(
          appBar: AppBar(
            title: const Text('Register'),
            leading: IconButton(
              icon: const Icon(Icons.arrow_back),
              onPressed: () {
                Navigator.pop(context);
              },
            ),
          ),
          body: Center(
            child: SingleChildScrollView(
              padding: const EdgeInsets.all(16.0),
              child: Card(
                elevation: 8,
                shape: RoundedRectangleBorder(
                  borderRadius: BorderRadius.circular(12.0),
                ),
                child: Padding(
                  padding: const EdgeInsets.all(20.0),
                  child: Column(
                    mainAxisSize: MainAxisSize.min,
                    children: <Widget>[
                      const Text(
                        'Register',
                        style: TextStyle(
                          fontSize: 24.0,
                          fontWeight: FontWeight.bold,
                        ),
                      ),
                      const SizedBox(height: 30.0),
                      TextFormField(
                        controller: _usernameController,
                        decoration: const InputDecoration(
                          labelText: 'Username',
                          hintText: 'Enter your username',
                          border: OutlineInputBorder(
                            borderRadius: BorderRadius.all(Radius.circular(12.0)),
                          ),
                          contentPadding:
                              EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                        ),
                        validator: (value) {
                          if (value == null || value.isEmpty) {
                            return 'Please enter your username';
                          }
                          return null;
                        },
                      ),
                      const SizedBox(height: 12.0),
                      TextFormField(
                        controller: _passwordController,
                        decoration: const InputDecoration(
                          labelText: 'Password',
                          hintText: 'Enter your password',
                          border: OutlineInputBorder(
                            borderRadius: BorderRadius.all(Radius.circular(12.0)),
                          ),
                          contentPadding:
                              EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                        ),
                        obscureText: true,
                        validator: (value) {
                          if (value == null || value.isEmpty) {
                            return 'Please enter your password';
                          }
                          return null;
                        },
                      ),
                      const SizedBox(height: 12.0),
                      TextFormField(
                        controller: _confirmPasswordController,
                        decoration: const InputDecoration(
                          labelText: 'Confirm Password',
                          hintText: 'Confirm your password',
                          border: OutlineInputBorder(
                            borderRadius: BorderRadius.all(Radius.circular(12.0)),
                          ),
                          contentPadding:
                              EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                        ),
                        obscureText: true,
                        validator: (value) {
                          if (value == null || value.isEmpty) {
                            return 'Please confirm your password';
                          }
                          return null;
                        },
                      ),
                      const SizedBox(height: 24.0),
                      ElevatedButton(
                        onPressed: () async {
                          String username = _usernameController.text;
                          String password1 = _passwordController.text;
                          String password2 = _confirmPasswordController.text;

                          // Cek kredensial
                          // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
                          // Untuk menyambungkan Android emulator dengan Django pada localhost,
                          // gunakan URL http://10.0.2.2/
                          final response = await request.postJson(
                              "http://127.0.0.1:8000/auth/register/",
                              jsonEncode({
                                "username": username,
                                "password1": password1,
                                "password2": password2,
                              }));
                          if (context.mounted) {
                            if (response['status'] == 'success') {
                              ScaffoldMessenger.of(context).showSnackBar(
                                const SnackBar(
                                  content: Text('Successfully registered!'),
                                ),
                              );
                              Navigator.pushReplacement(
                                context,
                                MaterialPageRoute(
                                    builder: (context) => const LoginPage()),
                              );
                            } else {
                              ScaffoldMessenger.of(context).showSnackBar(
                                const SnackBar(
                                  content: Text('Failed to register!'),
                                ),
                              );
                            }
                          }
                        },
                        style: ElevatedButton.styleFrom(
                          foregroundColor: Colors.white,
                          minimumSize: Size(double.infinity, 50),
                          backgroundColor: Theme.of(context).colorScheme.primary,
                          padding: const EdgeInsets.symmetric(vertical: 16.0),
                        ),
                        child: const Text('Register'),
                      ),
                    ],
                  ),
                ),
              ),
            ),
          ),
        );
      }
    }
    ```

10. Membuat file `product.dart` pada folder `lib/models`.
    ```dart
        // To parse this JSON data, do
    //
    //     final product = productFromJson(jsonString);

    import 'dart:convert';

    List<Product> productFromJson(String str) => List<Product>.from(json.decode(str).map((x) => Product.fromJson(x)));

    String productToJson(List<Product> data) => json.encode(List<dynamic>.from(data.map((x) => x.toJson())));

    class Product {
        String model;
        String pk;
        Fields fields;

        Product({
            required this.model,
            required this.pk,
            required this.fields,
        });

        factory Product.fromJson(Map<String, dynamic> json) => Product(
            model: json["model"],
            pk: json["pk"],
            fields: Fields.fromJson(json["fields"]),
        );

        Map<String, dynamic> toJson() => {
            "model": model,
            "pk": pk,
            "fields": fields.toJson(),
        };
    }

    class Fields {
        int user;
        String name;
        int price;
        String description;

        Fields({
            required this.user,
            required this.name,
            required this.price,
            required this.description,
        });

        factory Fields.fromJson(Map<String, dynamic> json) => Fields(
            user: json["user"],
            name: json["name"],
            price: json["price"],
            description: json["description"],
        );

        Map<String, dynamic> toJson() => {
            "user": user,
            "name": name,
            "price": price,
            "description": description,
        };
    }
    ```
  
11. Tambahkan kode berikut pada file `android/app/src/main/AndroidManifest.xml`.
    ```xml
    ...
        <application>
        ...
        </application>
        <!-- Required to fetch data from the Internet. -->
        <uses-permission android:name="android.permission.INTERNET" />
    ...
    ```
  
12. Buat file `list_product.dart` pada folder `screens`.
    ```dart
    import 'package:flutter/material.dart';
    import 'package:pbp_django_auth/pbp_django_auth.dart';
    import 'package:provider/provider.dart';
    import 'package:shield_mobile/models/product.dart';
    import 'package:shield_mobile/widgets/left_drawer.dart';

    class ProductPage extends StatefulWidget {
      const ProductPage({super.key});

      @override
      State<ProductPage> createState() => _ProductPageState();
    }

    class _ProductPageState extends State<ProductPage> {
      Future<List<Product>> fetchProduct(CookieRequest request) async {
        // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
        final response = await request.get('http://127.0.0.1:8000/json/');
        
        // Melakukan decode response menjadi bentuk json
        var data = response;
        
        // Melakukan konversi data json menjadi object Product
        List<Product> listProduct = [];
        for (var d in data) {
          if (d != null) {
            listProduct.add(Product.fromJson(d));
          }
        }
        return listProduct;
      }

      @override
      Widget build(BuildContext context) {
        final request = context.watch<CookieRequest>();
        return Scaffold(
          appBar: AppBar(
            title: const Text('Product List'),
          ),
          drawer: const LeftDrawer(),
          body: FutureBuilder(
            future: fetchProduct(request),
            builder: (context, AsyncSnapshot snapshot) {
              if (snapshot.data == null) {
                return const Center(child: CircularProgressIndicator());
              } else {
                if (!snapshot.hasData) {
                  return const Column(
                    children: [
                      Text(
                        'Belum ada data Product pada shield.',
                        style: TextStyle(fontSize: 20, color: Color(0xff59A5D8)),
                      ),
                      SizedBox(height: 8),
                    ],
                  );
                } else {
                  return ListView.builder(
                    itemCount: snapshot.data!.length,
                    itemBuilder: (_, index) => Container(
                      margin:
                          const EdgeInsets.symmetric(horizontal: 16, vertical: 12),
                      padding: const EdgeInsets.all(20.0),
                      child: Column(
                        mainAxisAlignment: MainAxisAlignment.start,
                        crossAxisAlignment: CrossAxisAlignment.start,
                        children: [
                          Text(
                            "${snapshot.data![index].fields.name}",
                            style: const TextStyle(
                              fontSize: 18.0,
                              fontWeight: FontWeight.bold,
                            ),
                          ),
                          const SizedBox(height: 10),
                          Text("${snapshot.data![index].fields.price}"),
                          const SizedBox(height: 10),
                          Text("${snapshot.data![index].fields.description}")
                        ],
                      ),
                    ),
                  );
                }
              }
            },
          ),
        );
      }
    }
    ```
  
13. Ubah `left_drawer.dart` menjadi seperti berikut.
    ```dart
    ...
    ListTile(
        leading: const Icon(Icons.add_shopping_cart_rounded),
        title: const Text('Daftar Produk'),
        onTap: () {
            // Route menu ke halaman product
            Navigator.push(
                context,
                MaterialPageRoute(builder: (context) => const ProductPage()),
            );
        },
    ),
    ...
    ```

14. Ubah `product_card.dart` menjadi seperti berikut.
    ```dart
    ...
    else if (item.name == "Lihat Daftar Produk") {
        Navigator.push(context,
            MaterialPageRoute(
                builder: (context) => const ProductPage()
            ),
        );
    } else if (item.name == "Logout") {
        final response = await request.logout(
            // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
            "http://127.0.0.1:8000/auth/logout/");
        String message = response["message"];
        if (context.mounted) {
            if (response['status']) {
                String uname = response["username"];
                ScaffoldMessenger.of(context).showSnackBar(SnackBar(
                    content: Text("$message Sampai jumpa, $uname."),
                ));
                Navigator.pushReplacement(
                    context,
                    MaterialPageRoute(builder: (context) => const LoginPage()),
                );
            } else {
                ScaffoldMessenger.of(context).showSnackBar(
                    SnackBar(
                        content: Text(message),
                    ),
                );
            }
        }
    }
    ...
    ```

15. Buat method pada `main/views.py`
    ```python
    from django.views.decorators.csrf import csrf_exempt
    import json
    from django.http import JsonResponse
    ...
    @csrf_exempt
    def create_product_flutter(request):
        if request.method == 'POST':

            data = json.loads(request.body)
            new_product = Product.objects.create(
                user=request.user,
                name=data["name"],
                price=int(data["price"]),
                description=data["description"]
            )

            new_product.save()

            return JsonResponse({"status": "success"}, status=200)
        else:
            return JsonResponse({"status": "error"}, status=401)
    ```

16. Tambahkan URL _routing_ method tersebut..

17. Ubah `product_form.dart`
    ```dart
    onPressed: () async {
        if (_formKey.currentState!.validate()) {
            // Kirim ke Django dan tunggu respons
            // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
            final response = await request.postJson(
                "http://127.0.0.1:8000/create-flutter/",
                jsonEncode(<String, String>{
                    'name': _name,
                    'price': _price.toString(),
                    'description': _description,
                // TODO: Sesuaikan field data sesuai dengan aplikasimu
                }),
            );
            if (context.mounted) {
                if (response['status'] == 'success') {
                    ScaffoldMessenger.of(context)
                        .showSnackBar(const SnackBar(
                    content: Text("Product baru berhasil disimpan!"),
                    ));
                    Navigator.pushReplacement(
                        context,
                        MaterialPageRoute(builder: (context) => MyHomePage()),
                    );
                } else {
                    ScaffoldMessenger.of(context)
                        .showSnackBar(const SnackBar(
                        content:
                            Text("Terdapat kesalahan, silakan coba lagi."),
                    ));
                }
            }
        }
    },
    ```

18. Melakukan `add`-`commit`-`push` ke GitHub.