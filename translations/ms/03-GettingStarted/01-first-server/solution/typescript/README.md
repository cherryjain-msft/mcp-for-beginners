<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "ac67652abc453e2a7e2c75cd7a8897ae",
  "translation_date": "2025-07-13T18:06:40+00:00",
  "source_file": "03-GettingStarted/01-first-server/solution/typescript/README.md",
  "language_code": "ms"
}
-->
# Menjalankan contoh ini

Anda disarankan untuk memasang `uv` tetapi ia bukan wajib, lihat [arahan](https://docs.astral.sh/uv/#highlights)

## -1- Pasang kebergantungan

```bash
npm install
```

## -3- Jalankan contoh


```bash
npm run build
```

## -4- Uji contoh

Dengan pelayan berjalan di satu terminal, buka terminal lain dan jalankan arahan berikut:

```bash
npm run inspector
```

Ini sepatutnya memulakan pelayan web dengan antara muka visual yang membolehkan anda menguji contoh.

Setelah pelayan disambungkan:

- cuba senaraikan alat dan jalankan `add`, dengan argumen 2 dan 4, anda sepatutnya melihat 6 dalam hasilnya.
- pergi ke resources dan resource template dan panggil "greeting", taipkan nama dan anda akan melihat ucapan dengan nama yang anda berikan.

### Ujian dalam mod CLI

Inspector yang anda jalankan sebenarnya adalah aplikasi Node.js dan `mcp dev` adalah pembungkus di sekelilingnya.

Anda boleh melancarkannya terus dalam mod CLI dengan menjalankan arahan berikut:

```bash
npx @modelcontextprotocol/inspector --cli node ./build/index.js --method tools/list
```

Ini akan menyenaraikan semua alat yang tersedia di pelayan. Anda sepatutnya melihat output berikut:

```text
{
  "tools": [
    {
      "name": "add",
      "description": "Add two numbers",
      "inputSchema": {
        "type": "object",
        "properties": {
          "a": {
            "title": "A",
            "type": "integer"
          },
          "b": {
            "title": "B",
            "type": "integer"
          }
        },
        "required": [
          "a",
          "b"
        ],
        "title": "addArguments"
      }
    }
  ]
}
```

Untuk memanggil alat taip:

```bash
nnpx @modelcontextprotocol/inspector --cli node ./build/index.js --method tools/call --tool-name add --tool-arg a=1 --tool-arg b=2
```

Anda sepatutnya melihat output berikut:

```text
{
  "content": [
    {
      "type": "text",
      "text": "3"
    }
  ],
  "isError": false
}
```

> ![!TIP]
> Biasanya lebih cepat menjalankan inspector dalam mod CLI berbanding di pelayar.
> Baca lebih lanjut tentang inspector [di sini](https://github.com/modelcontextprotocol/inspector).

**Penafian**:  
Dokumen ini telah diterjemahkan menggunakan perkhidmatan terjemahan AI [Co-op Translator](https://github.com/Azure/co-op-translator). Walaupun kami berusaha untuk ketepatan, sila ambil maklum bahawa terjemahan automatik mungkin mengandungi kesilapan atau ketidaktepatan. Dokumen asal dalam bahasa asalnya harus dianggap sebagai sumber yang sahih. Untuk maklumat penting, terjemahan profesional oleh manusia adalah disyorkan. Kami tidak bertanggungjawab atas sebarang salah faham atau salah tafsir yang timbul daripada penggunaan terjemahan ini.