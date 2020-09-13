## IF5020 - Hiring Problem
**Aditya Rachman Putra** (23520032)

_hiring problem_ ini digunakan sebagai studi kasus untuk bisa memahami lebih dalam mengenai _Probabilistic Analysis_ dan _Randomized Algorithm_

---

## Hiring Problem

--

### Permasalahan:

- Kita ingin meng-_hire_ satu orang _office assistant_. Dan kita ingin _office assistant_ yang kita pekerjakan selalu _office assistant_ terbaik.
- Kita menggunakan jasa agen ketenagakerjaan.
    - Setiap harinya agen tersebut akan mengirimkan satu kandidat
    - Kita akan interview kandidat tersebut dan  memutuskan untuk memperkajakannya atau tidak

--

- Karena kita menggunakan jasa agensi, kita perlu membayar agency tersebut untuk setiap kandidat yang mereka kirimkan
- Dan untuk meng-_hire_ seorang kandidat kita perlu mengeluarkan kocek yang lebih besar lagi
    - Karena perlu memecat _office assistant_ yang ada, lalu
    - Membayar agency untuk meng-_hire_ kandidat baru tsb.

--

- Karena kita berkomitmen untuk selalu mempekerjakan _office assistant_ terbaik, maka bila saat interview kandidat, kandidat tersebut lebih baik dibanding _office assistant_ kita maka kita akan memecat office assistant kita dan mempekerjakan kandidat tersebut.
- Dalam hal ini, kita berani membayar seluruh cost tersebut, namun kita ingin bisa **mengestimasi berapa besar total cost yang perlu dibayarkan**.

--

### Pseudo Code

``` js
Hire-Assistant(n)
best = 0
for i = 1 to n
    interview candidate i
    if candidate i is better than candidate best
        best = i
        hire candidate i
```
- **(Asumsi)** Dengan menginterview kandidat kita bisa mengestimasi apakah kandidat tersebut yang terbaik sejauh ini.

--
### Komponen Cost

- Bukan menghitung ~~running time~~
- Fokus terhadap **cost** agency, dengan komponen:
    - Cost Interview kandidat(`$c_i$`)
    - Cost Hiring kandidat (`$c_h$`)
    - `$n$` orang kandidat
    - `$m$` orang yang di-_hire_,
- maka cost yang akan kita keluarkan adalah:
`$O(c_i n + c_h m)$`
Note:
Dalam permasalahan ini kita tidak menghitung running time dari algorima ini. Karena dalam konteks ini, running timenya akan sama dengan jumlah kandidat. Meskipun terlihat berbeda, tapi cara analisa ini bisa digunakan juga untuk hal tersebut, karena pada intinya kita menghitung cost dari melakukan suatu operasi.

--

Karena kita pasti menginterview semua kandidat, jadi kita bisa fokus menganalisa cost hiring, yaitu:
### `$$c_h m$$`

--

### Analisa kemungkinan terburuk

- Cost maksimal yang mungkin dikeluarkan
- Itu terjadi ketika kandidat yang datang selalu lebih baik dari kandidat sebelumnya.
`$$O(c_h n)$$`
- Bagaimana untuk kasus pada umumnya ?

Note:
- Dengan melihat kemungkinan terburuk kita bisa melihat batas cost maksimal yang bisa dikeluarkan
- Itu terjadi ketika kandidat yang datang selalu lebih baik dari kandidat sebelumnya. Sehingga cost yang perlu kita keluarkan adalah
    - `$$O(c_h n)$$`
- Namun karena kandidat bisa datang dengan urutan kualitas yang berbeda-beda, maka wajar bila kita ingin tahu berapa cost untuk kasus pada umumnya (atau rata-rata)

---

## Probabilistic Analysis

- Menggunakan pendekatan probabilistic
- Perlu tahu atau dapat berasumsi mengenai distribusi dari input algoritme yang dianalisa.

--

### Average-Case

