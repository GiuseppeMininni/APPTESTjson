
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora TCO</title>
    <style>
        .hidden { display: none; }
    </style>
</head>
<body>
    <div id="pagina1">
        <h1>Calculadora TCO</h1>
        <form id="tcoForm">
            <label for="modelo1">Modelo 1:</label>
            <select id="modelo1" name="modelo1"></select><br><br>
            <label for="acabado1">Acabado 1:</label>
            <select id="acabado1" name="acabado1"></select><br><br>
            <label for="motor1">Motor 1:</label>
            <select id="motor1" name="motor1"></select><br><br>
            <button type="button" onclick="calcular()">Calcular</button>
        </form>
    </div>
    <div id="pagina2" class="hidden">
        <h1>Resultados</h1>
        <p id="resultados"></p>
        <button type="button" onclick="volver()">Volver</button>
    </div>
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            fetch('BBDD_Audi_TCO.json')
                .then(response => response.json())
                .then(data => {
                    const modelos = [...new Set(data.map(item => item.Modelo))];
                    const acabados = [...new Set(data.map(item => item.Acabado))];
                    const motores = [...new Set(data.map(item => item.Motor))];

                    const modelo1Select = document.getElementById('modelo1');
                    const acabado1Select = document.getElementById('acabado1');
                    const motor1Select = document.getElementById('motor1');

                    modelos.forEach(modelo => {
                        const option = document.createElement('option');
                        option.value = modelo;
                        option.text = modelo;
                        modelo1Select.add(option);
                    });

                    acabados.forEach(acabado => {
                        const option = document.createElement('option');
                        option.value = acabado;
                        option.text = acabado;
                        acabado1Select.add(option);
                    });

                    motores.forEach(motor => {
                        const option = document.createElement('option');
                        option.value = motor;
                        option.text = motor;
                        motor1Select.add(option);
                    });
                });

            document.getElementById('pagina2').classList.add('hidden');
        });

        function calcular() {
            document.getElementById('pagina1').classList.add('hidden');
            document.getElementById('pagina2').classList.remove('hidden');
            document.getElementById('resultados').innerText = 'Resultados calculados...';
        }

        function volver() {
            document.getElementById('pagina2').classList.add('hidden');
            document.getElementById('pagina1').classList.remove('hidden');
        }
    </script>
</body>
</html>

