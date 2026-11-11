# ABSA Product Intelligence v6

Notebook analisis Aspect-Based Sentiment Analysis atas `dataset_labeled_v6.xlsx` (6.158 ulasan, 6 aspek: Kualitas, Bahan, Ukuran, Desain, Warna, Kenyamanan), disusun sesuai `brief_pengerjaan_notebook_absa_dataset_labeled_v6.md`.

## File
| File | Keterangan |
|:--|:--|
| `ABSA_Product_Intelligence_v6.ipynb` | Notebook final, sudah dieksekusi (grafik & tabel ter-render) |
| `dataset_labeled_v6.xlsx` | Data input (letakkan di folder yang sama dengan notebook) |

## Cara menjalankan
```bash
pip install pandas numpy matplotlib seaborn scipy openpyxl jinja2 jupyter
jupyter notebook ABSA_Product_Intelligence_v6.ipynb   # Kernel -> Restart & Run All
```
Notebook mencari data di folder kerja, lalu di `/mnt/user-data/uploads/`.

## Struktur
| Section | Isi |
|:--|:--|
| 0 | Executive Summary |
| 1 | Audit skema, konsistensi `label_json`/`jumlah_aspek_aktif`, duplikasi, deviasi vs brief |
| 2 | Metrik SoV, ANR, NSS, WPI + diverging bar + kuadran strategis |
| 3 | Hidden Dissatisfaction Rate, anatomi komplain ★4–5, analisis ★1–2 berteks positif |
| 4 | Co-occurrence, peluang bersyarat (heatmap), uji Kruskal-Wallis / Mann-Whitney |
| 5 | Preprocessing, bigram/trigram per aspek, tabel akar masalah |
| 6 | Kandidat aspek v7, ICE action plan, validasi angka kunci |

## Temuan utama
- Ukuran: ANR 32,6% dari 847 ulasan aktif, NSS 34,8%, 29,7% dari seluruh keluhan aspek.
- HDR ★5: 340 dari 5.136 ulasan (6,6%); ★4–5: 452 ulasan.
- 1.059 ulasan (17,2%) tanpa aspek aktif; kandidat aspek v7: pengiriman, pelayanan admin, kesesuaian produk, kemasan, harga/value.

## Catatan data (beda dari brief)
- Kolom di-rename: `rating`→`Rating`, `ulasan`→`Comment`, `jumlah_aspek`→`jumlah_aspek_aktif`; `panjang_kata` dihitung sendiri.
- `pola_ulasan` hanya `terstruktur`/`bebas`; segmen perilaku diturunkan dari Rating × aspek.
- Rata-rata rating 4,70 (brief: 4,81); 21 rating kosong (hanya dikeluarkan dari analisis berbasis rating); zero-aspek 1.059 (brief: ~964).

## Batasan
- Tema akar masalah dan kategori penyebab rating rendah berbasis kata kunci.
- Skor ICE adalah penilaian analis, bukan hasil model.
- Label aspek berlaku per ulasan, jadi n-gram bisa memuat kata dari topik lain.
