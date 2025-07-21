---
tags:
  - Leetcode
  - Easy
  - two-pointer
  - merge-sorted-array
solve date: 2025-07-21
---
# 🧩 Problem Statement

Kamu diberikan dua buah array
- `nums1` panjangnya m + n, di mana :
	- elemen pertama sebanyak `m` sudah terurut menaik
	- Elemen sisanya (`n` buah angka 0 diakhir) adalah slot kosong untuk digabung 
- `nums2`, panjangnya `n`, juga terurut menaik

Tugasmu adalah untuk membandingkan `nums2` kedalam `nums1` secara *in-place*, tanpa membuat array baru, hasil akhirnya harus tetap terurut menaik.

# 🔄 Analogi
## Langkah 1: Konsep Dasar (Sederhanakan)
Bayangkan kamu punya satu **rak besar** berisi **mainan warna-warni**:
- Di bagian depan, sudah ada `m` buah mainan yang **tersusun rapi** dari kecil ke besar.
- Di belakangnya, ada **ruang kosong** (kotak kosong) sebanyak `n`, siap diisi mainan tambahan.
    
Lalu, kamu datang membawa `n` mainan lain (`nums2`), juga tersusun rapi.

Tugasmu adalah menyusun **semua mainan (lama + baru)** ke dalam rak **tanpa menambah rak baru**.  
Tapi hati-hati: jangan rusak urutan! Harus tetap dari kecil ke besar.

---
### 🎯 Tujuan Akhir
1. **Gabungkan** mainan dari rak lama dan mainan baru ke dalam satu rak (`nums1`).
2. Lakukan semuanya **dari belakang**, supaya kamu tidak menimpa mainan yang masih kamu butuhkan.
3. Setelah selesai, rak `nums1` akan berisi semua mainan terurut dari kecil ke besar.


# 💡 Solusi

Nah, kamu minta bantuan 3 teman kecil:
- 🧒 Si **i**: penjaga rak lama, mulai dari ujung mainan lama (`m-1`).
- 🧑 Si **j**: penjaga rak baru (`nums2`), mulai dari ujung (`n-1`).
- 🧓 Si **k**: tukang isi rak dari belakang (`m+n-1`), biar tidak numpuk.

## Cara kerjanya:

1. Si i dan j membandingkan siapa mainannya lebih besar.
2. Yang lebih besar, dikasih ke si k untuk ditaruh di slot paling belakang.
3. Ulangi sampai mainan dari rak baru (j) habis.

Kalau mainan rak lama (i) habis duluan, jangan khawatir.  
Langsung salin sisa mainan rak baru ke slot kosong depan rak.

---
## 🧮 Langkah-langkahnya (2-pointer dari belakang)
1. Inisialisasi:
    - `i = m - 1`
    - `j = n - 1`
    - `k = m + n - 1`
2. Selama `i >= 0` dan `j >= 0`:
    - Jika `nums1[i] > nums2[j]`, taruh `nums1[i]` di `nums1[k]`, kurangi `i`.
    - Kalau tidak, taruh `nums2[j]` di `nums1[k]`, kurangi `j`.
    - Kurangi `k`.
3. Kalau masih ada sisa di `nums2`, salin semuanya ke `nums1[0..j]`.


# ✅ Kode Lengkap di Go
```Go
func merge(nums1 []int, m int, nums2 []int, n int) {
	i := m - 1
	j := n - 1
	k := m + n - 1

	for i >= 0 && j >= 0 {
		if nums1[i] > nums2[j] {
			nums1[k] = nums1[i]
			i--
		} else {
			nums1[k] = nums2[j]
			j--
		}
		k--
	}

	// Salin sisa nums2 jika ada
	for j >= 0 {
		nums1[k] = nums2[j]
		j--
		k--
	}
}
```



# 💡 Solusi ke 2
Gunakan strategi “kasar tapi cepat”:
- Potong bagian `nums1` agar hanya berisi elemen yang valid (`[:m]`)
- Gabungkan `nums2` ke `nums1` pakai `append`
- Urutkan semua isi `nums1` pakai `sort.Ints`

## 🧮 Langkah-langkahnya (versi manusia)
1. Abaikan semua nol di belakang `nums1`, cukup ambil `nums1[:m]`.
2. Gabungkan semua isi `nums2` ke belakang `nums1`.
3. Urutkan semua angka dari awal supaya hasil akhirnya rapi.


# ✅ Kode Lengkap di Go
```Go
import "sort"

func merge(nums1 []int, m int, nums2 []int, n int) {
   nums1 = nums1[:m]               
   nums1 = append(nums1, nums2...) 
   sort.Ints(nums1)                
}
```
