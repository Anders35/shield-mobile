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