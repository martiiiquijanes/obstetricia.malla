# obstetricia.malla
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Malla Obstetricia y Puericultura UV</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Obstetricia y Puericultura (10 semestres)</h1>
  <div class="grid">
    <!-- Primer semestre ejemplo -->
    <div class="semester">
      <h2>1° Semestre</h2>
      <div class="course" data-name="Anatomía" data-credits="6" data-area="Básica" data-prereq="">Anatomía</div>
      <div class="course" data-name="Química General y Orgánica" data-credits="3" data-area="Básica" data-prereq="">Química</div>
      <!-- Añade los demás ramos según tu imagen -->
    </div>
    <!-- Continúa los semestres 2° a 10° -->
  </div>

  <div id="popup" class="popup">
    <button id="closePopup">X</button>
    <h3 id="pName"></h3>
    <p><strong>Créditos:</strong> <span id="pCredits"></span></p>
    <p><strong>Área:</strong> <span id="pArea"></span></p>
    <p><strong>Prerrequisitos:</strong> <span id="pPrereq"></span></p>
  </div>

  <script src="script.js"></script>
</body> 
</html>