rata-rata cost dari keseluruhan distribusi kemungkinan input, merepresentasikan keseluruhan kemungkinan input tersebut.

--

#### Average-Case Cost in Hiring Problem

- Bergantung pada distribusi yang kita gunakan
- Asumsi pada _hiring problem_:
    - **total_order**
    - urutan datangnya kandidat **acak**
    - seluruh permutasi urutan datangnya kandidat  **memiliki kemungkinan yang sama untuk terjadi** (_uniform random permutation_)

Note:
_Probabilistic Analysis_ ini sangat bergantung pada distribusi yang kita gunakan. Sehingga perlu hati-hati dalam menentukan distribusi tersebut. Ada masalah yang kita bisa memilih distribusi input yang memungkinkan sehingga bisa menganalisa secara probabilistik, namun ada juga masalah yang kita tidak bisa menentukan distribusi input yang memungkinan. Untuk masalah tersebut analisa ini tak dapat dilakukan.

Untuk _hiring problem_ terdapat beberapa asumsi  yang akan kita gunakan.
- Berlaku _total order_ untuk keseluruhan kandidat
    - Tidak ada dua kandidat yang memiliki kualitas yang sama
    - Kita bisa mengukur kualitas suatu kandidat `$i$` dengan fungsi `$rank(i)$`, yang akan menghasilkan angka `$1$` hingga `$n$` (angka besar menandakan kualitas yang lebih baik)
- Sehingga, list `$(rank(1), .. ,rank(n))$` merupakan permutasi dari list `$(1,..,n)$`
- Kandidat datang **secara acak** dalam kasus ini diasumsikan bahwa yang dimaksud dengan **acak** adalah seluruh kemungkinan permutasi list kualitas tersebut **memiliki kemungkinan yang sama untuk terjadi** (_uniform random permutation_)

--

### Randomized Algorithm

pendekatan yang lain dalam merancang suatu algoritme, agar dapat dilakukan _probabilistic analysis_ dengan membuat bagian algoritme tersebut berperilaku secara **random**.

Note:
- Ini merupakan pendekatan yang lain dalam merancang suatu algoritme, agar dapat dilakukan _probabilistic analysis_
- dalam _probabilistic analysis_ tersebut kita butuh tau distribusi input, namun banyak kasus dimana kita tidak mengetahui distribusi input yang memungkinkan. Dalam kasus tersebut, untuk membantu merancang dan menganalisa algoritmenya, kita membuat salah satu bagian algoritme tersebut berperilaku **random**.

--

#### Randomized Algorithm in Hiring Problem

- Merubah Hiring Problem menjadi:
    - Di awal mendapat list kandidat dari agency (hanya nama kandidat)
    - Setiap hari kandidat dipanggil secara _random_ dari list tersebut
- sehingga memaksa urutan kandidat agar bersifat **random**

Note:
Dengan begitu, _cost_ kita tidak lagi bergantung hanya pada urutan datangnya kandidat yang diberikan oleh agency, namun kita memaksa urutan tersebut agar bersifat **random**.

--

#### Algorithm

Cost hanya bergantung pada input

![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FAlphaWorks%2Fw6syQHS9PF.png?alt=media&token=44e2c234-4668-4cb2-bd5c-687044d47ab4)

--

#### Randomized Algorithm
- Cost bergantung pada input dan suatu **random-number generator**

![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FAlphaWorks%2FUSFfEnAXI-.png?alt=media&token=7f4ead53-0018-4471-927b-9c3127b87249)

--

#### Property dari Randomized Algorithm

- Stokastik
- Tidak ada input yang selalu memberikan worst-case

Note:
- **Algoritme deterministik**, untuk input yang tertentu, outputnya tidak akan berubah-ubah
- **Algoritme Stochastic**, untuk input yang sama bisa memiliki output yang berbeda-beda
- Terdapat input yang bisa secara konsisten memberikan worst-case behavior
- Tidak ada input tertentu yang akan selalu memberikan worst-case behavior

