---
tags:
  - Leetcode
  - Easy
  - happy-number
solved date: 2025-07-22
---
# 🧩 Problem Statement

Kamu diberikan sebuah angka `n`.  
Tugasmu adalah menentukan apakah angka tersebut merupakan **Happy Number**.
### Apa itu Happy Number?
- Ambil semua **digit** dari angka tersebut.
- Kuadratkan masing-masing digit dan jumlahkan hasilnya.
- Ulangi proses ini dengan hasil sebelumnya sebagai angka baru.
- Jika akhirnya mencapai angka `1`, maka **happy** ✅.
- Jika **terjebak dalam siklus** dan tidak pernah sampai `1`, maka **bukan happy** ❌.

---
# 🔄 Analogi
## Langkah 1: Konsep Dasar (Sederhanakan)
Bayangkan kamu sedang bermain **game teka-teki angka**:
- Kamu masukkan satu angka ke mesin ajaib.
- Mesin akan mengambil **masing-masing digit angka itu**, kuadratkan, lalu menjumlahkannya.
- Mesin akan terus mengulang ini dengan hasil sebelumnya.

Kalau hasil akhirnya adalah `1`, mesin akan berbunyi: 🎉 _Happy!_
Tapi kalau mesin **berputar-putar terus menerus tanpa pernah sampai `1`**, artinya kamu terjebak di dalam **loop tak berujung**, dan mesin akan berkata: ❌ _Not Happy!_

---

### 🎯 Tujuan Akhir
1. Ulangi proses kuadrat-jumlah hingga ketemu `1` (happy),  
    atau mendeteksi adanya **siklus angka** (tidak happy).
2. Lakukan ini tanpa menyimpan semua hasil sebelumnya,  
    tapi cukup pakai **dua pointer** untuk mendeteksi siklus seperti balapan.
---
# 💡 Solusi
Kita pakai **Floyd's Cycle Detection Algorithm**, yaitu:
- 🐢 **slow** pointer: jalan pelan (1 langkah)
- 🐇 **fast** pointer: jalan cepat (2 langkah)

## Cara kerjanya:
1. Slow dan fast mulai dari angka awal.
2. Setiap langkah:
    - Slow: hitung total kuadrat digit sekali
    - Fast: hitung dua kali (2x lebih cepat)
3. Kalau keduanya ketemu **di angka selain 1**, berarti ada **loop** → bukan happy.
4. Kalau fast akhirnya jadi `1`, berarti angka happy.

---
## 🧮 Detail Fungsi `getNext(n int)`
Bayangkan kamu punya angka, misalnya `82`.
### Langkah-langkah fungsi `getNext(82)`:
1. Ambil digit terakhir: `2`
2. Kuadratkan: `2² = 4`
3. Ambil digit berikutnya: `8`
4. Kuadratkan: `8² = 64`
5. Jumlahkan hasilnya: `4 + 64 = 68`

Jadi, `getNext(82) = 68`
### Secara umum:
```Go
func getNext(n int) int {
    sum := 0
    for n > 0 {
        d := n % 10       // ambil digit terakhir
        sum += d * d      // kuadratkan dan tambahkan ke sum
        n /= 10           // buang digit terakhir
    }
    return sum
}
```


## 🧮 Langkah-langkah Utama (2-pointer deteksi siklus)
1. `slow = n`, `fast = getNext(n)`
2. Ulangi selama `fast != 1` dan `slow != fast`:
    - `slow = getNext(slow)`
    - `fast = getNext(getNext(fast))`
3. Kalau `fast == 1` → happy ✅  
    Kalau `slow == fast` → loop ❌

---
# ✅ Kode Lengkap di Go
```Go
package main

import (
	"fmt"
)

// Fungsi bantu: hitung jumlah kuadrat dari setiap digit angka
func getNext(n int) int {
	sum := 0
	for n > 0 {
		d := n % 10        // Ambil digit terakhir
		sum += d * d       // Kuadratkan dan tambahkan ke total
		n /= 10            // Hapus digit terakhir
	}
	return sum
}

// Main logic: cek apakah angka happy
func isHappy(n int) bool {
	slow := n
	fast := getNext(n)

	for fast != 1 && slow != fast {
		slow = getNext(slow)
		fast = getNext(getNext(fast))
	}

	return fast == 1
}

func main() {
	n := 19
	fmt.Println(n, "is happy?", isHappy(n)) // Output: true
}
```

# 🎓 Catatan Tambahan
- Kenapa pakai 2 pointer? Karena kita **tidak perlu menyimpan semua angka sebelumnya**.
- Kita hanya ingin tahu apakah proses ini **berulang di angka yang sama** → berarti ada siklus.
- Ini sama seperti deteksi **loop pada linked list** (konsep klasik CS).