# Tingkatkan Code Quality dengan Unit Testing pada Go

![Photo by Roman Mager on Unsplash](/2018/1/roman-mager-59976-unsplash.jpg)
*Photo by Roman Mager on Unsplash*

*Programming is not easy;* bahkan programmer terbaik pun tidak selalu mampu menulis program yang bekerja persis seperti yang diharapkan. Oleh karena itu bagian penting pada proses pengembangan perangkat lunak adalah pengujian. Menulis *tests* adalah cara yang baik untuk memastikan kualitas dan meningkatkan *reliability* pada *code* yang kita buat. Terdapat beberapa jenis pengujian pada proses pengembangan perangkat lunak, salah satunya adalah Unit Testing.

Unit Testing adalah sebuah level pengujian perangkat lunak dimana unit-unit individu atau komponen-komponen dari sebuah perangkat lunak diuji. Sebuah unit adalah bagian terkecil yang dapat diuji dari perangkat lunak, biasanya memiliki satu atau beberapa input dan biasanya juga hanya memiliki satu output yang dihasilkan. Dalam *object-oriented programming*, unit terkecil adalah sebuah *method*, yang mungkin dimilik oleh base/super class, abstract class atau child class.

![Types of Testing](/2018/1/1_S-WQ9KwM7kkmwKWy41SPYw.png)

---

## Unit Testing pada Go

Membuat Unit Testing dengan Go sangat mudah. By default kamu tidak perlu menginstall *tools* yang diperlukan untuk membuat dan menjalankan testing, karena Go sudah memiliki package `testing` yang ada didalamnya dan sebuah *built-in testing command* yang disebut `go test` untuk menjalankan *tests* yang telah dibuat.

### Menulis Tests

Mari kita mulai dengan menggunakan contoh lingkaran, pada lingkaran kita dapat mencari panjang diameter, luas, dan kelilingnya. Berikut contoh *code* yang akan kita gunakan untuk membuat unit testing.

```go
package circle

import (
	"math"
)

type Circle struct {
	Radius float64
}

func (c Circle) Diameter() float64 {
	return 2 * c.Radius
}

func (c Circle) Area() float64 {
	return math.Pi * c.Radius * c.Radius
}

func (c Circle) Circumference() float64 {
	return math.Pi * c.Diameter()
}
```

Kemudian kita buat test untuk menguji code yang telah dibuat sebelumnya pada file yang terpisah. File test dapat berada pada *package* (circle) yang sama atau pada *package* (dan folder) yang berbeda. Dibawah ini merupakan unit testing untuk menguji luas lingkaran:

```go
package circle

import (
	"testing"
)

func TestArea(t *testing.T) {
	circle := Circle{Radius: 10}

	expected := 314.1592653589793
	actual := circle.Area()

	if actual != expected {
		t.Errorf("TestArea failed, expected: '%.2f', got: '%.2f'", expected, actual)
	}
}
```

Pada *test function* yang kita tulis memiliki karakteristik yaitu:

* Hanya memiliki 1 parameter bertipe `*testing.T`, dengan parameter tersebut kita bisa mengakses method-method untuk keperluan testing.
* Dimulai dengan kata `Test` lalu diikuti oleh kata atau *phrase* yang menunjukkan apa yang dilakukan pada pengujian tersebut dan dimulai dengan huruf besar. Contoh pada test tersebut adalah `TestArea`.
* Memanggil `t.Error` atau `t.Fail` untuk mengindikasikan sebuah kesalahan yang terjadi.
* Dapat menggunakan `t.Log` untuk melakukan *debugging* atau melihat informasi dari suatu nilai yang ada pada test.
* Harus disimpan pada file dengan *suffix* `_test.go`, misal `circle_test.go`.

### Menjalankan Tests

Untuk menjalankan *tests* sebuah *package* yang telah dibuat, terdapat 2 cara yaitu:

#### 1. Dalam folder yang sama

Cara ini menjalankan file apapun yang cocok dengan *packagename_test.go* pada folder yang diarahkan.

```bash
go test
```

#### 2. Berdasarkan *package*

Menjalankan test dengan *path* dimana package itu berada. Misal:

```bash
go test github.com/ramadani/go-unit-test/circle
```

Untuk melihat lebih detail *output* yang dihasilkan pada pengujian, kamu bisa menambahkan argumen `-v` dibelakang test command

```bash
go test -v

=== RUN   TestArea--- PASS: TestArea (0.00s)PASS
ok      path/to/your/sourcecode        0.010s
```

