# Belajar Dengan Jenius Cryptocurrency Trading

## Penulis : Gun Gun Febrianza

# Drafts

# Bitcoin Address

**P2PKH atau Legacy Address Format (addresses dimulai dengan karakter “1”)**

Contoh: 1BvBMSEYstWetqTFn5Au4m4GFg7xJaNVN2

Format bitcoin address pertama kali, format ini cenderung memberikan nilai fee yang sangat tinggi saat bertransaksi. Selain itu address ini tidak dapat bersinergi dengan segwits address.



# Segwits

Segwits atau Segregate Witness memberikan manfaat yaitu :

1. Meningkatkan jumlah transaksi perdetik yang dapat diproses protokol bitcoin.
2. Memperbaiki permasalahan Transaction Malleability dalam protokol bitcoin. 

Eksistensi Segwits pada bitcoin protocol menciptakan klasifikasi transaksi baru yang disebut dengan segwits transaction. 

Setiap block dalam protokol bitcoin 

## vByte (Virtual Byte)

Semenjak di aktifkannya segwits ukuran transaksi diekspresikan dengaan Weigh Unit. Weigh Unit dapat dikonversi kedalam Virtual Byte atau Virtual Size dengan cara membaginya dengan angka integer 4 dan pembulatan (rounding). Virtual Size menentukan seberapa besar transaksi saat membayar fee.

## Non-segwits Transaction

Setiap Non-segwit byte dihitung 4 Weigh Units.

Setiap transaksi terdiri dari beberapa fields berikut :

- Version (4 bytes)
- \# of Inputs (VarInt, 1 byte for numbers up to 252)
- Inputs (varies)
- \# of Outputs (VarInt, 1 byte for numbers up to 252)
- Outputs (varies)
- Locktime (4 bytes)

Kita akan membedah setiap field dibawah ini yang bersumber dari [non-segwit raw transaction](https://blockstream.info/tx/791bd9b3bda632ee1757de37db8939b0287ece4753f3077b9a5f5c7e28545967): 

`0200000001d2eed35b0d55763981c635cab7788c28e3683af3d329947a17d7f6005390e6ef010000006a47304402200ffaac8f12e56f4af66109220812b76c7d6bb0e5906cf2de235b79496b3e080b0220037304894b648fa0b50e0d82ef9f58b537233ee282ab31fc04fb3d169d2c97cc0121030120a287eb98922752a89b39df64f7f3314036f6f096341c9189b0cb3c692aaeffffffff02404ff200000000001976a9140b818b11f9624e6a2d5b757a3e8fe45db3f6647788ace0b4b401000000001976a914a1e5e47fce1c5c0868107dba3851eb696c2ead5388ac00000000`

### Version

Versi dari transaksi ini adalah `02000000` (2 in little-endian), ukuran versi selalu 4 bytes (16 WU).

### # of Inputs

Nomor dari input adalah `01`, ini memberikan indikasi bahwa terdapat 1 input yang digunakan (spent) dalam transaksi ini. Data ini menambahkan 1 byte (4 WU).

### Inputs

Setiap Inputs terdiri dari fields:

- Referenced Transaction Hash (32 bytes)
- Output Index (4 bytes)
- Script Length (VarInt, 1 byte for numbers up to 252)
- ScriptSig (varies)
- Sequence (4 bytes)

Pada contoh transaksi di atas :

- RefTX: `d2eed35b0d55763981c635cab7788c28e3683af3d329947a17d7f6005390e6ef`
- Output Index: `01000000` (1 in little-endian)
- Script Length: `6a` (106 in VarInt notation)
- ScriptSig: `47304402200ffaac8f12e56f4af66109220812b76c7d6bb0e5906cf2de235b79496b3e080b0220037304894b648fa0b50e0d82ef9f58b537233ee282ab31fc04fb3d169d2c97cc0121030120a287eb98922752a89b39df64f7f3314036f6f096341c9189b0cb3c692aae`
- Sequence: `ffffffff`

Secara total, input ini menambahkan 147 bytes (588 WU).

### of Outputs

Nomor dari outputs adalah `02` (2 in VarInt notation), ini memberikan indikasi bahwa terdapat 2 outputs yang dibuat dalam transaksi ini. Data ini menambahkan 1 byte (4 WU).

### Output

Setiap Outputs terdiri dari fields :

- Value (8 bytes)
- Script Length (VarInt, 1 byte for numbers up to 252)
- ScriptPubKey (varies)

Pada contoh transaksi di atas terdapat 2 outputs. Output pertama :

- Value: `404ff20000000000` (15,880,000 satoshi, in little-endian)
- Script Length: `19` (25 in VarInt notation)
- ScriptPubKey: `76a9140b818b11f9624e6a2d5b757a3e8fe45db3f6647788ac`

Secara total, output ini menambahkan 34 bytes (136 WU).

Output kedua :

- Value: `e0b4b40100000000` (28,620,000 satoshi, in little-endian)
- Script Length: `19` (25 in VarInt notation)
- ScriptPubKey: `76a914a1e5e47fce1c5c0868107dba3851eb696c2ead5388ac`

Secara total, output ini menambahkan 34 bytes (136 WU).

### Locktime

Pada contoh transaksi di atas nilai dari locktime adalah `00000000` (0 in little-endian). Ukuran data Locktime selalu 4 bytes (16 WU).

Secara total, transaksi ini bernilai 900 WU. 

Konveri ke dalam vByte akan bernilai 225 vByte. (900/4=225)

Dengan [Input Value](https://blockstream.info/tx/efe6905300f6d7177a9429d3f33a68e3288c78b7ca35c6813976550d5bd3eed2?output:1) sebesar 0.4491 BTC dan kombinasi dari Output Value sebesar 0.445 BTC, total fee untuk miner sebesar 0.0041 atau 410,000 satoshi. Jika kita konversi ke dalam notasi sat/vB maka kita akan mendapatkan nilai feerate sebesar 1,822 sat/vB. 

## Segwits Transaction



---------------------

