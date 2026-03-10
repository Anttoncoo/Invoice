<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Invoice UD Barokah Jaya</title>

<link rel="manifest" href="manifest.json">

<style>

body{
font-family:Arial;
margin:0;
background:linear-gradient(135deg,#001b44,#0b6cff,#b30000);
color:white;
}

.header{
background:black;
padding:15px;
text-align:center;
font-size:22px;
color:#c36bff;
font-weight:bold;
letter-spacing:2px;
}

.container{
padding:15px;
}

.box{
background:rgba(0,0,0,0.65);
padding:15px;
border-radius:10px;
}

.top{
display:flex;
gap:6px;
}

.top input{
flex:1;
padding:10px;
border:none;
border-radius:6px;
}

.inputRow{
display:grid;
grid-template-columns:40% 20% 15% 25%;
gap:5px;
margin-top:10px;
}

.inputRow input{
padding:10px;
border:none;
border-radius:6px;
width:100%;
}

.inputRow button{
background:#0b6cff;
color:white;
border:none;
border-radius:6px;
}

table{
width:100%;
margin-top:15px;
border-collapse:collapse;
}

th{
background:#111;
padding:8px;
}

td{
padding:8px;
border-bottom:1px solid #555;
}

.total{
margin-top:12px;
font-size:18px;
}

button{
width:100%;
padding:12px;
border:none;
border-radius:6px;
color:white;
font-size:16px;
margin-top:8px;
}

.hitung{background:#ff2b2b;}
.wa{background:#00b14f;}

</style>
</head>

<body>

<div class="header">
UD BAROKAH JAYA
</div>

<div class="container">

<div class="box">

<div class="top">
<input type="date" id="tanggal">
<input type="number" id="invoiceNo">
</div>

<div class="inputRow">
<input type="text" id="barang" placeholder="Nama Barang">
<input type="number" id="harga" placeholder="Harga">
<input type="number" id="qty" placeholder="Qty">
<button onclick="tambah()">Tambah</button>
</div>

<table id="tabel">

<tr>
<th>Barang</th>
<th>Harga</th>
<th>Qty</th>
<th>Subtotal</th>
</tr>

</table>

<div class="total">
Total : Rp <span id="total">0</span>
</div>

<input type="number" id="bayar" placeholder="Jumlah Bayar" style="padding:10px;border-radius:6px;border:none;width:100%;margin-top:10px;">

<button class="hitung" onclick="hitung()">Hitung Kembalian</button>

<div class="total">
Kembalian : Rp <span id="kembali">0</span>
</div>

<button class="wa" onclick="wa()">Kirim WhatsApp</button>

</div>

</div>

<script>

let total=0

/* NOMOR OTOMATIS */

let nomor=localStorage.getItem("invoice")

if(nomor==null){
nomor=1
}else{
nomor=parseInt(nomor)+1
}

document.getElementById("invoiceNo").value=nomor


/* TAMBAH BARANG */

function tambah(){

let barang=document.getElementById("barang").value
let harga=parseInt(document.getElementById("harga").value)
let qty=parseInt(document.getElementById("qty").value)

if(!barang || !harga || !qty){
alert("Isi data barang")
return
}

let sub=harga*qty
total+=sub

let tabel=document.getElementById("tabel")

let row=tabel.insertRow()

row.insertCell(0).innerHTML=barang
row.insertCell(1).innerHTML=harga
row.insertCell(2).innerHTML=qty
row.insertCell(3).innerHTML=sub

document.getElementById("total").innerHTML=total

document.getElementById("barang").value=""
document.getElementById("harga").value=""
document.getElementById("qty").value=""

}


/* HITUNG KEMBALIAN */

function hitung(){

let bayar=parseInt(document.getElementById("bayar").value)

let kembali=bayar-total

document.getElementById("kembali").innerHTML=kembali

}


/* WHATSAPP */

function wa(){

let nomor=document.getElementById("invoiceNo").value
let tanggal=document.getElementById("tanggal").value

localStorage.setItem("invoice",nomor)

let text="Invoice UD Barokah Jaya%0A"
text+="No : "+nomor+"%0A"
text+="Tanggal : "+tanggal+"%0A"
text+="Total : Rp "+total

window.open("https://wa.me/?text="+text)

}

</script>

</body>
</html>