--

#### Average vs Expected

- _average-case cost_ : analisa berdasarkan kemungkinan distribusi input
- _expected cost_ : analisa cost dari __randomized algorithm__ (berdasarkan distribusi kemungkinan yang dihasilkan RNG)

---

## Analyzing Hiring Problem

--

### Indicator Random Variable

_Random Variable_ yang dirancang untuk mempermudah konversi dari _probability_ menjadi _expectation_

`$$ I\{A\}=
\begin{cases}
1 & \text{bila A terjadi,} \\
0 & \text{bila A tidak terjadi.}
\end{cases}$$`

Note:
- _Indicator Random Variable_ pada dasarnya adalah _Random Variable_ seperti yang kita kenal selama ini, namun dirancang untuk mempermudah dalam mengkonversi dari kemungkinan menjadi ekspektasi.
`$$ I\{A\}=
\begin{cases}
1 & \text{bila A terjadi,} \\
0 & \text{bila A tidak terjadi.}
\end{cases}$$`

--

### How to Use?

_Probability_ jadi _expectation_:
`$$E[I\{A\}] = E[X_A] = P_r \{A\}$$`
Mempermudah trial acak yang berulang, karena sifat _linearity_ dari _expectation_
`$$E[\sum_{i=1}^{n} X_i] = \sum_{i=1}^{n} E[X_i]$$`
<sub><sup>Berlaku walaupun terdapat kebergantungan antar random variables (kenapa?)</sup></sub>

--

#### Hiring Problem menggunakan indicator random variables

_Expectation_ konvensional, `$X$` adalah jumlah kandidat yang di-_hire_ (repot?)
`$$E[X] = \sum_{x=1}^{n} x P_r\{X = x\}$$`

Note:
- Namun perhitungan tersebut cukup repot untuk dilakukan, bila dilakukan pendekatan menggunakan indicator random variables, daripada menggunakan satu random variable untuk menandakan berapa kali kita meng-_hire_,
--

Menggunakan `$n$` _indicator random variable_ `$X_i$` menandakan event kandidat `$i$` di-_hire_
`$$\begin{aligned}
X_i &= I\{\text{kandidat i di-hire}\} \\
X_i &= \begin{cases}
    1 & \text{bila kandidat i di-hire,} \\
    0 & \text{bila kandidat i tidak di-hire.}
    \end{cases}
\end{aligned}
$$`

Note:
- kita bisa menggunakan `$n$` random variable `$X_i$` untuk menandakan event kandidat kandidat `$i$` di-_hire_
    - `$X_i = I\{\text{kandidat i di-hire}\}$`
    - `$ X_i = \begin{cases} 1 & \text{bila kandidat i di-hire,} \\0 & \text{bila kandidat i tidak di-hire.}\end{cases}$`

--

Sehingga untuk seluruh _event_
`$$X = X_1 + X_2 + ... + X_n$$`
Untuk mengetahui ekspektasi keseluruhan perlu ekspektasi masing-masing _event_
`$$E[X_i] = P_r \{\text{kandidat i di-hire}\}$$`
Bagaimana menghitungnya?

Note:
- Sehingga `$X = X_1 + X_2 + ... + X_n$` dan untuk mengetahui ekspektasi keseluruhan kita memerlukan ekspektasi tiap event `$E[X_i] = P_r \{\text{kandidat i di-hire}\}$`. Jadi kita perllu mengetahui kemungkinan kandidat ke-i di-_hire_.

--

#### Menghitung Kemungkinan Event `$X_i$`

- Asumsi distribusi input _random uniform permutation_
- Event `$X_i$` bernilai 1 bila kandidat `$i$` lebih baik dibandingkan kandidat `$1 - X_i$`
- Kemungkinan kandidat `$i$` lebih baik dibanding semua kandidat sebelumnya adalah `$1/i$`

