---
tags:
  - two-pointer
  - Leetcode
  - Easy
solve date: 2025-07-19
---
# Problem Statement
Kamu diberi sebuah array (daftar angka) yang sudah terurut, tapi ada beberapa angka yang muncul lebih dari sekali (duplikat). Tugasmu adalah menghapus semua duplikat sehingga setiap angka hanya muncul sekali, dan kamu harus melakukannya tanpa menggunakan memori tambahan (di tempat). Array yang dihasilkan harus tetap terurut, dan kamu perlu mengembalikan panjang array baru tanpa duplikat.

# Analogi
**Langkah 1: Konsep Dasar (Sederhanakan)**
Bayangkan kamu punya **deretan kotak mainan** yang sudah disusun rapi di **rak panjang**.  
Kotak-kotak ini **sudah diurutkan berdasarkan warna** — misalnya:
```Go
[Merah, Merah, Biru, Biru, Hijau, Hijau]
```
Tapi kamu hanya ingin **menyimpan satu kotak untuk setiap warna**.  
Jadi kalau ada dua kotak merah atau tiga kotak hijau, kamu akan **menyingkirkan yang duplikat**.

Tapi… kamu **tidak boleh menambah rak baru** atau memindahkan ke rak lain.  
Kamu hanya boleh **menggeser-geser posisi kotak di rak yang sama**, sehingga kotak-kotak dengan warna unik berada di bagian depan rak.

### 🎯 **Tujuan Akhir**
1. Pastikan setiap warna hanya muncul **satu kali** di awal rak.
2. Hitung ada **berapa kotak unik** yang tersisa.
3. Abaikan sisa kotak di belakang — mereka boleh tetap di rak, tapi tidak dihitung lagi.

# Solusi
Nah, kamu minta bantuan dua teman kecilmu:
- Si **Left**: dia duduk di posisi terakhir kotak unik.
- Si **Right**: dia menyisir rak dari kiri ke kanan, nyari warna baru.

Setiap kali Right menemukan kotak **dengan warna berbeda dari Left**, dia bilang:
> “Hei Left! Aku nemu warna baru!”
Lalu Left akan maju satu langkah dan bilang:
> “Sini, aku simpan di tempatku.”

Dengan cara ini, kotak-kotak unik akan **ngumpul di depan rak**, dan kotak duplikat akan ditimpa dan dilupakan.

## 🧮 **Langkah-langkahnya**

Pakai 2 pointer:
- `left`: posisi terakhir angka unik.
- `right`: penjelajah untuk mencari angka baru.

### Pseudocode versi bahasa manusia:
1. Mulai dari index `left = 0`, `right = 1`.
2. Selama `right` belum sampai akhir:
    - Kalau `nums[left] == nums[right]` → lewati aja, duplikat.
    - Kalau beda → `left++`, lalu `nums[left] = nums[right]`.
3. Setelah selesai, `left+1` adalah jumlah angka unik.


✅ **Kode Lengkap di Go**
```Go
func removeDuplicates(nums []int) int {
    left, right := 0, 1

    for right < len(nums) {
        if nums[left] == nums[right] {
            right++ 
        } else {
            left++
            nums[left] = nums[right]
        }
    }
    return left + 1
}
```

# Illustrasi
[[Remove Duplicates from Sorted Array - Drawing]]
