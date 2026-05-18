<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Cervecería Nacional — Escáner de Hojas de Vida</title>

<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700;800&family=Open+Sans:wght@400;600&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/mammoth/1.6.0/mammoth.browser.min.js"></script>

<style>
:root{
  --bg:#f4f6f9;--surface:#fff;--surface2:#eef1f7;--border:#d0d8e8;
  --accent:#003087;--accent2:#0052cc;--gold:#F5A623;--danger:#d0021b;
  --text:#1a2240;--muted:#5a6a8a;
}
*{box-sizing:border-box;margin:0;padding:0}
body{background:var(--bg);font-family:'Open Sans',sans-serif;color:var(--text)}
.container{max-width:1100px;margin:auto;padding:0 24px}
header{background:var(--accent)}
.header-inner{height:72px;display:flex;align-items:center;gap:18px}
.logo-mark{width:44px;height:44px;background:var(--gold);border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:22px}
.brand h1{font-family:Montserrat,sans-serif;color:white;font-size:1.25rem;text-transform:uppercase}
.brand p{color:rgba(255,255,255,.7);font-size:.75rem}
.sub-header{background:var(--accent2);color:white;text-align:center;padding:10px;font-family:Montserrat,sans-serif;font-size:.72rem;letter-spacing:.12em;text-transform:uppercase;margin-bottom:36px}
.layout{display:grid;grid-template-columns:1fr 1fr;gap:24px}
@media(max-width:768px){.layout{grid-template-columns:1fr}}
.card{background:white;border:1px solid var(--border);border-radius:12px;padding:28px;box-shadow:0 2px 16px rgba(0,48,135,.08);border-top:3px solid var(--accent)}
.card-title{font-family:Montserrat,sans-serif;font-size:.9rem;font-weight:800;color:var(--accent);text-transform:uppercase;letter-spacing:.08em;margin-bottom:20px}
label{display:block;font-size:.75rem;font-weight:700;color:var(--muted);margin-bottom:7px;text-transform:uppercase;font-family:Montserrat,sans-serif}
textarea,input[type=text]{width:100%;background:var(--surface2);border:1.5px solid var(--border);border-radius:8px;color:var(--text);font-size:.88rem;padding:12px;outline:none}
textarea{min-height:150px;resize:vertical}
.form-group{margin-bottom:18px}
.dropzone{border:2px dashed var(--border);border-radius:10px;padding:28px 20px;text-align:center;cursor:pointer;background:var(--surface2);margin-bottom:14px}
.dropzone:hover,.drag-over{border-color:var(--accent)}
.dropzone-icon{font-size:2.2rem;margin-bottom:10px}
.dropzone p{color:var(--muted);font-size:.85rem}
.dropzone strong{color:var(--accent)}
#fileInput{display:none}
.file-list{display:flex;flex-direction:column;gap:7px;margin-bottom:14px}
.file-item{background:var(--surface2);border:1px solid var(--border);border-radius:7px;padding:9px 13px;display:flex;gap:10px;font-size:.83rem}
.file-name{flex:1;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.file-size{color:var(--muted);font-size:.73rem}
.remove-btn{background:none;border:none;color:var(--danger);cursor:pointer;font-size:1rem}
.btn{padding:14px;border-radius:8px;border:none;font-family:Montserrat,sans-serif;font-weight:800;text-transform:uppercase;cursor:pointer;width:100%}
.btn-primary{background:linear-gradient(135deg,var(--gold),#e8950f);color:var(--accent)}
.btn-primary:disabled{opacity:.45;cursor:not-allowed}
#results{margin-top:36px}
.section-divider{display:flex;align-items:center;gap:12px;margin:32px 0 20px}
.section-divider span{font-size:.72rem;color:var(--accent);text-transform:uppercase;letter-spacing:.12em;font-family:Montserrat,sans-serif;font-weight:800}
.section-divider::before,.section-divider::after{content:'';flex:1;height:2px;background:var(--border)}
.results-header{display:flex;justify-content:space-between;margin-bottom:20px}
.results-header h2{font-family:Montserrat,sans-serif;color:var(--accent);font-size:1.1rem;text-transform:uppercase}
.results-count{font-size:.8rem;color:var(--muted);font-weight:700}
.candidates-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));gap:18px}
.candidate-card{background:white;border:1px solid var(--border);border-radius:12px;padding:22px;border-left:5px solid var(--border);box-shadow:0 4px 18px rgba(0,48,135,.08)}
.card-eligible{border-left-color:#1a9e5c}
.card-review{border-left-color:var(--gold)}
.card-not{border-left-color:var(--danger)}
.candidate-top{display:flex;justify-content:space-between;gap:10px;margin-bottom:14px}
.candidate-name{font-family:Montserrat,sans-serif;font-weight:800;color:var(--accent);font-size:1rem}
.candidate-file{font-size:.75rem;color:var(--muted);margin-top:4px}
.badge{padding:5px 12px;border-radius:100px;font-size:.72rem;font-weight:800;font-family:Montserrat,sans-serif;white-space:nowrap}
.badge-eligible{background:rgba(26,158,92,.1);color:#1a9e5c;border:1px solid rgba(26,158,92,.3)}
.badge-review{background:rgba(245,166,35,.13);color:#b87800;border:1px solid rgba(245,166,35,.4)}
.badge-not-eligible{background:rgba(208,2,27,.08);color:var(--danger);border:1px solid rgba(208,2,27,.25)}
.score-label{display:flex;justify-content:space-between;color:var(--muted);font-size:.8rem;margin-bottom:6px}
.score-label strong{color:var(--accent);font-size:1rem}
.score-bar{height:7px;background:var(--surface2);border-radius:100px;overflow:hidden;border:1px solid var(--border)}
.score-fill{height:100%;transition:width 1s ease}
.score-high{background:#1a9e5c}
.score-mid{background:var(--gold)}
.score-low{background:var(--danger)}
.skills-section{margin-top:14px}
.skills-section p{font-size:.72rem;color:var(--muted);font-weight:800;text-transform:uppercase;letter-spacing:.1em;margin-bottom:8px}
.skills-tags{display:flex;flex-wrap:wrap;gap:6px}
.skill-tag{font-size:.72rem;padding:4px 9px;border-radius:5px;font-weight:700}
.skill-match{background:rgba(0,48,135,.08);color:var(--accent);border:1px solid rgba(0,48,135,.18)}
.skill-miss{background:rgba(208,2,27,.06);color:var(--danger);border:1px solid rgba(208,2,27,.15)}
.summary-text{font-size:.84rem;color:var(--muted);line-height:1.6;border-top:1px solid var(--border);margin-top:14px;padding-top:14px}
.contact-btn{margin-top:14px;width:100%;background:var(--surface2);border:1.5px solid var(--border);color:var(--muted);border-radius:7px;padding:10px;font-weight:700;cursor:pointer}
.scan-progress{background:white;border:1px solid var(--border);border-radius:10px;padding:18px;margin-bottom:22px;display:none}
.scan-progress.active{display:block}
.progress-label{font-size:.82rem;color:var(--muted);margin-bottom:10px;font-weight:700}
.progress-bar{height:5px;background:var(--surface2);border-radius:100px;overflow:hidden}
.progress-fill{height:100%;background:linear-gradient(90deg,var(--accent),var(--accent2),var(--gold))}
.empty-state{text-align:center;padding:56px 20px;color:var(--muted)}
.empty-state .icon{font-size:2.8rem;margin-bottom:14px}
.toast{position:fixed;bottom:28px;right:28px;background:var(--accent);color:white;border-radius:10px;padding:13px 20px;box-shadow:0 8px 24px rgba(0,48,135,.35);opacity:0;transform:translateY(70px);transition:.3s}
.toast.show{opacity:1;transform:translateY(0)}
.spinner{display:inline-block;width:15px;height:15px;border:2px solid rgba(0,48,135,.2);border-top-color:var(--accent);border-radius:50%;animation:spin .7s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}
#syncNote{text-align:center;font-size:.75rem;margin-top:10px;min-height:18px;font-style:italic}
#syncNote.ok{color:#1a9e5c}
#syncNote.err{color:var(--danger)}
</style>
</head>

<body>
<div class="container">

<header>
  <div class="header-inner">
    <div class="logo-mark">🍺</div>
    <div class="brand">
      <h1>Cervecería Nacional</h1>
      <p>Escáner Inteligente de Hojas de Vida · Recursos Humanos</p>
    </div>
  </div>
</header>

<div class="sub-header">Gestión del Talento · Selección de Personal</div>

<div class="layout">
  <div class="card">
    <div class="card-title">💼 Descripción de la Vacante</div>

    <div class="form-group">
      <label>Nombre del cargo</label>
      <input type="text" id="jobTitle" placeholder="Ej: Soporte Técnico Junior">
    </div>

    <div class="form-group">
      <label>Requisitos y descripción del cargo</label>
      <textarea id="jobDesc" placeholder="Ejemplo:
- Conocimientos básicos en soporte técnico
- Manejo de Python, SQL, Excel y Office
- Conocimientos básicos de Linux
- Atención al cliente
- Trabajo en equipo
- Disponibilidad para aprender"></textarea>
    </div>
  </div>

  <div class="card">
    <div class="card-title">📄 Hojas de Vida</div>

    <div class="dropzone" id="dropzone" onclick="document.getElementById('fileInput').click()">
      <div class="dropzone-icon">📂</div>
      <p>Arrastra archivos aquí o <strong>haz clic para seleccionar</strong></p>
      <p style="margin-top:6px;font-size:0.75rem;">Soporta .txt, .pdf, .docx · Máx. 10 archivos</p>
    </div>

    <input type="file" id="fileInput" multiple accept=".txt,.pdf,.docx">
    <div class="file-list" id="fileList"></div>

    <button class="btn btn-primary" id="scanBtn" onclick="startScan()" disabled>
      🚀 Iniciar Escaneo
    </button>

    <div id="syncNote"></div>
  </div>
</div>

<div id="results">
  <div class="section-divider"><span>Resultados del Análisis</span></div>

  <div class="scan-progress" id="scanProgress">
    <div class="progress-label" id="progressLabel">Analizando hoja de vida...</div>
    <div class="progress-bar">
      <div class="progress-fill" id="progressFill" style="width:0%"></div>
    </div>
  </div>

  <div class="empty-state" id="emptyState">
    <div class="icon">🎯</div>
    <p>Configura la vacante, sube las hojas de vida<br>y haz clic en <strong>Iniciar Escaneo</strong></p>
  </div>

  <div class="results-header" id="resultsHeader" style="display:none">
    <h2>Candidatos Evaluados</h2>
    <div class="results-count" id="resultsCount"></div>
  </div>

  <div class="candidates-grid" id="candidatesGrid"></div>
</div>

<br><br>
</div>

<div class="toast" id="toast"></div>

<script>
pdfjsLib.GlobalWorkerOptions.workerSrc =
'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';

const APPS_SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbxoolrNmLBBP0HFnW-byzIHsZG8xfhoptMnfp4nGoji8f5G5BOV99KiNPCIKvuAimOQ/exec';

let uploadedFiles = [];

const dropzone = document.getElementById('dropzone');

dropzone.addEventListener('dragover', e => {
  e.preventDefault();
  dropzone.classList.add('drag-over');
});

dropzone.addEventListener('dragleave', () => {
  dropzone.classList.remove('drag-over');
});

dropzone.addEventListener('drop', e => {
  e.preventDefault();
  dropzone.classList.remove('drag-over');
  handleFiles(Array.from(e.dataTransfer.files));
});

document.getElementById('fileInput').addEventListener('change', e => {
  handleFiles(Array.from(e.target.files));
  e.target.value = '';
});

function handleFiles(files){
  const allowed = files.filter(f => /\.(txt|pdf|docx)$/i.test(f.name));

  if(allowed.length < files.length){
    showToast('⚠️ Solo se permiten .txt, .pdf y .docx');
  }

  allowed.forEach(file => {
    if(uploadedFiles.find(u => u.file.name === file.name)) return;

    if(uploadedFiles.length >= 10){
      showToast('Máximo 10 hojas de vida');
      return;
    }

    uploadedFiles.push({
      file,
      id: Date.now() + Math.random()
    });
  });

  renderFileList();
}

function renderFileList(){
  const list = document.getElementById('fileList');

  list.innerHTML = uploadedFiles.map(u => `
    <div class="file-item">
      <span>📄</span>
      <span class="file-name">${escapeHTML(u.file.name)}</span>
      <span class="file-size">${(u.file.size / 1024).toFixed(1)} KB</span>
      <button class="remove-btn" onclick="removeFile('${u.id}')">✕</button>
    </div>
  `).join('');

  document.getElementById('scanBtn').disabled = uploadedFiles.length === 0;
}

function removeFile(id){
  uploadedFiles = uploadedFiles.filter(u => String(u.id) !== String(id));
  renderFileList();
}

async function readFile(file){
  const ext = file.name.split('.').pop().toLowerCase();

  try{
    if(ext === 'pdf'){
      const buffer = await file.arrayBuffer();

      const pdf = await pdfjsLib.getDocument({
        data: buffer,
        useSystemFonts: true
      }).promise;

      let fullText = '';

      for(let pageNum = 1; pageNum <= pdf.numPages; pageNum++){
        const page = await pdf.getPage(pageNum);
        const content = await page.getTextContent();

        const strings = content.items
          .map(item => item.str || '')
          .filter(Boolean);

        fullText += strings.join(' ') + '\n';
      }

      return cleanExtractedText(fullText);
    }

    if(ext === 'docx'){
      const buffer = await file.arrayBuffer();
      const result = await mammoth.extractRawText({ arrayBuffer: buffer });
      return cleanExtractedText(result.value);
    }

    if(ext === 'txt'){
      return cleanExtractedText(await file.text());
    }

    return '';
  }catch(error){
    console.warn('Error leyendo archivo:', error);
    return '';
  }
}

function cleanExtractedText(text){
  return String(text || '')
    .replace(/\u0000/g, ' ')
    .replace(/\s+/g, ' ')
    .trim();
}

async function startScan(){
  const jobTitle = document.getElementById('jobTitle').value.trim();
  const jobDesc = document.getElementById('jobDesc').value.trim();

  if(!jobDesc){
    showToast('⚠️ Por favor describe la vacante');
    return;
  }

  if(!uploadedFiles.length){
    showToast('⚠️ Sube al menos una hoja de vida');
    return;
  }

  document.getElementById('emptyState').style.display = 'none';
  document.getElementById('resultsHeader').style.display = 'none';
  document.getElementById('candidatesGrid').innerHTML = '';
  document.getElementById('scanProgress').classList.add('active');
  document.getElementById('scanBtn').disabled = true;
  document.getElementById('scanBtn').innerHTML = '<span class="spinner"></span> Analizando...';
  document.getElementById('syncNote').textContent = '';
  document.getElementById('syncNote').className = '';

  const results = [];

  for(let i = 0; i < uploadedFiles.length; i++){
    const { file } = uploadedFiles[i];

    document.getElementById('progressFill').style.width =
      Math.round((i / uploadedFiles.length) * 100) + '%';

    document.getElementById('progressLabel').textContent =
      `Analizando: ${file.name} (${i + 1} de ${uploadedFiles.length})...`;

    const cvText = await readFile(file);
    const result = await analyzeCV(file.name, cvText, jobTitle, jobDesc);

    results.push(result);
    renderCard(result);

    await guardarEnSheets(result, jobTitle);
  }

  document.getElementById('progressFill').style.width = '100%';

  setTimeout(() => {
    document.getElementById('scanProgress').classList.remove('active');
  }, 600);

  const eligible = results.filter(r => r.status === 'eligible').length;
  const review = results.filter(r => r.status === 'review').length;
  const notEligible = results.length - eligible - review;

  document.getElementById('resultsHeader').style.display = 'flex';
  document.getElementById('resultsCount').textContent =
    `${eligible} elegible(s) · ${review} en revisión · ${notEligible} no elegible(s)`;

  document.getElementById('scanBtn').disabled = false;
  document.getElementById('scanBtn').innerHTML = '🔄 Escanear de Nuevo';

  showToast(`✅ Análisis completo: ${results.length} candidato(s) evaluado(s)`);
}

/* NO SE CAMBIARON LOS CAMPOS QUE SE ENVÍAN A GOOGLE SHEETS */
async function guardarEnSheets(r, puesto){
  const note = document.getElementById('syncNote');

  try{
    const params = new URLSearchParams({
      action: 'addCV',
      nombre: r.name || '',
      email: r.contact_email || '',
      puesto: puesto || '',
      score: r.score || 0,
      estado: r.status || '',
      habilidades_match: (r.matched_skills || []).join(', '),
      habilidades_falta: (r.missing_skills || []).join(', '),
      resumen: r.summary || '',
      contacto_email: r.contact_email || '',
      contacto_tel: r.contact_phone || '',
      archivo: r.filename || ''
    });

    await fetch(APPS_SCRIPT_URL + '?' + params.toString(), {
      method: 'GET',
      mode: 'no-cors'
    });

    note.textContent = '✅ Guardado en Google Sheets';
    note.className = 'ok';

  }catch(e){
    note.textContent = '⚠️ No se pudo conectar con Sheets';
    note.className = 'err';
    console.warn('Sheets error:', e);
  }
}

async function analyzeCV(filename, cvText, jobTitle, jobDesc){
  const rawText = String(cvText || '');
  const cleanCV = normalizeText(rawText);
  const cleanJob = normalizeText(jobTitle + ' ' + jobDesc);

  const name = extractName(rawText, filename);
  const email = extractEmail(rawText);
  const phone = extractPhone(rawText);

  const candidateSkills = detectCandidateSkills(cleanCV);
  const jobRequirements = extractJobRequirements(cleanJob);

  const matched = [];
  const missing = [];

  jobRequirements.forEach(req => {
    const reqClean = normalizeText(req);

    const found =
      candidateSkills.some(skill => {
        const skillClean = normalizeText(skill);
        return skillClean.includes(reqClean) || reqClean.includes(skillClean);
      }) ||
      cleanCV.includes(reqClean) ||
      compactText(cleanCV).includes(compactText(reqClean));

    if(found){
      matched.push(req);
    }else{
      missing.push(req);
    }
  });

  const transferableSkills = detectTransferableSkills(candidateSkills, cleanCV, cleanJob);
  const extraSkills = candidateSkills.filter(skill => !matched.includes(skill));
  const allMatched = [...new Set([...matched, ...transferableSkills, ...extraSkills])];

  let score = 0;

  if(cleanCV.length < 40){
    score = 35;
  }else{
    score += calculateEducationScore(cleanCV, cleanJob);
    score += calculateExperienceScore(cleanCV, cleanJob);
    score += calculateSkillsScore(matched, jobRequirements, candidateSkills);
    score += calculateRecruiterPotential(candidateSkills, cleanCV, cleanJob);

    if(email) score += 3;
    if(phone) score += 2;
  }

  score = Math.max(0, Math.min(100, Math.round(score)));

  let status = 'not_eligible';

  if(score >= 65){
    status = 'eligible';
  }else if(score >= 40){
    status = 'review';
  }

  const summary = buildSummary(name, jobTitle, score, allMatched, missing, cleanCV.length, candidateSkills);

  return {
    name,
    filename,
    status,
    score,
    matched_skills: allMatched.slice(0, 12),
    missing_skills: missing.slice(0, 8),
    summary,
    contact_email: email,
    contact_phone: phone
  };
}

function normalizeText(text){
  return String(text || '')
    .toLowerCase()
    .normalize('NFD')
    .replace(/[\u0300-\u036f]/g, '')
    .replace(/[^\w\s@.+-]/g, ' ')
    .replace(/\s+/g, ' ')
    .trim();
}

function compactText(text){
  return normalizeText(text).replace(/\s+/g, '');
}

function extractEmail(text){
  const match = String(text || '').match(/[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}/i);
  return match ? match[0] : '';
}

function extractPhone(text){
  const match = String(text || '').match(/(\+?507[\s-]?)?(\d{4}[\s-]?\d{4})/);
  return match ? match[0] : '';
}

function extractName(text, filename){
  const lines = String(text || '')
    .split(/\n| {2,}/)
    .map(l => l.trim())
    .filter(l => l.length > 2);

  const ignored = [
    'contacto','celular','email','direccion','experiencia',
    'educacion','certificacion','habilidades','idiomas',
    'sobre mi','perfil','curriculum','hoja de vida'
  ];

  for(const line of lines.slice(0, 12)){
    const clean = normalizeText(line);
    if(ignored.some(word => clean.includes(word))) continue;
    if(line.includes('@')) continue;
    if(/\d{4}/.test(line)) continue;
    if(line.length > 60) continue;
    return line;
  }

  return filename.replace(/\.(pdf|docx?|txt)$/i, '').replace(/[-_]/g, ' ');
}

function detectCandidateSkills(text){
  const compact = compactText(text);
  const skills = [];

  function has(...terms){
    return terms.some(term => {
      const normal = normalizeText(term);
      const compactTerm = compactText(term);
      return text.includes(normal) || compact.includes(compactTerm);
    });
  }

  if(has('python','python pro','programacion basica en python','curso python pro 1')) skills.push('python');
  if(has('sql','base de datos','bases de datos','gestion de bases de datos')) skills.push('sql');
  if(has('excel','microsoft excel')) skills.push('excel');
  if(has('word','microsoft word')) skills.push('word');
  if(has('powerpoint','power point')) skills.push('powerpoint');
  if(has('office','microsoft office','paquete microsoft office')) skills.push('office');
  if(has('linux','ndg linux','linux essentials','ndg linux essentials')) skills.push('linux');
  if(has('aws','amazon web services','gestion en la nube con aws','nube')) skills.push('aws');
  if(has('cisco','networking basics','redes')) skills.push('redes');
  if(has('ciberseguridad','cybersecurity','seguridad informatica')) skills.push('ciberseguridad');
  if(has('inventario','control de inventarios','stock','almacen')) skills.push('inventario');
  if(has('logistica','despacho','carga','planificacion logistica')) skills.push('logistica');
  if(has('operaciones','operativo','operativa')) skills.push('operaciones');
  if(has('reportes','reporte','registros operativos')) skills.push('reportes');
  if(has('atencion al cliente','servicio al cliente')) skills.push('atencion al cliente');
  if(has('comunicacion efectiva','comunicacion')) skills.push('comunicacion efectiva');
  if(has('trabajo en equipo','equipo')) skills.push('trabajo en equipo');
  if(has('ingles','english','avanzado')) skills.push('ingles');
  if(has('administracion','administrador','gestion')) skills.push('administracion');
  if(has('soporte tecnico','help desk','service desk','soporte')) skills.push('soporte tecnico');
  if(has('digitalizacion','digital','sistemas digitales')) skills.push('digitalizacion');

  return [...new Set(skills)];
}

function extractJobRequirements(jobText){
  const possible = [
    'python','sql','excel','word','powerpoint','office',
    'linux','aws','redes','ciberseguridad','inventario',
    'logistica','operaciones','reportes','atencion al cliente',
    'comunicacion efectiva','trabajo en equipo','ingles',
    'bachiller','universidad','licenciatura','soporte tecnico',
    'administracion','experiencia','disponibilidad'
  ];

  const requirements = [];

  possible.forEach(req => {
    if(jobText.includes(normalizeText(req)) || compactText(jobText).includes(compactText(req))){
      requirements.push(req);
    }
  });

  if(jobText.includes('base de datos') && !requirements.includes('sql')) requirements.push('sql');
  if(jobText.includes('cisco') && !requirements.includes('redes')) requirements.push('redes');
  if(jobText.includes('almacen') && !requirements.includes('inventario')) requirements.push('inventario');
  if(jobText.includes('despacho') && !requirements.includes('logistica')) requirements.push('logistica');

  if(requirements.length === 0){
    requirements.push('comunicacion efectiva','trabajo en equipo','experiencia');
  }

  return [...new Set(requirements)];
}

function detectTransferableSkills(candidateSkills, cv, job){
  const transferibles = [];

  const isTechRole =
    job.includes('soporte') ||
    job.includes('tecnico') ||
    job.includes('sistemas') ||
    job.includes('it') ||
    job.includes('ciberseguridad') ||
    job.includes('redes');

  if(isTechRole){
    if(candidateSkills.includes('sql') || candidateSkills.includes('python')) transferibles.push('base técnica');
    if(candidateSkills.includes('linux') || candidateSkills.includes('aws') || candidateSkills.includes('redes')) transferibles.push('infraestructura básica');
    if(candidateSkills.includes('operaciones') || candidateSkills.includes('reportes')) transferibles.push('seguimiento operativo');
    if(candidateSkills.includes('atencion al cliente') || candidateSkills.includes('comunicacion efectiva')) transferibles.push('servicio y comunicación');
  }

  return [...new Set(transferibles)];
}

function calculateEducationScore(cv, job){
  let score = 0;

  if(cv.includes('universidad')) score += 8;
  if(cv.includes('licenciatura')) score += 8;
  if(cv.includes('ciberseguridad')) score += 12;
  if(cv.includes('informatica')) score += 10;
  if(cv.includes('bachiller')) score += 6;
  if(cv.includes('certificacion') || cv.includes('curso')) score += 10;

  return Math.min(score, 28);
}

function calculateExperienceScore(cv, job){
  let score = 0;

  if(cv.includes('experiencia')) score += 8;
  if(cv.includes('practicante')) score += 8;
  if(cv.includes('administrador')) score += 8;
  if(cv.includes('auxiliar')) score += 6;
  if(cv.includes('operaciones')) score += 8;
  if(cv.includes('almacen')) score += 6;
  if(cv.includes('remoto')) score += 5;
  if(cv.includes('base de datos')) score += 8;
  if(cv.includes('inventario')) score += 6;
  if(cv.includes('logistica')) score += 6;

  return Math.min(score, 30);
}

function calculateSkillsScore(matched, requirements, candidateSkills){
  let score = 0;

  if(requirements.length > 0){
    score += (matched.length / requirements.length) * 30;
  }

  score += Math.min(candidateSkills.length * 7, 45);

  const techSkills = ['python','sql','linux','aws','redes','ciberseguridad','excel','office'];
  const techCount = candidateSkills.filter(s => techSkills.includes(s)).length;

  if(techCount >= 5) score += 12;
  else if(techCount >= 3) score += 8;
  else if(techCount >= 2) score += 5;

  return Math.min(score, 55);
}

function calculateRecruiterPotential(candidateSkills, cv, job){
  let score = 0;

  const techBase = ['python','sql','linux','aws','redes','ciberseguridad','excel','office'];
  const techCount = candidateSkills.filter(s => techBase.includes(s)).length;

  if(techCount >= 4) score += 10;
  else if(techCount >= 2) score += 6;

  if(cv.includes('universidad') && (cv.includes('ciberseguridad') || cv.includes('informatica'))) score += 8;
  if(cv.includes('ingles')) score += 5;
  if(cv.includes('practicante') || cv.includes('operaciones') || cv.includes('base de datos')) score += 7;
  if(cv.includes('curso') || cv.includes('certificacion')) score += 5;

  return Math.min(score, 20);
}

function buildSummary(name, jobTitle, score, matched, missing, textLength, candidateSkills){
  const cargo = jobTitle || 'la vacante indicada';

  if(textLength < 40){
    return `${name} fue cargado correctamente, pero el sistema no pudo extraer suficiente texto del archivo. Conviene subirlo en DOCX o PDF con texto seleccionable.`;
  }

  let text = `${name} presenta una compatibilidad de ${score}% para ${cargo}.`;

  if(score >= 65){
    text += ` El perfil muestra potencial sólido para una posición junior o de entrada.`;
  }else if(score >= 40){
    text += ` El perfil puede considerarse para revisión, especialmente si la vacante permite formación inicial.`;
  }else{
    text += ` El perfil requiere mayor validación frente a los requisitos principales del cargo.`;
  }

  if(matched.length){
    text += ` Destaca por ${matched.slice(0,5).join(', ')}.`;
  }

  if(missing.length && score < 65){
    text += ` Se recomienda validar en entrevista aspectos como ${missing.slice(0,3).join(', ')}.`;
  }else if(missing.length){
    text += ` Aunque hay puntos por validar, cuenta con habilidades transferibles relevantes.`;
  }else{
    text += ` Cubre los principales requisitos definidos para el cargo.`;
  }

  return text;
}

function renderCard(r){
  const grid = document.getElementById('candidatesGrid');

  const badgeClass =
    r.status === 'eligible' ? 'badge-eligible' :
    r.status === 'review' ? 'badge-review' :
    'badge-not-eligible';

  const badgeLabel =
    r.status === 'eligible' ? '✅ Elegible' :
    r.status === 'review' ? '⚠️ Revisar' :
    '❌ No Elegible';

  const scoreClass =
    r.score >= 65 ? 'score-high' :
    r.score >= 40 ? 'score-mid' :
    'score-low';

  const matchedTags = (r.matched_skills || []).slice(0, 8)
    .map(s => `<span class="skill-tag skill-match">${escapeHTML(s)}</span>`)
    .join('');

  const missingTags = (r.missing_skills || []).slice(0, 5)
    .map(s => `<span class="skill-tag skill-miss">${escapeHTML(s)}</span>`)
    .join('');

  const contactInfo = r.contact_email || r.contact_phone
    ? `📧 ${r.contact_email || ''} ${r.contact_phone ? '· 📞 ' + r.contact_phone : ''}`
    : '📋 Ver hoja de vida para contacto';

  const card = document.createElement('div');

  card.className = 'candidate-card ' + (
    r.status === 'eligible' ? 'card-eligible' :
    r.status === 'review' ? 'card-review' :
    'card-not'
  );

  card.innerHTML = `
    <div class="candidate-top">
      <div>
        <div class="candidate-name">${escapeHTML(r.name || 'Candidato')}</div>
        <div class="candidate-file">${escapeHTML(r.filename || '')}</div>
      </div>
      <span class="badge ${badgeClass}">${badgeLabel}</span>
    </div>

    <div class="score-label">
      <span>Compatibilidad</span>
      <strong>${r.score}%</strong>
    </div>

    <div class="score-bar">
      <div class="score-fill ${scoreClass}" style="width:${r.score}%"></div>
    </div>

    ${matchedTags || missingTags ? `
      <div class="skills-section">
        <p>Habilidades</p>
        <div class="skills-tags">${matchedTags}${missingTags}</div>
      </div>
    ` : ''}

    <p class="summary-text">${escapeHTML(r.summary || '')}</p>

    <button class="contact-btn" onclick="copyContact('${escapeJS(r.contact_email || '')}','${escapeJS(r.contact_phone || '')}','${escapeJS(r.name || '')}')">
      ${escapeHTML(contactInfo)}
    </button>
  `;

  grid.appendChild(card);
}

function copyContact(email, phone, name){
  const info = [name, email, phone].filter(Boolean).join(' · ');

  if(info){
    navigator.clipboard.writeText(info).then(() => showToast('📋 Info copiada'));
  }else{
    showToast('ℹ️ No hay datos de contacto');
  }
}

function showToast(msg){
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');

  clearTimeout(t._timer);
  t._timer = setTimeout(() => t.classList.remove('show'), 3500);
}

function escapeHTML(value){
  return String(value || '')
    .replace(/&/g,'&amp;')
    .replace(/</g,'&lt;')
    .replace(/>/g,'&gt;')
    .replace(/"/g,'&quot;')
    .replace(/'/g,'&#039;');
}

function escapeJS(value){
  return String(value || '')
    .replace(/\\/g,'\\\\')
    .replace(/'/g,"\\'")
    .replace(/"/g,'\\"')
    .replace(/\n/g,' ');
}
</script>

</body>
</html>
