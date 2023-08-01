# PROSES PEMBUATAN TABULASI SILANG

## Penjelasan nya :
##### - Mengenai Data tentang penyebab-penyebab kematian di Indonesia.
1. Pertama, import data ke dalam Spreadsheet.
2. Kemudian setelah data di import ke dalam Spreadsheet, langkah selanjutnya masuk ke ekstensi lalu masuk ke Apps Script beri judul dan masukkan kode berikut :

- function causeAndYear() {
  let ss = SpreadsheetApp.getActiveSpreadsheet();
  let sheet = ss.getSheetByName('Penyebab Kematian di Indonesia yang Dilaporkan - Clean');
  let numberRows = sheet.getLastRow();
  let numberCols = sheet.getLastColumn();

  let data = sheet.getRange(2, 1, numberRows-1, numberCols).getValues();

  // Get unique causes and years
  let causes = [];
  let years = [];
  for (let i = 0; i < data.length; i++) {
    let cause = data[i][0];
    let year = data[i][2];
    if (causes.indexOf(cause) == -1) causes.push(cause);
    if (years.indexOf(year) == -1) years.push(year);
  }
  
  // Sort years in ascending order
  years.sort((a, b) => a - b);

  // Create new sheet
  let newSheet = ss.insertSheet('Penyebab Kematian di Indonesia');
  newSheet.getRange('A1').setValue('Cause');
  for (let i = 0; i < years.length; i++) {
    newSheet.getRange(1, i + 2).setValue(years[i]);
  }

  // Calculate totals and add to sheet
  for (let i = 0; i < causes.length; i++) {
    let cause = causes[i];
    newSheet.getRange(i + 2, 1).setValue(cause);
    for (let j = 0; j < years.length; j++) {
      let year = years[j];
      let totalDeaths = 0;
      for (let k = 0; k < data.length; k++) {
        if (data[k][0] == cause && data[k][2] == year) {
          totalDeaths += Number(data[k][4]);
        }
      }
      newSheet.getRange(i + 2, j + 2).setValue(totalDeaths);
    }
  }
}

## Berikut adalah penjelasan mengenai bagian-bagian utama dari kode tersebut:
1. SpreadsheetApp.getActiveSpreadsheet(): Fungsi ini digunakan untuk mendapatkan objek Spreadsheet aktif yang sedang dibuka.

2. ss.getSheetByName('Penyebab Kematian di Indonesia yang Dilaporkan - Clean'): Fungsi ini digunakan untuk mendapatkan lembar kerja (sheet) dari Spreadsheet berdasarkan nama lembar kerjanya, yaitu 'Penyebab Kematian di Indonesia yang Dilaporkan - Clean'.

3. sheet.getLastRow(): Fungsi ini digunakan untuk mendapatkan indeks baris terakhir yang berisi data pada lembar kerja.

4. sheet.getLastColumn(): Fungsi ini digunakan untuk mendapatkan indeks kolom terakhir yang berisi data pada lembar kerja.

5. sheet.getRange(2, 1, numberRows-1, numberCols).getValues(): Fungsi ini digunakan untuk mendapatkan data dari seluruh sel pada lembar kerja, kecuali baris header pertama, dalam bentuk array dua dimensi.

6. Pengolahan data untuk mendapatkan daftar unik penyebab kematian dan tahun-tahun yang ada pada data:

- causes: Array yang akan menyimpan daftar unik penyebab kematian.
- years: Array yang akan menyimpan daftar unik tahun-tahun.

7. years.sort((a, b) => a - b): Mengurutkan tahun-tahun dalam array years secara ascending (berurutan dari kecil ke besar).

8. ss.insertSheet('Penyebab Kematian di Indonesia'): Fungsi ini digunakan untuk membuat lembar kerja baru dengan nama 'Penyebab Kematian di Indonesia'.

9. newSheet.getRange('A1').setValue('Cause'): Menempatkan label 'Cause' pada sel A1 pada lembar kerja baru.

10. Menempatkan tahun-tahun unik sebagai label kolom pada lembar kerja baru.

11. Melakukan perhitungan total kematian berdasarkan penyebab dan tahun, dan menempatkan hasilnya pada lembar kerja baru.

- Fungsi _causeAndYear_ ini pada dasarnya melakukan pengolahan data untuk membuat lembar kerja baru yang berisi total kematian berdasarkan penyebab dan tahun-tahun tertentu. Dengan demikian, data yang awalnya disajikan dalam format tabel akan diolah menjadi format yang lebih ringkas dan mudah dipahami.

