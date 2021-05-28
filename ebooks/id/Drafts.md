# Belajar Dengan Jenius Cryptocurrency Trading

## Penulis : Gun Gun Febrianza

# Drafts

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

Each Non-Segwit byte of data is counted is 4 WU when determining size. 

Setiap transaksi terdiri dari beberapa fields berikut :

- Version (4 bytes)
- \# of Inputs (VarInt, 1 byte for numbers up to 252)
- Inputs (varies)
- \# of Outputs (VarInt, 1 byte for numbers up to 252)
- Outputs (varies)
- Locktime (4 bytes)

Let's break each of these fields down by looking at a [non-segwit raw transaction](https://blockstream.info/tx/791bd9b3bda632ee1757de37db8939b0287ece4753f3077b9a5f5c7e28545967): ``

`0200000001d2eed35b0d55763981c635cab7788c28e3683af3d329947a17d7f6005390e6ef010000006a47304402200ffaac8f12e56f4af66109220812b76c7d6bb0e5906cf2de235b79496b3e080b0220037304894b648fa0b50e0d82ef9f58b537233ee282ab31fc04fb3d169d2c97cc0121030120a287eb98922752a89b39df64f7f3314036f6f096341c9189b0cb3c692aaeffffffff02404ff200000000001976a9140b818b11f9624e6a2d5b757a3e8fe45db3f6647788ace0b4b401000000001976a914a1e5e47fce1c5c0868107dba3851eb696c2ead5388ac00000000`

### Version

Versi dari transaksi ini adalah `02000000` (2 in little-endian), ukuran versi selalu 4 bytes (16 WU)



---------------------
