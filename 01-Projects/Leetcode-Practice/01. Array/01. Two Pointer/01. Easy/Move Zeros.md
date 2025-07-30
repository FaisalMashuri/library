---
tags:
  - Leetcode
  - Easy
  - move-zeros
solved date: 2025-07-30
---
# 🧩 Problem Statement

Kamu diberikan sebuah array int `nums`. Tugas kita untuk memindahkan elemen yang bernilai `0` ke bagian belakang array

---
# 🔄 Analogi
Jadi bayangkan ada sebuah antrian, setiap orang yang antri dikategorikan menjadi 2 yaitu
- elemen zero => orang yang antri **tidak bawa belanjaan**
- elemen non zero => orang yang antri dengan membawa belanjaan
---

### 🎯 Tujuan Akhir

Kita diminta untuk memindahkan orang yang termasuk kategori zero untuk berpindah di belakang tanpa harus membuat antrian baru

---
# 💡 Solusi

## Two Pointer
kita bisa membuat 2 buah pointer dengan nilai awal yang sama, yaitu 
- `left` untuk mencari tempat kosong pertama yang akan diisi
- `right` untuk mencari orang yang mengantri dengan membawa belanjaan

## Cara kerjanya
1. `left` dan `right` di-inisiasi dengan nilai 0
2. Lalu lakukan perulangan selama nilai pointer right kurang dari panjang antrian
3. Selama perulangan terjadi, cek kondisi jika antrian ke `right` tidak sama dengan `nol` maka tukar antrian ke `left` dengan antrian `right`. Kemudian value `left` maju satu langkah.
4. Lalu tambahkan nilai `right` dengan 1
---

# Implementasi Go
```Go
func Solution(nums []int) {
	left, right := 0,0
	for right < len(nums) {
		if nums[right] != 0 {
			temp := nums[left]
			nums[left] = nums[right]
			nums[right] = temp
			left++
		}
		right++
	}
}
```

# 🎓 Catatan Tambahan
- **Kenapa dua pointer?**  
    Karena kita ingin menggeser semua non-zero ke depan sambil mempertahankan urutan, dan memindahkan nol ke belakang **tanpa array baru**.
- **Optimisasi**: Jika `left == right`, tidak perlu melakukan swap (mengurangi operasi yang tidak perlu).
- **Kompleksitas waktu**: `O(n)` — hanya satu kali iterasi.
- **Kompleksitas memori**: `O(1)` — in-place.