`$$E[X_i] = P_r \{\text{kandidat i di-hire}\} = 1/i$$`
Note:
- Ingat asumsi bahwa distribusi inputnya _random uniform permutation_, yang artinya semua permutasi urutan kandidat memiliki kemungkinan yang sama.
- Event `$X_i$` terjadi bila kandidat `$i$` lebih baik dibandingkan kandidat `$1$` hingga `$i-1$`. Karena semua permutasi memiliki kemungkinan yang sama, maka setiap kandidat 1 hingga i memiliki kemungkinan yang sama untuk lebih baik dibandingkan yang lain. Maka kemungkinan kandidat `$i$` lebih baik dibanding semua kandidat sebelumnya adalah `$1/i$`
- `$E[X_i] = 1/i$`

--

`$$\begin{aligned}
E[X] &= E[\sum_{x=1}^{n} X_i] \\
&= \sum_{x=1}^{n} E[X_i] \\
&= \sum_{x=1}^{n} 1/i \\
&= ln\, n + O(1) \\
\end{aligned}
$$`

--

Secara rata-rata, kita _hire_ sebanyak `$ln\, n$` kandidat, sehingga:
`$$\text{average-case hiring cost} = O(c_h\, ln\, n)$$`

<sub><sup>(_average-case_ karena kita menggunakan asumsi distribusi input untuk menganalisa kemungkinannya)</sup></sub>

Note:
- Dengan ekspektasi tersebut, maka _average-case hiring cost_ yang kita perlu keluarkan adalah `$$O(c_h\, ln(n))$$`
    - _average-case_ karena kita menggunakan asumsi distribusi input untuk menganalisa kemungkinannya

---

## Randomized Algorithm

sering kali distribusi kemungkinan input tidak diketahui, sehingga _average-case analysis_ tidak bisa dilakukan. Disaat tersebut kita bisa menggunakan _randomized algorithm_

Note:
- Bila sebelumnya kita mengetahui (atau memiliki asumsi) distribusi kemungkinan input, sering kali kita tidak memiliki pengetahuan tersebut, sehingga _average-case analysis_ tidak bisa dilakukan. Disaat tersebut kita bisa menggunakan _randomized algorithm_
--

### Analisa Hiring Problem menggunakan Randomized Algorithm

- Asumsi _random uniform permutation_ membantu analisa dan desain algoritma hiring problem
- Daripada mengasumsikan distribusi, kita membuat masukan algoritme ini memiliki _random uniform permutation_
- Sehingga asumsi selalu berlaku

Note:
- Untuk masalah _hiring problem_ asumsi _random uniform permutation_ mempermudah kita, untuk itu daripada berasumsi input memiliki distribusi seperti itu, kita bisa membuat agar masukan algoritme ini memiliki _random uniform permutation_ sehingga untuk input dengan distribusi kemungkinan seperti apapun, property tersebut masih berlaku

--

### Expected Hiring Cost

`$$\text{expected hiring cost} = O(c_h\, ln(n))$$`

Note:
- _expected hiring cost_ randomized algorithm ini adalah `$O(c_h\, ln(n))$`. Namun berbeda dengan _average-case_, disini kita tidak mengambil asumsi mengenai distribusi input algoritme ini. Namun kita memerlukan cara untuk bisa _randomly permuting input_.

---

## Merancang Randomized Algorithm

Untuk Hiring Problem terdapat setidaknya **dua** cara untuk secara acak menyusun input dari algoritme ini.

- Permute by sorting
- Randomize in place

--
### Permute by Sorting

```
n = A.length
let P[1::n] be a new array
for i = 1 to n
  P[i] = RANDOM(1,n^3)
sort A, using P as sort keys
```

Note:
Why does this result in uniform random permutation?
--

### Randomized in-place

```
n = A.length
for i = 1 to n
  swap A[i] with A[RANDOM(i,n)]
```

Complexity = O(n)

Note:
Why does this result in uniform random permutation?
