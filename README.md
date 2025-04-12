<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Form Penjualan</title>
  <style>
    * {
      box-sizing: border-box;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    body {
      background: #f9f9f9;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      margin: 0;
    }

    .container {
      background: #fff;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 5px 15px rgba(0,0,0,0.1);
      width: 100%;
      max-width: 400px;
    }

    h2 {
      text-align: center;
      margin-bottom: 20px;
      color: #333;
    }

    .form-group {
      margin-bottom: 15px;
    }

    label {
      display: block;
      margin-bottom: 6px;
      font-weight: bold;
      color: #444;
    }

    input, select {
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 8px;
      transition: border-color 0.3s;
    }

    input:focus, select:focus {
      border-color: #007bff;
      outline: none;
    }

    button {
      background: #007bff;
      color: white;
      padding: 12px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-weight: bold;
      font-size: 16px;
      width: 100%;
      transition: background 0.3s;
    }

    button:hover {
      background: #0056b3;
    }

    .success-msg {
      text-align: center;
      margin-top: 15px;
      color: green;
      font-weight: bold;
    }
  </style>
</head>
<body>

  <div class="container">
    <h2>Form Penjualan</h2>
    <form id="salesForm">
      <div class="form-group">
        <label>ID Gerobak</label>
        <input name="idGerobak" required>
      </div>
      <div class="form-group">
        <label>Lokasi</label>
        <input name="lokasi" required>
      </div>
      <div class="form-group">
        <label>Nama Penjual</label>
        <input name="namaPenjual" required>
      </div>
      <div class="form-group">
        <label>Nama Kue</label>
        <input name="namaKue" required>
      </div>
      <div class="form-group">
        <label>Harga</label>
        <input type="number" name="harga" required>
      </div>
      <div class="form-group">
        <label>Status</label>
        <select name="status" required>
          <option value="">Pilih Status</option>
          <option value="Sukses">Sukses</option>
          <option value="Gagal">Gagal</option>
        </select>
      </div>
      <button type="submit">Submit</button>
    </form>
  </div>

  <script>
    document.getElementById('salesForm').addEventListener('submit', function(e){
      e.preventDefault();
      const formData = new FormData(e.target);
      const data = Object.fromEntries(formData.entries());

      fetch("https://script.google.com/macros/s/AKfycbzqAEUvPndAxr9EFfRN-qIL_zkRAq2GpH-uI5_rX3s8p5N4c8Vz4yzMzmxL9CHI8w5qiA/exec", {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify(data)
      })
      .then(res => res.text())
      .then(msg => {
        alert("Data berhasil dikirim!");

        const printWindow = window.open('', '', 'width=600,height=400');
        printWindow.document.write(`
          <pre>
            STRUK PENJUALAN

            ID Gerobak   : ${data.idGerobak}
            Lokasi       : ${data.lokasi}
            Nama Penjual : ${data.namaPenjual}
            Nama Kue     : ${data.namaKue}
            Harga        : ${data.harga}
            Status       : ${data.status}

            Terima kasih 😊
          </pre>
        `);
        printWindow.document.close();
        printWindow.print();

        e.target.reset();
      })
      .catch(err => {
        alert("Gagal mengirim data!");
        console.error(err);
      });
    });
  </script>

</body>
</html>
