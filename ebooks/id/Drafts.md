# Belajar Dengan Jenius Cryptocurrency Trading

## Penulis : Gun Gun Febrianza

# Drafts

# Bitcoin Address

**P2PKH atau Legacy Address Format (addresses dimulai dengan karakter “1”)**

Contoh: 1BvBMSEYstWetqTFn5Au4m4GFg7xJaNVN2

Format bitcoin address pertama kali, format ini cenderung memberikan nilai fee yang sangat tinggi saat bertransaksi. Selain itu address ini tidak dapat bersinergi dengan segwits address.

**P2SH atau Compatibility Address Format (addresses dimulai dengan karakter “3”)**

Contoh:3J98t1WpEZ73CNmQviecrnyiWrnqRhWNLy.

Format bitcoin address ini dapat digunakan untuk mengirimkan dana baik ke legacy address atau segwit address. 

**Bech32 atau Segwit Address Format (addresses dimulai dengan karakter “bc1”)**

Example: bc1qar0srrr7xfkvy5l643lydnw9re59gtzzwf5mdq

Format bitcoin address yang mendukung Segwit address. Penggunaan Segwit address dapat memperkecil fees saat melakukan transaksi. Namun sebagai catatan, beberapa jasa wallet dipihak ke 3 atau exchange biasanya belum mendukung format ini.

# Segwits

Segwits atau Segregate Witness memberikan manfaat yaitu :

1. Meningkatkan jumlah transaksi perdetik yang dapat diproses protokol bitcoin.
2. Memperbaiki permasalahan Transaction Malleability dalam protokol bitcoin. 

Eksistensi Segwits pada bitcoin protocol menciptakan klasifikasi transaksi baru yang disebut dengan segwits transaction. 

Inovasi Segwits pada protokol bitcoin menambahkan 2 format bitcoin address yaitu :

1. Segwit Address
2. Compability Address yang dapat mendukung transaksi antara legacy address dan segwit address.

Size dalam bytes dan vsize dalam virtual size adalah dua metrics yang berbeda :

1. Size dalam bytes adalah bytes of transaction mengacu pada serangkaian raw byte yang telah di serialisasi (serialized format) agar dapat dikirimkan lewat jaringan komputer dan disimpan ke dalam disk.
2. Virtual size dalam vBytes adalah berat suatu transaksi (weighted size) dalam aturan segwits. Digunakan untuk membandingkan seberapa banyak blockweight yang perlu dialokasikan agar bisa mengkonfirmasi sebuah transaksi.

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

### # of Outputs

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

Segwit transaction adalah transaksi yang di dalamnya terdapat segwit input baik itu segwit address atau compability address yang di awali dengankarakter "3" atau "bc1". Selain itu pada segwit transaction juga terdapat informasi ekstra seperti witness data. Data segwit dihitung 1 WU/byte, ukurannya sangat kecil untuk ditambahkan pada transaksi.

Hal inilah yang membuat segwit dapat menghemat biaya. Transaksi Segwit terdiri dari beberapa fields :

- Version (4 bytes)
- **Marker** (1 byte)
- **Flag** (1 byte)
- \# of Inputs (VarInt, 1 byte for numbers up to 252)
- Inputs (varies)
- \# of Outputs (VarInt, 1 byte for numbers up to 252)
- Outputs (varies)
- **Witness Data** (varies)
- Locktime (4 bytes)

