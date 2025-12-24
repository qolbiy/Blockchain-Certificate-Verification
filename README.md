# Blockchain Certificate Verification

Proyek ini merupakan aplikasi terdesentralisasi (Decentralized Application / DApp) yang dikembangkan sebagai tugas akhir mata kuliah Blockchain.  
Sistem ini bertujuan untuk menyediakan mekanisme verifikasi sertifikat digital yang aman, transparan, dan sulit dimanipulasi dengan memanfaatkan teknologi blockchain.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Gambaran Umum Proyek

Blockchain Certificate Verification dirancang untuk mencegah pemalsuan sertifikat digital dengan cara menyimpan nilai hash kriptografis dari sertifikat ke dalam blockchain.  
Alih-alih menyimpan file sertifikat secara langsung, sistem hanya mencatat hash sertifikat, sehingga integritas data tetap terjaga tanpa mengorbankan privasi pengguna.

Aplikasi ini memungkinkan proses penerbitan dan verifikasi sertifikat dilakukan secara terdesentralisasi tanpa ketergantungan pada server pusat.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Fitur Utama

- Unggah file sertifikat digital
- Pembuatan hash SHA-256 secara otomatis
- Penyimpanan hash sertifikat ke blockchain Ethereum
- Verifikasi keaslian sertifikat berbasis blockchain
- Transparansi transaksi melalui Etherscan
- Mekanisme anti-duplikasi untuk mencegah pemalsuan sertifikat

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Alur Kerja Sistem

1. Pengguna mengunggah file sertifikat digital  
2. Sistem menghasilkan hash kriptografis dari file tersebut  
3. Hash disimpan ke blockchain melalui smart contract  
4. Pada proses verifikasi, hash file dibandingkan dengan data yang tersimpan di blockchain  
5. Sistem menampilkan hasil verifikasi (valid atau tidak valid)  

File sertifikat asli tidak pernah disimpan di blockchain.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Teknologi yang Digunakan

- Blockchain: Ethereum (Testnet Sepolia)
- Bahasa Smart Contract: Solidity ^0.8.x
- Frontend: HTML, CSS, JavaScript
- Library Web3: ethers.js
- Wallet: MetaMask
- IDE Smart Contract: Remix IDE

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Struktur Proyek
```teks
blockchain-certificate-verification/
├── contracts/
│   └── CertificateRegistry.sol
├── frontend/
│   ├── index.html
│   ├── styles.css
│   └── app.js
├── README.md
```
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


## Informasi Smart Contract

- Nama Contract: CertificateRegistry  
- Network: Ethereum Sepolia Testnet  
- Alamat Contract:   `0xdDda8234D69eb05893b773fb5138B9DC5B0eb65c`


Tautan Etherscan:  
https://sepolia.etherscan.io/address/0xdDda8234D69eb05893b773fb5138B9DC5B0eb65c

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Cara Menjalankan Aplikasi

1. Pastikan ekstensi MetaMask telah terpasang pada browser  
2. Atur jaringan MetaMask ke Ethereum Sepolia Testnet  
3. Clone atau unduh repository ini  
4. Buka folder `frontend/`  
5. Jalankan `index.html` menggunakan Live Server  
6. Hubungkan wallet MetaMask  
7. Gunakan fitur penerbitan dan verifikasi sertifikat  

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Aspek Keamanan Sistem

- Setiap sertifikat direpresentasikan oleh hash yang unik  
- Hash yang sama tidak dapat disimpan lebih dari satu kali  
- Sifat immutable blockchain menjamin data tidak dapat diubah  
- Sistem tidak menggunakan penyimpanan terpusat  

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Tujuan Proyek

- Menerapkan konsep blockchain dan smart contract pada studi kasus nyata  
- Membangun sistem verifikasi sertifikat digital yang terdesentralisasi  
- Mengurangi risiko pemalsuan sertifikat digital  
- Menyediakan mekanisme verifikasi yang transparan dan dapat dipercaya  

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Anggota Kelompok

- Nayuda Gigih Fayruz Qolbiy
- Abiestia Dika Mulya Saputra 
- Riyan Dwi Saputra
- Febrian Fadilla

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Demo Aplikasi

Aplikasi dapat dilihat secara langsung di:

[https://qolbiy.github.io/Blockchain.github.io/](https://qolbiy.github.io/blockchain-certificate-verif/)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Lisensi

Proyek ini dikembangkan untuk keperluan akademik dan pembelajaran.
