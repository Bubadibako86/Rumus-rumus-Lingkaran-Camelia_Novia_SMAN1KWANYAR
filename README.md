<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Rumus Lingkaran</title>
<style>
    body {
        margin: 0;
        font-family: Arial;
        background: linear-gradient(#ffb6c1, #ff69b4);
    }
    .container {
        padding: 20px;
        text-align: center;
    }
    input, button, select {
        padding: 10px;
        margin: 10px;
        border-radius: 8px;
        border: none;
        background: #c2185b;
        color: white;
    }
    .top-right {
        position: fixed;
        top: 10px;
        right: 15px;
        font-weight: bold;
    }
    .menu {
        position: fixed;
        top: 10px;
        left: 15px;
        cursor: pointer;
    }
    .back {
        position: fixed;
        bottom: 15px;
        left: 15px;
        padding: 10px 20px;
        background: #880e4f;
        color: white;
        border-radius: 8px;
        cursor: pointer;
    }
    .hidden {
        display: none;
    }
</style>
</head>
<body>

<div class="top-right" id="displayName"></div>
<div class="menu">☰</div>
<div class="back hidden" id="backBtn" onclick="goBack()">Kembali</div>

<div class="container" id="page1">
    <h2>Masukkan Nama Anda</h2>
    <input type="text" id="namaInput" placeholder="Nama" /> <br>
    <button onclick="saveName()">Lanjut</button>
</div>

<div class="container hidden" id="menuPage">
    <h2>Pilih Fitur</h2>
    <button onclick="openPage('taliMenu')">Panjang Tali Busur</button><br>
    <button onclick="openPage('busurPage')">Panjang Busur</button><br>
    <button onclick="openPage('juringLuasPage')">Luas Juring</button><br>
    <button onclick="openPage('juringKelPage')">Keliling Juring</button><br>
    <button onclick="openPage('temberengLuasPage')">Luas Tembereng</button><br>
    <button onclick="openPage('temberengKelPage')">Keliling Tembereng</button>
</div>

<!-- Tali Busur Menu -->
<div class="container hidden" id="taliMenu">
    <h2>Metode Panjang Tali Busur</h2>
    <button onclick="openPage('taliApotemaPage')">Jika diketahui Apotema</button><br>
    <button onclick="openPage('taliSudutPage')">Jika diketahui jari-jari & sudut</button>
</div>

<!-- Tali Busur - Apotema -->
<div class="container hidden" id="taliApotemaPage">
    <h2>Panjang Tali Busur (Apotema)</h2>
    <input id="r1" type="number" placeholder="r (jari-jari)"> <br>
    <input id="d1" type="number" placeholder="d (apotema)"> <br>
    <button onclick="hitungTaliApotema()">Hitung</button>
    <p id="hasilTaliApotema"></p>
</div>

<!-- Tali Busur - Sudut -->
<div class="container hidden" id="taliSudutPage">
    <h2>Panjang Tali Busur (Sudut)</h2>
    <input id="r2" type="number" placeholder="r (jari-jari)"> <br>
    <input id="a2" type="number" placeholder="∅ (sudut)"> <br>
    <button onclick="hitungTaliSudut()">Hitung</button>
    <p id="hasilTaliSudut"></p>
</div>

<!-- Panjang Busur -->
<div class="container hidden" id="busurPage">
    <h2>Panjang Busur</h2>
    <input id="a3" type="number" placeholder="a (sudut)"> <br>
    <input id="r3" type="number" placeholder="r (jari-jari)"> <br>
    <button onclick="hitungPanjangBusur()">Hitung</button>
    <p id="hasilBusur"></p>
</div>

<!-- Luas Juring -->
<div class="container hidden" id="juringLuasPage">
    <h2>Luas Juring</h2>
    <input id="a4" type="number" placeholder="a (sudut)"> <br>
    <input id="r4" type="number" placeholder="r (jari-jari)"> <br>
    <button onclick="hitungLuasJuring()">Hitung</button>
    <p id="hasilLuasJuring"></p>
</div>

<!-- Keliling Juring -->
<div class="container hidden" id="juringKelPage">
    <h2>Keliling Juring</h2>
    <input id="a5" type="number" placeholder="a (sudut)"> <br>
    <input id="r5" type="number" placeholder="r (jari-jari)"> <br>
    <button onclick="hitungKelJuring()">Hitung</button>
    <p id="hasilKelJuring"></p>
</div>

<!-- Luas Tembereng -->
<div class="container hidden" id="temberengLuasPage">
    <h2>Luas Tembereng</h2>
    <input id="a6" type="number" placeholder="a (sudut)"> <br>
    <input id="t6" type="number" placeholder="t (tinggi)"> <br>
    <input id="A6" type="number" placeholder="A (alas)"> <br>
    <input id="r6" type="number" placeholder="r (jari-jari)"> <br>
    <button onclick="hitungLuasTembereng()">Hitung</button>
    <p id="hasilLuasTembereng"></p>
</div>

<!-- Keliling Tembereng -->
<div class="container hidden" id="temberengKelPage">
    <h2>Keliling Tembereng</h2>
    <input id="a7" type="number" placeholder="a (sudut)"> <br>
    <input id="d7" type="number" placeholder="d (apotema)"> <br>
    <input id="o7" type="number" placeholder="∅ (sudut)"> <br>
    <input id="r7" type="number" placeholder="r (jari-jari)"> <br>
    <button onclick="hitungKelTembereng()">Hitung</button>
    <p id="hasilKelTembereng"></p>
</div>

<script>
let historyStack = [];

function saveName() {
    const nama = document.getElementById('namaInput').value;
    document.getElementById('displayName').textContent = nama;
    openPage('menuPage');
}

function openPage(id) {
    document.querySelectorAll('.container').forEach(p => p.classList.add('hidden'));
    document.getElementById(id).classList.remove('hidden');
    historyStack.push(id);
    document.getElementById('backBtn').classList.remove('hidden');
}

function goBack() {
    historyStack.pop();
    const last = historyStack[historyStack.length - 1];
    if (!last) location.reload();
    document.querySelectorAll('.container').forEach(p => p.classList.add('hidden'));
    document.getElementById(last).classList.remove('hidden');
}

function pi(r) {
    return r % 7 === 0 ? 22/7 : 3.14;
}

function hitungTaliApotema() {
    let r = Number(r1.value), d = Number(d1.value);
    let hasil = 2 * Math.sqrt(r*r - d*d);
    hasilTaliApotema.textContent = "Hasil: " + hasil;
}

function hitungTaliSudut() {
    let r = Number(r2.value), a = Number(a2.value);
    let hasil = 2 * r * Math.sin((a * Math.PI / 180) / 2);
    hasilTaliSudut.textContent = "Hasil: " + hasil;
}

function hitungPanjangBusur() {
    let a = Number(a3.value), r = Number(r3.value);
    let p = pi(r);
    let hasil = a/360 * 2 * p * r;
    hasilBusur.textContent = "Hasil: " + hasil;
}

function hitungLuasJuring() {
    let a = Number(a4.value), r = Number(r4.value);
    let p = pi(r);
    let hasil = a/360 * p * r*r;
    hasilLuasJuring.textContent = "Hasil: " + hasil;
}

function hitungKelJuring() {
    let a = Number(a5.value), r = Number(r5.value);
    let p = pi(r);
    let hasil = 2*r + (a/360) * (2 * p * r);
    hasilKelJuring.textContent = "Hasil: " + hasil;
}

function hitungLuasTembereng() {
    let a = Number(a6.value), t = Number(t6.value), A = Number(A6.value), r = Number(r6.value);
    let p = pi(r);
    let hasil = a/360 * p * r*r - 0.5 * A * t;
    hasilLuasTembereng.textContent = "Hasil: " + hasil;
}

function hitungKelTembereng() {
    let a = Number(a7.value), d = Number(d7.value), o = Number(o7.value), r = Number(r7.value);
    let p = pi(r);
    let rumus1 = 2 * Math.sqrt(r*r - d*d) + a/360 * 2 * p * r;
    let rumus2 = 2 * r * Math.sin((o * Math.PI / 180) / 2);
    hasilKelTembereng.innerHTML = "Rumus 1: " + rumus1 + "<br>Rumus 2: " + rumus2;
}
</script>

</body>
</html>
