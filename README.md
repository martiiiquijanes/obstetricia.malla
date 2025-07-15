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
body { font-family: Arial; margin: 20px; }
.grid { display: flex; flex-wrap: wrap; gap: 20px; }
.semester { flex: 1; min-width: 200px; background: #f5f5f5; padding: 10px; border-radius: 6px; }
.course {
  padding: 8px; margin: 5px 0; background: #ddd; cursor: pointer;
  border-radius: 4px; transition: background 0.3s;
}
.course.approved { background: #8fbc8f; color: white; }
.course.available { border: 2px dashed #f90; }
.popup {
  position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%);
  background: white; border: 2px solid #333; padding: 20px;
  box-shadow: 0 0 10px rgba(0,0,0,0.5); display: none;
}
#closePopup {
  position: absolute; top: 5px; right: 5px; cursor: pointer;
}
document.querySelectorAll('.course').forEach(c => {
  c.addEventListener('click', () => {
    const name = c.dataset.name;
    const credits = c.dataset.credits;
    const area = c.dataset.area;
    const prereq = c.dataset.prereq;
    document.getElementById('pName').textContent = name;
    document.getElementById('pCredits').textContent = credits;
    document.getElementById('pArea').textContent = area;
    document.getElementById('pPrereq').textContent = prereq || 'Ninguno';
    document.getElementById('popup').style.display = 'block';
    c.classList.toggle('approved');
    updateAvailability();
  });
});

document.getElementById('closePopup').addEventListener('click', () => {
  document.getElementById('popup').style.display = 'none';
});

function updateAvailability() {
  document.querySelectorAll('.course').forEach(c => c.classList.remove('available'));
  document.querySelectorAll('.course.approved').forEach(ap => {
    const next = findFollowing(ap);
    next.forEach(nc => nc.classList.add('available'));
  });
}

function findFollowing(el) {
  const name = el.dataset.name;
  // Si el curso es "Anatomía", habilita "Embriología" por ej.
  const map = {
    'Anatomía': ['Embriología'],
    'Química General y Orgánica': ['Bioquímica'],
    // Completa esto con tus prerrequisitos reales
  };
  const nexts = map[name] || [];
  return Array.from(document.querySelectorAll('.course'))
    .filter(c => nexts.includes(c.dataset.name));
}
