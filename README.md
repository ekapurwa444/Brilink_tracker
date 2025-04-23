# Brilink_tracker
Web catatan transaksi Brilink
<!DOCTYPE html><html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Catatan Brilink</title>
  <style>
    body { font-family: sans-serif; padding: 20px; }
    input, select, button { margin: 5px; padding: 5px; }
    table { width: 100%; border-collapse: collapse; margin-top: 20px; }
    th, td { border: 1px solid #aaa; padding: 8px; text-align: left; }
  </style>
</head>
<body>
  <h2>Catatan Transaksi Brilink</h2><label>Nama Nasabah: <input type="text" id="nama"></label> <label>Jenis Transaksi: <select id="jenis"> <option>Setor Tunai</option> <option>Tarik Tunai</option> <option>Transfer</option> <option>Bayar Tagihan</option> </select> </label> <label>Jumlah: <input type="number" id="jumlah"></label> <button onclick="tambahData()">Simpan</button> <button onclick="downloadExcel()">Download Excel</button>

  <table id="tabel">
    <thead>
      <tr>
        <th>Tanggal</th>
        <th>Nama</th>
        <th>Jenis</th>
        <th>Jumlah</th>
      </tr>
    </thead>
    <tbody></tbody>
  </table>  <script>
    let data = [];

    function tambahData() {
      const nama = document.getElementById('nama').value;
      const jenis = document.getElementById('jenis').value;
      const jumlah = document.getElementById('jumlah').value;
      const tanggal = new Date().toLocaleDateString();

      if (nama && jumlah) {
        data.push({ tanggal, nama, jenis, jumlah });
        renderTabel();
        document.getElementById('nama').value = '';
        document.getElementById('jumlah').value = '';
      } else {
        alert('Isi semua data!');
      }
    }

    function renderTabel() {
      const tbody = document.querySelector('#tabel tbody');
      tbody.innerHTML = '';
      data.forEach(row => {
        const tr = document.createElement('tr');
        tr.innerHTML = `<td>${row.tanggal}</td><td>${row.nama}</td><td>${row.jenis}</td><td>${row.jumlah}</td>`;
        tbody.appendChild(tr);
      });
    }

    function downloadExcel() {
      let csv = 'Tanggal,Nama,Jenis,Jumlah\n';
      data.forEach(row => {
        csv += `${row.tanggal},${row.nama},${row.jenis},${row.jumlah}\n`;
      });

      const blob = new Blob([csv], { type: 'text/csv' });
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = 'catatan_brilink.csv';
      a.click();
    }
  </script></body>
</html>