atau

```bash
go test -v github.com/ramadani/go-unit-test/circle

=== RUN   TestArea--- PASS: TestArea (0.00s)PASS
ok      github.com/ramadani/go-unit-tests/circle        0.010s
```

*Output* ketika terjadi kesalahan

```bash
=== RUN   TestArea--- FAIL: TestArea (0.00s)
        circle_test.go:14: TestArea failed, expected: '300.00', got: '314.16'
FAIL
exit status 1
FAIL    github.com/ramadani/go-unit-tests/circle        0.006s
```

### Test Coverage

> In computer science, test coverage is a measure used to describe the degree to which the source code of a program is executed when a particular test suite runs. A program with high test coverage, measured as a percentage, has had more of its source code executed during testing, which suggests it has a lower chance of containing undetected software bugs compared to a program with low test coverage. - [Wikipedia](https://en.wikipedia.org/wiki/Code_coverage)

Test Coverage bertujuan untuk mengukur berapa banyak *code* yang diuji. Pada `go test` tool telah memiliki *built-in code-coverage* sehingga untuk menggunakannya kita hanya tinggal menambahkan `-cover` pada *test command*.

```bash
go test -cover

PASS
coverage: 33.3% of statements
ok      github.com/ramadani/go-unit-tests/circle        0.005s
```

Bisa dilihat nilai dari *test coverage* yang dihasilkan adalah 33.3%, karena pada test yang dibuat kita hanya menguji untuk method `Area()` saja. Coba kita tambahkan test untuk method lainnya.

```go
package circle

import (
	"testing"
)

func TestDiameter(t *testing.T) {
	circle := Circle{Radius: 7}

	expected := 14.0
	actual := circle.Diameter()

	if actual != expected {
		t.Errorf("TestDiameter failed, expected: '%.2f', got: '%.2f'", expected, actual)
	}
}

func TestArea(t *testing.T) {
	circle := Circle{Radius: 10}

	expected := 314.1592653589793
	actual := circle.Area()

	if actual != expected {
		t.Errorf("TestArea failed, expected: '%.2f', got: '%.2f'", expected, actual)
	}
}

func TestCircumference(t *testing.T) {
	circle := Circle{Radius: 10}

	expected := 62.83185307179586
	actual := circle.Circumference()

	if actual != expected {
		t.Errorf("TestCircumference failed, expected: '%.2f', got: '%.2f'", expected, actual)
	}
}
```

Kemudian kita jalankan lagi *test command* seperti sebelumnya

```bash
go test -cover

PASS
coverage: 100.0% of statements
ok      github.com/ramadani/go-unit-tests/circle        0.006s
```

Dengan membuat test untuk method lainnya maka hasilnya 100.0%. Tapi *test coverage* tidak menjamin bahwa tests yang kita buat benar, karena nilai metrik yang dihasilkan dapat menyebabkan *misleading*. Kita perlu memastikan bahwa kita tidak hanya mengeksekusi *code* yang ada, tetapi kita lakukan verifikasi *behaviour* dan nilai *output* serta membuat test yang beragam.

## Kesimpulan

Untuk membuat testing, di Go sudah terdapat package `testing` dan `go test` *command* yang dapat memudahkanmu untuk memulai membuat testing karena tidak perlu lagi menginstallnya. Di Go juga sudah ada package testing lain, salah satunya **[testify](https://github.com/stretchr/testify)** yang dapat kamu install menggunakan `go get`.

Manfaat dengan adanya unit testing dapat meningkatkan keyakinan pada perubahan maupun *maintaining code*. Jika unit test ditulis dengan baik dan jika itu dijalankan setiap kali terdapat perubahan pada *code*, kita akan dapat segera menemukan setiap *defects* yang diperlihatkan karena adanya perubahan pada *code*. *code* yang ditulis juga akan lebih *reusable* karena untuk membuat unit test, *code* yang dibuat harus modular. Selain itu juga dengan adanya unit test, proses development bisa lebih cepat dan *cost* yang dikeluarkan untuk memperbaiki *defects* bisa dikurangi.

## Referensi

* [Software Testing Fundamental - Unit Testing](http://softwaretestingfundamentals.com/unit-testing/)
* [Golang basics - writing unit tests](https://blog.alexellis.io/golang-writing-unit-tests/)
* [Code coverage](https://en.wikipedia.org/wiki/Code_coverage)
* [Dasar Pemrograman Golang - Unit Test](https://blog.alexellis.io/golang-writing-unit-tests/)