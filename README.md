# Ahmetst
Site
<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<title>Şifre Üretici</title>
<style>
  body { font-family: Arial; padding: 20px; background: #111; color: #eee; }
  button { margin: 5px; padding: 10px; cursor: pointer; }
  input { width: 300px; padding: 5px; margin-right: 5px; }
</style>
</head>
<body>
<h2>Şifre Üretici</h2>

<div>
  <input type="text" id="daily" readonly>
  <button onclick="copyToClipboard('daily')">Günlük Kopyala</button>
</div>
<div>
  <input type="text" id="weekly" readonly>
  <button onclick="copyToClipboard('weekly')">Haftalık Kopyala</button>
</div>
<div>
  <input type="text" id="monthly" readonly>
  <button onclick="copyToClipboard('monthly')">Aylık Kopyala</button>
</div>

<script>
// Basit şifre üretici fonksiyonu
function generatePassword(seed) {
    let hash = 0;
    for (let i = 0; i < seed.length; i++) {
        hash = seed.charCodeAt(i) + ((hash << 5) - hash);
    }
    let pass = '';
    const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%&*';
    for (let i = 0; i < 12; i++) { // 12 karakterli şifre
        pass += chars[Math.abs(hash + i) % chars.length];
    }
    return pass;
}

// Tarih bazlı seedler
const today = new Date();
const dailySeed = today.toDateString();
const weeklySeed = `${today.getFullYear()}-W${Math.ceil(today.getDate()/7)}`;
const monthlySeed = `${today.getFullYear()}-${today.getMonth()+1}`;

// Şifreleri oluştur ve inputlara yaz
document.getElementById('daily').value = generatePassword(dailySeed);
document.getElementById('weekly').value = generatePassword(weeklySeed);
document.getElementById('monthly').value = generatePassword(monthlySeed);

// Clipboard kopyalama fonksiyonu
function copyToClipboard(id) {
    const input = document.getElementById(id);
    input.select();
    input.setSelectionRange(0, 99999);
    navigator.clipboard.writeText(input.value).then(() => {
        alert(id + ' şifre kopyalandı!');
    });
}
</script>
</body>
</html>
