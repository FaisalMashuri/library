---
tags:
  - Leetcode
  - Easy
  - intersection-of-two-arrays
solve date: 2025-07-30
---
# 🧩 Problem Statement

Kita diberikan dua buah array `nums1` dan `nums2`.  Kita diminta untuk mencari irisan dari 2 buah array tersebut

---

# 🔄 Analogi
Bayangkan kamu sudah selesai membuat acara, dan kamu punya
- `list1` yang berisi daftar undangan
- `list2` yang berisi daftar yang hadir
Kita diminta untuk melihat siapa aja yang diundang dan hadir pada acara tersebut.

---

# 💡 Solusi
- Buat `set1` berisi semua elemen `nums1`.
- Iterasi `nums2`, cek apakah elemen ada di `set1`.
- Simpan ke `resultSet` supaya tidak ada duplikat.
- Konversi `resultSet` jadi array.

# Implementasi Go

```Go
func Solution(nums1 []int, nums2 []int) []int {
	set1 := make(map[int]bool)
	for _,num := range nums1 {
		set1[num] = true
	}
	set2 := make(map[int]bool)
	for _, num := range nums2 {
		if set1[num] {
			set2[num] = true
		}
	}
	result := []int{}
	for num := range set2 {
		result = append(result, num)
	}
	return result
}
```

