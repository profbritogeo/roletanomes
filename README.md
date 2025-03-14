<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Roleta de Sorteio</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 50px;
        }
        .roleta-container {
            position: relative;
            display: inline-block;
        }
        .roleta {
            width: 400px;
            height: 400px;
            border: 5px solid black;
            border-radius: 50%;
            transition: transform 5s cubic-bezier(0.17, 0.67, 0.83, 0.67);
        }
        .botao {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
        }
        .seta {
            position: absolute;
            top: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 0;
            height: 0;
            border-left: 10px solid transparent;
            border-right: 10px solid transparent;
            border-bottom: 20px solid black;
        }
    </style>
</head>
<body>
    <h1>Roleta de Sorteio</h1>
    <div class="roleta-container">
        <div class="seta"></div>
        <canvas id="roleta" width="400" height="400"></canvas>
    </div>
    <br>
    <button class="botao" onclick="girarRoleta()">Girar</button>
    <p id="resultado"></p>

    <script>
        const canvas = document.getElementById("roleta");
        const ctx = canvas.getContext("2d");
        const nomes = [
            "Ana", "Arthur", "Beatriz", "Bruno", "Caio", "Carla", "Daniel", "Diana", "Eduardo", "Elisa", 
            "Felipe", "Fernanda", "Gabriela", "Gustavo", "Helena", "Hugo", "Igor", "Isabela", "João", "Juliana", 
            "Karina", "Kauê", "Larissa", "Lucas", "Mariana", "Matheus", "Nathan", "Nina", "Olivia", "Otávio", 
            "Paula", "Pedro", "Quintino", "Rafaela", "Raquel", "Samuel", "Sofia", "Tatiana", "Thiago", "Ulisses", 
            "Ursula", "Vanessa", "Vinicius", "Wanessa", "William", "Xavier", "Yago", "Yasmin", "Zoe", "Zélia"
        ];
        const numSetores = nomes.length;
        const anguloSetor = (2 * Math.PI) / numSetores;
        let anguloAtual = 0;
        
        function desenharRoleta() {
            for (let i = 0; i < numSetores; i++) {
                ctx.beginPath();
                ctx.moveTo(200, 200);
                ctx.arc(200, 200, 200, i * anguloSetor, (i + 1) * anguloSetor);
                ctx.fillStyle = i % 2 === 0 ? "#FFD700" : "#FF4500";
                ctx.fill();
                ctx.stroke();
                
                ctx.save();
                ctx.translate(200, 200);
                ctx.rotate(i * anguloSetor + anguloSetor / 2);
                ctx.textAlign = "right";
                ctx.fillStyle = "black";
                ctx.font = "14px Arial";
                ctx.fillText(nomes[i], 180, 5);
                ctx.restore();
            }
        }
        desenharRoleta();

        function girarRoleta() {
            let indiceSorteado = Math.floor(Math.random() * numSetores);
            let rotacaoFinal = 360 * 10 + indiceSorteado * (360 / numSetores);
            anguloAtual += rotacaoFinal;
            
            canvas.style.transition = "transform 5s ease-out";
            canvas.style.transform = `rotate(${anguloAtual}deg)`;
            
            setTimeout(() => {
                document.getElementById("resultado").textContent = `Nome sorteado: ${nomes[indiceSorteado]}`;
            }, 5000);
        }
    </script>
</body>
</html>
