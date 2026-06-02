<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<title>PixelAI</title>

<style>
body{
  margin:0;
  font-family:Arial;
  background:#0b1220;
  color:white;
  display:flex;
  justify-content:center;
  align-items:center;
  height:100vh;
}

.box{ width:780px; }

h1{ text-align:center; }

input{
  width:100%;
  padding:12px;
  border-radius:8px;
  border:none;
}

button{
  width:100%;
  margin-top:10px;
  padding:12px;
  border:none;
  border-radius:8px;
  background:#22c55e;
  cursor:pointer;
}

#out{
  margin-top:15px;
  background:#111a2e;
  padding:15px;
  border-radius:8px;
  height:260px;
  overflow-y:auto;
  white-space:pre-wrap;
}

.info{
  text-align:center;
  font-size:12px;
  color:#94a3b8;
  margin-top:10px;
}
</style>
</head>

<body>

<div class="box">

<h1>PixelAI</h1>

<input id="q" placeholder="Bir şey yaz..." />
<button onclick="ask()">Gönder</button>

<div id="out"></div>

<div class="info">
Soru kapasitesi: sınırsız
</div>

</div>

<script>

document.getElementById("q").addEventListener("keypress", e=>{
  if(e.key==="Enter") ask();
});

function isMath(q){
  return /^[0-9+\-*/(). ]+$/.test(q);
}

function ask(){
  const q = document.getElementById("q").value.trim().toLowerCase();
  const out = document.getElementById("out");

  if(!q) return;

  document.getElementById("q").value = "";
  out.innerText = cevap(q);
}

// 🌍 MEGA BİLGİ BANKASI
function bilgi(q){

  if(q.includes("uzay")){
    if(q.includes("kaç evren")) return "Şu an bilim sadece 1 evren olduğunu kabul eder.";
    if(q.includes("kara delik")) return "Kara delik ışığın bile kaçamadığı bölgedir.";
    if(q.includes("galaksi")) return "Milyarlarca galaksi olduğu düşünülmektedir.";
    return "Uzay çok geniştir ve büyük kısmı bilinmemektedir.";
  }

  if(q.includes("kaç gezegen")) return "Güneş sisteminde 8 gezegen vardır.";
  if(q.includes("dünya")) return "Dünya 3. gezegendir.";
  if(q.includes("güneş")) return "Güneş bir yıldızdır.";
  if(q.includes("ay")) return "Ay Dünya'nın uydusudur.";

  if(q.includes("atom")) return "Atom maddenin en küçük yapı taşıdır.";
  if(q.includes("robot")) return "Robotlar programlanabilen makinelerdir.";
  if(q.includes("insan")) return "İnsan gelişmiş bir canlıdır.";

  if(q.includes("türkiye")) return "Türkiye iki kıtada yer alan bir ülkedir.";
  if(q.includes("internet")) return "İnternet dünya genelinde bilgi ağıdır.";
  if(q.includes("okul")) return "Okul eğitim kurumudur.";

  return null;
}

// 🧠 EN ÇOK SORULANLAR
function popular(q){

  if(q.includes("nasılsın")) return "İyiyim, teşekkür ederim.";
  if(q.includes("napıyon") || q.includes("napıyorsun")) return "İyiyim, sen napıyon?";
  if(q.includes("sıkıldım")) return "İstersen sana soru sorabilirim.";
  if(q.includes("yardım")) return "Hangi konuda yardım istiyorsun?";
  if(q.includes("neden")) return "Sebebi değişebilir.";
  if(q.includes("nasıl")) return "Adım adım açıklayabilirim.";

  // 😄 DUYGU SİSTEMİ (YENİ EKLENDİ)
  if(q.includes("bende iyiyim") || q.includes("iyiyim") || q.includes("iyim")){
    return "Güzel 👍 sorularını alayım";
  }

  if(
    q.includes("kötüyüm") ||
    q.includes("üzgünüm") ||
    q.includes("moralim bozuk") ||
    q.includes("berbatım")
  ){
    return "Geçmiş olsun 😔 neyse sorularını alayım";
  }

  return null;
}

// 🧠 ANA CEVAP
function cevap(q){

  // 🧮 MATEMATİK
  if(isMath(q)){
    try{
      return "Sonuç: " + eval(q);
    }catch{
      return "Hatalı işlem.";
    }
  }

  // 🤝 SELAM
  if(q.includes("selam")) return "Selam 👋";
  if(q.includes("merhaba")) return "Merhaba 👋";

  // 💬 POPULAR + DUYGU
  const p = popular(q);
  if(p) return p;

  // 🌍 BİLGİ
  const b = bilgi(q);
  if(b) return b;

  // 🧠 FALLBACK
  const list = [
    "Bunu tam anlayamadım.",
    "Biraz daha açık yazar mısın?",
    "İlginç bir soru.",
    "Bu konu biraz karmaşık.",
    "Daha fazla bilgi lazım."
  ];

  return list[Math.floor(Math.random()*list.length)];
}

</script>

</body>
</html>

