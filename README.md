# cark-felek
<!DOCTYPE html><html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>İsimli Çarkıfelek</title>
    <style>
        body { text-align: center; font-family: Arial, sans-serif; }
        .wheel-container { position: relative; width: 300px; height: 300px; margin: 50px auto; }
        .wheel { width: 100%; height: 100%; border-radius: 50%; border: 5px solid #000; transition: transform 3s ease-out; }
        .arrow { position: absolute; top: -20px; left: 50%; transform: translateX(-50%); font-size: 30px; }
        .button { margin-top: 20px; padding: 10px 20px; font-size: 18px; cursor: pointer; }
    </style>
</head>
<body>
    <h1>İsimli Çarkıfelek</h1>
    <div class="wheel-container">
        <div class="arrow">▼</div>
        <canvas id="wheelCanvas" class="wheel"></canvas>
    </div>
    <button class="button" onclick="spinWheel()">Çarkı Çevir</button>
    <p id="result"></p><script>
    const names = ["Kardelen", "Dark", "Azap", "Taha"];
    const canvas = document.getElementById("wheelCanvas");
    const ctx = canvas.getContext("2d");
    const size = names.length;
    const arc = (2 * Math.PI) / size;
    let rotation = 0;

    canvas.width = 300;
    canvas.height = 300;

    function drawWheel() {
        for (let i = 0; i < size; i++) {
            ctx.beginPath();
            ctx.fillStyle = i % 2 === 0 ? "#f4a261" : "#2a9d8f";
            ctx.moveTo(150, 150);
            ctx.arc(150, 150, 150, i * arc, (i + 1) * arc);
            ctx.lineTo(150, 150);
            ctx.fill();
            ctx.fillStyle = "#fff";
            ctx.font = "16px Arial";
            ctx.textAlign = "center";
            ctx.fillText(names[i], 150 + Math.cos(i * arc + arc / 2) * 100, 150 + Math.sin(i * arc + arc / 2) * 100);
        }
    }

    function spinWheel() {
        let randomSpin = Math.floor(3600 + Math.random() * 360);
        rotation += randomSpin;
        document.querySelector(".wheel").style.transform = `rotate(${rotation}deg)`;
        setTimeout(() => {
            let index = Math.floor(((rotation % 360) / 360) * size);
            document.getElementById("result").textContent = "Kazanan: " + names[size - 1 - index];
        }, 3000);
    }

    drawWheel();
</script>

</body>
</html>