Kita akan membedah lagi setiap fields dibawah ini yang bersumber dari  [Segwit Transaction](https://blockstream.info/tx/3d0acedc2f5787d2fbefa85e72ef6aac0465e78e4d3f05ae5f813488420bde38): ` 02000000000101caba4ccb61cca412fe29ec553d286134a02335c04355a9cc1e056fe2403692cf1400000000fdffffff026406010000000000160014093c864a10516154d18d2accd61c6b2920a2040f60361e000000000017a9140195e8dd3d1527038a0a77e0b0e4515d6c8ab195870247304402200760efedbcee3bbd913661fb40c364caed622b331ee3b5bc70ac25df2d3763d5022020efdb41ef325089d146eb48948b6aaec85c086fa38a3df4d2a51ee729645ebc012102be338e0362fb01101a873a7502012cb82f7d9d303b4943fa0702829a763e49762b550900` 

### Version

Versi dari transaksi ini adalah `02000000` (2 in little-endian), ukuran versi selalu 4 bytes (16 WU).

### Marker

Marker `00` (0 in VarInt notation) memberikan indikasi bawah ini adalah segwit transaction. Sebuah nodes yang sudah mendukung segwit dapat membaca marker tersebut. Sementara untuk node yang tidak mendukung segwit akan memperlakukan marker sebagai "# of inputs" field, node menganggapnya sebagai invalid karena memiliki 0 inputs. Data ini menambahkan 1 byte (1WU)

### Flag

Flag dengan nilai `01` (1 in VarInt notation), memberikan indikasi bahwa Witness Data akan hadir pada transaksi ini. Data ini menambahkan 1 byte (1 WU).

### # of Inputs

Nomor dari inputs `01` (1 in VarInt notation) memberikan indikasi bahwa terdapat 1 input dalam transaksi. Data ini menambahkan 1 byte (4 WU).

### Inputs

Input yang pertama dan hanya satu yaitu :

- RefTX: `caba4ccb61cca412fe29ec553d286134a02335c04355a9cc1e056fe2403692cf`
- Output Index: `14000000` (14 in little-endian)
- Script Length: `00` (0 in VarInt notation)
- ScriptSig: [EMPTY]
- Sequence: `fdffffff`

Input ini menambahkan data sebesar 41 bytes (164 WU).

### # Of Outputs

Nomor dari outputs `02` (2 in VarInt notation), memberikan indikasi bahwa terdapat 2 outputs yang tercipta dalam transaksi ini. Data ini menambahkan 1 byte (4 WU).

### Outputs

Output pertama :

- Value: `6406010000000000` (67,172 satoshi, in little-endian)
- Script Length: `16` (22 in VarInt notation)
- ScriptPubKey: `0014093c864a10516154d18d2accd61c6b2920a2040f`

Output ini menambahkan 31 bytes (124 WU). 

Output yang kedua :

- Value: `60361e0000000000` (1,980,000 satoshi, in little-endian)
- Script Length: `17` (23 in VarInt notation)
- ScriptPubKey: `a9140195e8dd3d1527038a0a77e0b0e4515d6c8ab19587`

Output ini menambahkan 32 bytes (128 WU).

### Witness Data

Witness program pada transaksi ini : ` 0247304402200760efedbcee3bbd913661fb40c364caed622b331ee3b5bc70ac25df2d3763d5022020efdb41ef325089d146eb48948b6aaec85c086fa38a3df4d2a51ee729645ebc012102be338e0362fb01101a873a7502012cb82f7d9d303b4943fa0702829a763e4976 `

Witness Data menambahkan107 bytes (107 WU).

### Locktime

Locktime dari transaksi ini adalah `2b550900` (611,627  in little-endian) dan digunakan sebagai block height pada hasil transaction output ini dapat digunakan (spent). Data ini menambahkan 4 bytes (16 WU).

Total transaksi ini adalah 565 WU. 

Konveri ke dalam vByte akan bernilai 142 vB (dibulatkan). 

Dengan [Input Value](https://blockstream.info/tx/cf923640e26f051ecca95543c03523a03461283d55ec29fe12a4cc61cb4cbaca?output:20) sebesar 0.02118172 BTC dan kombinasi dari nilai Output sebesar 0.02047172 BTC, maka fee untuk transaksi adalah fee is 0.00071 BTC (71,000 satoshi).  Maka nilai feerate pada transaksi ini sebesar 500 sat/vB.

## Estimating Fee :

Read More Here : https://bitcoin.stackexchange.com/questions/92587/calculate-transaction-fee-for-external-addresses-which-doesnt-belong-to-my-loca/92600#92600

---------------------

