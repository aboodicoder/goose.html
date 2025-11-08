<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Emoji Goose 🪿</title>
<style>
body {
  margin: 0;
  overflow: hidden;
  background: linear-gradient(180deg, #b3eaff, #f7f7f7);
  height: 100vh;
  cursor: default; /* Regular cursor */
}

#goose {
  position: absolute;
  font-size: 100px;
  pointer-events: auto;
  user-select: none;
}

#crying {
  position: fixed;
  bottom: 10px;
  left: 10px;
  font-size: 24px;
  color: #3498db;
  display: none;
  user-select: none;
  pointer-events: none;
}
</style>
</head>
<body>

<div id="goose">🪿</div>
<div id="crying">😢 Goose is sad!</div>

<script>
const goose = document.getElementById('goose');
const crying = document.getElementById('crying');

let mouseX = window.innerWidth/2;
let mouseY = window.innerHeight/2;
let gooseX = 100;
let gooseY = 100;
let hugging = false;
let caught = false;

document.addEventListener('mousemove', e => {
  mouseX = e.clientX;
  mouseY = e.clientY;
  caught = false;
  crying.style.display = 'none';
});

// Goose chasing cursor slowly
function moveGoose(){
  const dx = mouseX - gooseX;
  const dy = mouseY - gooseY;
  const dist = Math.sqrt(dx*dx + dy*dy);

  if(!hugging){
    if(dist>10){
      gooseX += dx*0.01; // slow movement
      gooseY += dy*0.01;
    }

    if(dist<50 && !hugging){
      hugging = true;
      caught = true;
      setTimeout(()=>{ hugging=false; }, 2000);
    }
  }

  goose.style.left = gooseX+'px';
  goose.style.top = gooseY+'px';
}

// Goose cries if not caught after 19s
setTimeout(()=>{
  if(!caught){
    crying.style.display='block';
  }
},19000);

// Click goose to make happy
goose.addEventListener('click', ()=>{
  crying.style.display='none';
});

setInterval(moveGoose,20);
</script>

</body>
</html>
