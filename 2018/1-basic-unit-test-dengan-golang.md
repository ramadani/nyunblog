# Tingkatkan Code Quality dengan Unit Testing pada Go

![roman-mager-59976-unsplash.jpg](/2018/1/roman-mager-59976-unsplash.jpg)
*Photo by Roman Mager on Unsplash*

*Programming is not easy;* bahkan programmer terbaik pun tidak selalu mampu menulis program yang bekerja persis seperti yang diharapkan. Oleh karena itu bagian penting pada proses pengembangan perangkat lunak adalah pengujian. Menulis *tests* adalah cara yang baik untuk memastikan kualitas dan meningkatkan *reliability* pada *code* yang kita buat. Terdapat beberapa jenis pengujian pada proses pengembangan perangkat lunak, salah satunya adalah Unit Testing.

Unit Testing adalah sebuah level pengujian perangkat lunak dimana unit-unit individu atau komponen-komponen dari sebuah perangkat lunak diuji. Sebuah unit adalah bagian terkecil yang dapat diuji dari perangkat lunak, biasanya memiliki satu atau beberapa input dan biasanya juga hanya memiliki satu output yang dihasilkan. Dalam object-oriented programming, unit terkecil adalah sebuah method, yang mungkin milik base/super class, abstract class atau child class.

![1_S-WQ9KwM7kkmwKWy41SPYw.png](/2018/1/1_S-WQ9KwM7kkmwKWy41SPYw.png)

## Unit Testing pada Go

Membuat Unit Testing dengan Go sangat mudah. By default kamu tidak perlu menginstall tools yang diperlukan untuk membuat dan menjalankan testing, karena Go sudah memiliki package `testing` yang ada didalamnya dan sebuah *built-in testing command* yang disebut `go test` untuk menjalankan tests yang telah dibuat.

## Kesimpulan

Manfaat dengan adanya unit testing dapat meningkatkan keyakinan pada perubahan maupun *maintaining code*. Jika unit test ditulis dengan baik dan jika itu dijalankan setiap kali terdapat perubahan pada *code*, kita akan dapat segera menemukan setiap *defects* yang diperlihatkan karena adanya perubahan pada *code*. **code** yang ditulis juga akan lebih *reusable* karena untuk unit test, **code** yang dibuat harus modular. Selain itu juga dengan adanya unit test, proses development bisa lebih cepat dan cost yang dikeluarkan untuk memperbaiki *defects* bisa dikurangi.

## Referensi

* [Software Testing Fundamental - Unit Testing](http://softwaretestingfundamentals.com/unit-testing/)
* [Dasar Pemrograman Golang - Unit Test](https://blog.alexellis.io/golang-writing-unit-tests/)