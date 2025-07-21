---
tags:
  - Leetcode
  - Easy
  - two-pointer
  - remove-elements
solve date: 2025-07-20
---
# Problem Statement
Kamu dikasih array `nums` dan sebuah nilai `val`.  
Tugasmu: **hapus semua nilai yang sama dengan `val`**, tanpa membuat array baru.  
Lalu **kembalikan panjang array** setelah nilai itu dihapus.
# Analogi
Bayangin kamu punya deretan mainan di lantai:
```Javascript
[🐻, 🚗, 🚗, 🐻]
```
Tapi kamu benci mainan 🐻.  
Jadi kamu bilang:

> _"Pokoknya semua 🐻 harus dibuang! Tapi aku gak boleh ambil wadah baru. Harus beresin di tempat yang sama."_

# Solusi
Lalu kamu pakai dua bocil buat bantuin:
### 🎯 Siapa yang Kerja?
- **Si Right**: kelilingin semua mainan satu per satu.
- **Si Left**: pegang tempat kosong di depan — khusus buat mainan yang **boleh disimpan**.

1. Si Right jalan keliling dari awal sampai akhir.
2. Kalau mainan yang dia lihat adalah 🐻, dia **lewati**.
3. Kalau mainannya bukan 🐻 (misalnya 🚗), dia bilang:
    > "Nih, Left! Mainan bagus!"
    - Si Left langsung taruh di tempat dia berdiri.
    - Lalu dia maju satu langkah.

Akhirnya, semua mainan yang boleh disimpan akan **ngumpul di depan** lantai. 
Dan kamu tinggal hitung **berapa banyak** yang tersisa = posisi terakhir Left.

## 🧮 **Langkah-langkahnya**

Pakai 2 pointer:
- `left`: posisi untuk **menyimpan elemen yang bukan `val`**.
- `right`: penjelajah yang **mengecek semua isi array**.

### Pseudocode versi bahasa manusia
1. Mulai dari index `left = 0`, `right = 0`.
2. Selama `right` belum sampai akhir array:
    - Kalau `nums[right] == val` → artinya elemen ini harus dibuang → **lewati aja** (`right++`).
    - Kalau `nums[right] != val` → artinya elemen ini boleh disimpan:
        - Simpan di `nums[left] = nums[right]`
        - Geser `left++` (karena kita sudah simpan satu element            
        - Geser `right++` juga untuk lanjutkan scanning.
3. Setelah selesai, `left` adalah jumlah elemen yang **boleh disimpan** (bukan `val`).

✅ **Kode Lengkap di Go**
```Go
func removeElement(nums []int, val int) int {
    left, right := 0, 0
    for right < len(nums) {
        if nums[right] == val {
            right++
        } else {
            nums[left] = nums[right]
            left++
            right++
        }
    }
    return left
}
```

# Illustrasi

