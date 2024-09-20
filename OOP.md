# Pengenalan Object-Oriented Programming (OOP) dalam JavaScript

Object-Oriented Programming (OOP) adalah paradigma pemrograman yang berfokus pada objek. Objek adalah entitas yang berisi data (property) dan perilaku (method). OOP memungkinkan kita untuk membuat kode yang lebih modular, mudah di-maintain, dan dapat digunakan kembali.

JavaScript mendukung OOP melalui konsep **class**, **object**, **inheritance**, **encapsulation**, dan **polymorphism**.

## 1. Class dan Object (Instance)

  **Class** adalah template atau blueprint untuk membuat object. **Object** adalah instansiasi dari class yang berisi property dan method.
  ```javascript
  // Membuat class untuk mobil
  class Mobil {
    constructor(merk, model, tahun) {
      this.merk = merk;
      this.model = model;
      this.tahun = tahun;
    }

    infoMobil() {
      return `${this.merk} ${this.model} keluaran tahun ${this.tahun}`;
    }
  }

  // Membuat object dari class Mobil
  const mobil1 = new Mobil('Toyota', 'Avanza', 2020);
  console.log(mobil1.infoMobil()); // Output: Toyota Avanza keluaran tahun 2020
  ```

## 2. Prinsip dalam OOP
  ## a. Inheritance (Pewarisan)
  Inheritance adalah konsep di mana sebuah class bisa mewarisi property dan method dari class lain. Dalam JavaScript, kita bisa menggunakan keyword **extends**.

  ```javascript
  class Kendaraan {
    constructor(jenis, merk) {
      this.jenis = jenis;
      this.merk = merk;
    }

    infoKendaraan() {
      return `Ini adalah kendaraan jenis ${this.jenis} merk ${this.merk}.`;
    }
  }

  class Mobil extends Kendaraan {
    constructor(merk, model, tahun) {
      super('Mobil', merk); // memanggil constructor dari class Kendaraan
      this.model = model;
      this.tahun = tahun;
    }

    infoMobil() {
      return `${this.merk} ${this.model} keluaran tahun ${this.tahun}`;
    }
  }

  const mobil3 = new Mobil('Suzuki', 'Ertiga', 2022);
  console.log(mobil3.infoKendaraan()); // Output: Ini adalah kendaraan jenis Mobil merk Suzuki.
  console.log(mobil3.infoMobil()); // Output: Suzuki Ertiga keluaran tahun 2022
  ```

  ## b. Encapsulation (Pembungkus)
  Encapsulation atau pembungkus merupakan konsep mengenai pengikatan data atau metode berbeda yang disatukan menjadi satu unit data agar tidak dapat diakses secara sembarangan oleh program lain. Encapsulation dapat mempermudah dalam pembacaan kode karena informasi yang disajikan tidak perlu dibaca secara rinci. Dalam konsep encapsulation terdapat hak akses atau yang biasa disebut dengan access modifier yang terdiri dari private, protected, dan public.

  Encapsulation adalah prinsip di mana data (properti atau method) suatu objek disembunyikan dan hanya dapat diakses melalui method tertentu. Dalam JavaScript, kita bisa menggunakan **variabel private** dengan menggunakan awalan #.

  ```javascript
  class Mobil {
    #kilometer; // Properti private
    
    constructor(merk, model, tahun) {
      this.merk = merk;
      this.model = model;
      this.tahun = tahun;
      this.#kilometer = 0;
    }

    tambahKilometer(km) {
      if (km > 0) {
        this.#kilometer += km;
      }
    }

    getKilometer() {
      return this.#kilometer;
    }
  }

  const mobil2 = new Mobil('Honda', 'Civic', 2021);
  mobil2.tambahKilometer(150);
  console.log(mobil2.getKilometer()); // Output: 150
  ```
  ## c. Polymorphism 
  Polymorphism adalah konsep dimana suatu objek yang berbeda dapat diakses melalui interface yang sama. Dalam konsep polymorphism menggunakan dua method yaitu method overriding dan method overloading.

  Polimorfisme memungkinkan kita menggunakan **method yang sama dengan cara yang berbeda** di class yang berbeda. (atau meng-overide methd yang sudah ada dari parent)

  ```javascript
  class Kendaraan {
    infoKendaraan() {
      return "Ini adalah kendaraan.";
    }
  }

  class Mobil extends Kendaraan {
    infoKendaraan() {
      return "Ini adalah mobil.";
    }
  }

  class Motor extends Kendaraan {
    infoKendaraan() {
      return "Ini adalah motor.";
    }
  }

  const kendaraan1 = new Kendaraan();
  const mobil4 = new Mobil();
  const motor1 = new Motor();

  console.log(kendaraan1.infoKendaraan()); // Output: Ini adalah kendaraan.
  console.log(mobil4.infoKendaraan()); // Output: Ini adalah mobil.
  console.log(motor1.infoKendaraan()); // Output: Ini adalah motor.
  ```
  ## d. Abstraction (Abstraksi)
  Abstarction merupakan konsep dimana memungkinkan untuk memerintahkan suatu fungsi, tanpa harus mengetahui bagaimana fungsi tersebut bekerja. Konsep abstraction hanya menunjukkan hal penting kepada pengguna dan menyembunyikan detail internal. Abstraction dapat diilustrasikan sebagai suatu cetak biru (blueprint) atau prototype untuk menciptakan sebuah objek.

  ## sebelum abstraction

  ```javascript
  class KartuKredit {
    constructor(nama, nomor, cvv) {
      this.nama = nama;
      this.nomor = nomor;
      this.cvv = cvv;
    }

    prosesPembayaran(jumlah) {
      console.log(`Proses pembayaran ${jumlah} menggunakan Kartu Kredit ${this.nama}`);
    }
  }

  class PayPal {
    constructor(email) {
      this.email = email;
    }

    prosesPembayaran(jumlah) {
      console.log(`Proses pembayaran ${jumlah} menggunakan PayPal dengan email ${this.email}`);
    }
  }

  const kartu = new KartuKredit("John Doe", "1234 5678 9012 3456", "123");
  const paypal = new PayPal("john@example.com");

  kartu.prosesPembayaran(500000);
  paypal.prosesPembayaran(750000);
  ```

  ## sesudah abstraction
  ```javascript
  class Pembayaran {
    proses(jumlah) {
      throw new Error("Method proses() harus diimplementasikan!");
    }
  }

  class KartuKredit extends Pembayaran {
    constructor(nama, nomor, cvv) {
      super();
      this.nama = nama;
      this.nomor = nomor;
      this.cvv = cvv;
    }

    proses(jumlah) {
      console.log(`Proses pembayaran ${jumlah} menggunakan Kartu Kredit ${this.nama}`);
    }
  }

  class PayPal extends Pembayaran {
    constructor(email) {
      super();
      this.email = email;
    }

    proses(jumlah) {
      console.log(`Proses pembayaran ${jumlah} menggunakan PayPal dengan email ${this.email}`);
    }
  }

  class TransferBank extends Pembayaran {
    constructor(namaBank, nomorRekening) {
      super();
      this.namaBank = namaBank;
      this.nomorRekening = nomorRekening;
    }

    proses(jumlah) {
      console.log(`Proses pembayaran ${jumlah} melalui Transfer Bank ke ${this.namaBank}`);
    }
  }

  // Penggunaan abstraksi
  function prosesTransaksi(metodePembayaran, jumlah) {
    metodePembayaran.proses(jumlah);
  }

  const kartu = new KartuKredit("John Doe", "1234 5678 9012 3456", "123");
  const paypal = new PayPal("john@example.com");
  const transferBank = new TransferBank("BCA", "1234567890");

  prosesTransaksi(kartu, 500000);
  prosesTransaksi(paypal, 750000);
  prosesTransaksi(transferBank, 1000000);
  ```

  ## Penjelasan:
  Class Pembayaran: Sebagai class abstrak yang memiliki method proses(). Setiap class turunan harus mengimplementasikan method ini.
  KartuKredit, PayPal, TransferBank: Mengimplementasikan method proses() sesuai dengan logika masing-masing.
  prosesTransaksi(): Sebuah fungsi umum yang tidak perlu tahu detail dari metode pembayaran yang digunakan. Fungsi ini cukup memanggil method proses() dari object yang diberikan.







