<!DOCTYPE html>
<html lang="pt-PT">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Esquema 3-4-2</title>
<style>
body {margin:0; font-family:Arial,sans-serif; background:orange; color:black; display:flex; flex-direction:column; min-height:100vh;}
header {background:orange; text-align:center; padding:1rem; font-size:2rem; font-weight:bold;}
.field {flex:1; display:flex; flex-direction:column; align-items:center; justify-content:space-around; background:#006400; margin:2rem; border:5px solid white; border-radius:15px; padding:1rem;}
.line {display:flex; justify-content:center; gap:1rem;}
.player {width:60px; height:60px; background:orange; border:2px solid black; border-radius:50%; display:flex; align-items:center; justify-content:center; font-size:0.8rem; cursor:pointer;}
#nameBox {background:white; padding:1rem; margin:1rem; border-radius:10px; display:flex; flex-wrap:wrap; gap:10px; justify-content:center; min-height:80px;}
.name {background:#ff8c00; padding:0.5rem 1rem; border-radius:5px; cursor:grab; user-select:none;}
</style>
</head>
<body>
<header>Terrão - 3-4-2</header>
<div id="nameBox">
  <div class="name">João</div>
  <div class="name">Maria</div>
  <div class="name">Pedro</div>
  <div class="name">Ana</div>
  <div class="name">Carlos</div>
  <div class="name">Sofia</div>
  <div class="name">Rafael</div>
  <div class="name">Isabela</div>
  <div class="name">Miguel</div>
  <div class="name">Lara</div>
  <div class="name">Lucas</div>
  <div class="name">Beatriz</div>
  <div class="name">Gustavo</div>
  <div class="name">Clara</div>
  <div class="name">Bruno</div>
</div>
<div class="field">
  <div class="line"><div class="player"></div></div>
  <div class="line"><div class="player"></div><div class="player"></div><div class="player"></div></div>
  <div class="line"><div class="player"></div><div class="player"></div><div class="player"></div><div class="player"></div></div>
  <div class="line"><div class="player"></div><div class="player"></div></div>
</div>

<script>
let dragged;

function setupDragAndDrop(elem) {
  elem.setAttribute('draggable', 'true');
  elem.addEventListener('dragstart', e => {
    dragged = e.target;
    setTimeout(() => e.target.style.opacity = '0.5', 0);
  });
  elem.addEventListener('dragend', e => {
    e.target.style.opacity = '1';
  });
}

// Inicializar drag nos nomes e jogadores
const allElements = document.querySelectorAll('.name, .player');
allElements.forEach(setupDragAndDrop);

const players = document.querySelectorAll('.player');
players.forEach(player => {
  player.addEventListener('dragover', e => e.preventDefault());
  player.addEventListener('drop', e => {
    e.preventDefault();
    if (dragged && dragged.classList.contains('name')) {
      if (player.textContent.trim() === '') {
        player.textContent = dragged.textContent;
        dragged.remove();
      }
    } else if (dragged && dragged.classList.contains('player')) {
      if (player.textContent.trim() === '' && dragged.textContent.trim() !== '') {
        player.textContent = dragged.textContent;
        dragged.textContent = '';
      }
    }
  });
});

// Permitir arrastar de volta para o nameBox
const nameBox = document.getElementById('nameBox');
nameBox.addEventListener('dragover', e => e.preventDefault());
nameBox.addEventListener('drop', e => {
  e.preventDefault();
  if (dragged && dragged.classList.contains('player') && dragged.textContent.trim() !== '') {
    const newName = document.createElement('div');
    newName.className = 'name';
    newName.textContent = dragged.textContent;
    setupDragAndDrop(newName);
    nameBox.appendChild(newName);
    dragged.textContent = '';
  }
});
</script>
</body>
</html>

