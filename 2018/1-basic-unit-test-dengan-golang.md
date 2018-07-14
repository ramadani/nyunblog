# Unit Test dengan Golang

Unit Testing adalah sebuah level pengujian perangkat lunak dimana unit-unit individu atau komponen-komponen dari sebuah perangkat lunak diuji. Sebuah unit adalah bagian terkecil yang dapat diuji dari perangkat lunak, biasanya memiliki satu atau beberapa input dan biasanya juga hanya memiliki satu output yang dihasilkan. Dalam object-oriented programming, unit terkecil adalah sebuah method, yang mungkin milik base/super class, abstract class atau child class.

(Gambar hirarki level pengujian)

Manfaat dengan adanya unit testing dapat meningkatkan keyakinan pada perubahan maupun maintaining code. Jika unit test ditulis dengan baik dan jika itu dijalankan setiap kali terdapat perubahan pada code, kita akan dapat segera menemukan setiap *defects* yang diperlihatkan karena adanya perubahan pada code. Code yang ditulis juga akan lebih reusable karena untuk unit test, code yang dibuat harus modular. Selain itu juga dengan adanya unit test, proses development bisa lebih cepat dan cost yang dikeluarkan untuk memperbaiki *defects* bisa dikurangi.

## Testing pada Golang

Golang memiliki sebuah *built-in testing command* yang disebut `go test` dan package `testing` yang berisikan banyak sekali tools untuk keperluan unit testing sehingga keduanya dapat digabungkan untuk memberikan pengalaman pengujian yang minimal namun lengkap.

## Referensi

* [Unit Testing](http://softwaretestingfundamentals.com/unit-testing/)