## Struktur data yang digunakan :
- Array dua dimensi digunakan untuk mewakili data dalam bentuk tabel, di mana setiap baris pada lembar kerja akan diwakili oleh satu elemen array, dan setiap elemen array akan berisi nilai-nilai dari sel-sel pada baris tersebut. Dengan demikian, data pada lembar kerja dapat diakses dan diolah menggunakan indeks baris dan kolom.

##### - Mengenai data tentang jumlah kematian di Indonesia berdasarkan tahun dan tipe.

1. Pertama, import data ke dalam Spreadsheet.
2. Kemudian setelah data di import ke dalam Spreadsheet, langkah selanjutnya masuk ke ekstensi lalu masuk ke Apps Script beri judul dan masukkan kode berikut :

- function causeAndYear() {
  let ss = SpreadsheetApp.getActiveSpreadsheet();
  let sheet = ss.getSheetByName('Penyebab Kematian di Indonesia yang Dilaporkan - Clean');
  let numberRows = sheet.getLastRow();
  let numberCols = sheet.getLastColumn();

  let data = sheet.getRange(2, 1, numberRows-1, numberCols).getValues();

  // Get unique causes and years
  let causes = [];
  let years = [];
  for (let i = 0; i < data.length; i++) {
    let cause = data[i][0];
    let year = data[i][2];
    if (causes.indexOf(cause) == -1) causes.push(cause);
    if (years.indexOf(year) == -1) years.push(year);
  }
  
  // Sort years in ascending order
  years.sort((a, b) => a - b);

  // Create new sheet
  let newSheet = ss.insertSheet('Penyebab Kematian di Indonesia');
  newSheet.getRange('A1').setValue('Cause');
  for (let i = 0; i < years.length; i++) {
    newSheet.getRange(1, i + 2).setValue(years[i]);
  }

  // Calculate totals and add to sheet
  for (let i = 0; i < causes.length; i++) {
    let cause = causes[i];
    newSheet.getRange(i + 2, 1).setValue(cause);
    for (let j = 0; j < years.length; j++) {
      let year = years[j];
      let totalDeaths = 0;
      for (let k = 0; k < data.length; k++) {
        if (data[k][0] == cause && data[k][2] == year) {
          totalDeaths += Number(data[k][4]);
        }
      }
      newSheet.getRange(i + 2, j + 2).setValue(totalDeaths);
    }
  }
}

## Berikut adalah penjelasan mengenai cara kerja fungsi causeAndYear:

1. Fungsi causeAndYear diawali dengan mendapatkan objek Spreadsheet aktif menggunakan SpreadsheetApp.getActiveSpreadsheet() dan menyimpannya dalam variabel ss.

2. Selanjutnya, fungsi ini mencari lembar kerja dengan nama "Penyebab Kematian di Indonesia yang Dilaporkan - Clean" menggunakan ss.getSheetByName('Penyebab Kematian di Indonesia yang Dilaporkan - Clean') dan menyimpannya dalam variabel sheet.

3. Untuk menghitung jumlah baris dan kolom pada lembar kerja, fungsi ini menggunakan getLastRow() dan getLastColumn() dan menyimpannya dalam variabel numberRows dan numberCols.

4. Data dari lembar kerja diambil menggunakan getRange() dengan parameter (baris mulai, kolom mulai, jumlah baris, jumlah kolom) dan disimpan dalam variabel data.

5. Fungsi ini mencari penyebab dan tahun unik dari data yang diambil dan menyimpannya dalam array causes dan years menggunakan loop for.

6. Array years diurutkan secara menaik menggunakan sort().

7. Selanjutnya, fungsi ini membuat lembar kerja baru dengan nama "Penyebab Kematian di Indonesia" menggunakan insertSheet('Penyebab Kematian di Indonesia') dan menyimpannya dalam variabel newSheet.

8. Judul "Cause" ditulis pada sel A1 pada lembar kerja baru menggunakan setValue('Cause').

9. Tahun-tahun unik ditulis pada baris pertama dari kolom B hingga kolom terakhir pada lembar kerja baru menggunakan loop for.

- Fungsi ini menghitung total kematian untuk setiap penyebab dan tahun, dan hasilnya ditulis pada lembar kerja baru sesuai dengan penyebab dan tahunnya menggunakan nested loop for.

- Setelah selesai, data hasil perhitungan telah disimpan dengan rapi pada lembar kerja baru "Penyebab Kematian di Indonesia".

##### Setelah semua telah di masukkan, langkah selanjutnya tinggal menjalankan 