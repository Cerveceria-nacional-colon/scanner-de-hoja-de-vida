<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Cervecería Nacional — Escáner de Hojas de Vida</title>

<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700;800&family=Open+Sans:wght@300;400;600&display=swap" rel="stylesheet">

<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/mammoth/1.6.0/mammoth.browser.min.js"></script>

<style>
:root{
  --bg:#f4f6f9;--surface:#fff;--surface2:#eef1f7;--border:#d0d8e8;
  --accent:#003087;--accent2:#0052cc;--gold:#F5A623;--gold2:#e8950f;
  --danger:#d0021b;--text:#1a2240;--muted:#5a6a8a;
  --card-shadow:0 2px 16px rgba(0,48,135,0.08);
}
*{box-sizing:border-box;margin:0;padding:0;}
body{background:var(--bg);color:var(--text);font-family:'Open Sans',sans-serif;min-height:100vh;overflow-x:hidden;}
body::before{content:'';position:fixed;inset:0;background-image:linear-gradient(rgba(0,48,135,0.025)1px,transparent 1px),linear-gradient(90deg,rgba(0,48,135,0.025)1px,transparent 1px);background-size:48px 48px;pointer-events:none;z-index:0;}
.container{position:relative;z-index:1;max-width:1100px;margin:0 auto;padding:0 24px;}
header{background:var(--accent);margin-bottom:0;position:relative;overflow:hidden;}
header::after{content:'';position:absolute;bottom:0;left:0;right:0;height:4px;background:linear-gradient(90deg,var(--gold),#ffd166,var(--gold));}
.header-inner{max-width:1100px;margin:0 auto;padding:0 24px;display:flex;align-items:center;gap:18px;height:72px;}
.logo-mark{width:44px;height:44px;background:var(--gold);border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:22px;flex-shrink:0;box-shadow:0 2px 8px rgba(0,0,0,0.2);}
.brand h1{font-family:'Montserrat',sans-serif;font-size:1.25rem;font-weight:800;letter-spacing:0.01em;color:#fff;text-transform:uppercase;}
.brand p{font-size:0.72rem;color:rgba(255,255,255,0.65);margin-top:2px;letter-spacing:0.03em;}
.sub-header{background:var(--accent2);padding:10px 24px;text-align:center;font-family:'Montserrat',sans-serif;font-size:0.72rem;font-weight:600;color:rgba(255,255,255,0.8);letter-spacing:0.12em;text-transform:uppercase;margin-bottom:36px;}
.layout{display:grid;grid-template-columns:1fr 1fr;gap:24px;align-items:start;}
@media(max-width:768px){.layout{grid-template-columns:1fr;}}
.card{background:var(--surface);border:1px solid var(--border);border-radius:12px;padding:28px;box-shadow:var(--card-shadow);border-top:3px solid var(--accent);}
.card-title{font-family:'Montserrat',sans-serif;font-size:0.9rem;font-weight:700;color:var(--accent);text-transform:uppercase;letter-spacing:0.08em;margin-bottom:20px;display:flex;align-items:center;gap:10px;}
label{display:block;font-size:0.75rem;font-weight:600;color:var(--muted);margin-bottom:7px;text-transform:uppercase;letter-spacing:0.08em;font-family:'Montserrat',sans-serif;}
textarea,input[type="text"]{width:100%;background:var(--surface2);border:1.5px solid var(--border);border-radius:8px;color:var(--text);font-family:'Open Sans',sans-serif;font-size:0.88rem;padding:11px 14px;resize:vertical;transition:border-color 0.2s;outline:none;}
textarea:focus,input:focus{border-color:var(--accent);box-shadow:0 0 0 3px rgba(0,48,135,0.08);}
textarea{min-height:120px;}
.form-group{margin-bottom:18px;}
.dropzone{border:2px dashed var(--border);border-radius:10px;padding:28px 20px;text-align:center;cursor:pointer;transition:all 0.25s;background:var(--surface2);margin-bottom:14px;}
.dropzone:hover,.dropzone.drag-over{border-color:var(--accent);background:rgba(0,48,135,0.04);}
.dropzone-icon{font-size:2.2rem;margin-bottom:10px;}
.dropzone p{color:var(--muted);font-size:0.83rem;line-height:1.5;}
.dropzone strong{color:var(--accent);}
#fileInput{display:none;}
.file-list{display:flex;flex-direction:column;gap:7px;margin-bottom:14px;}
.file-item{background:var(--surface2);border:1px solid var(--border);border-radius:7px;padding:9px 13px;display:flex;align-items:center;gap:10px;font-size:0.83rem;}
.file-name{flex:1;color:var(--text);overflow:hidden;text-overflow:ellipsis;white-space:nowrap;}
.file-size{color:var(--muted);font-size:0.73rem;}
.remove-btn{background:none;border:none;color:var(--muted);cursor:pointer;font-size:1rem;padding:2px 6px;border-radius:4px;}
.remove-btn:hover{color:var(--danger);}
.btn{display:inline-flex;align-items:center;gap:8px;padding:12px 24px;border-radius:8px;font-family:'Montserrat',sans-serif;font-size:0.85rem;font-weight:700;cursor:pointer;border:none;transition:all 0.2s;text-transform:uppercase;letter-spacing:0.06em;}
.btn-primary{background:linear-gradient(135deg,var(--gold),var(--gold2));color:var(--accent);width:100%;justify-content:center;padding:14px;box-shadow:0 3px 12px rgba(245,166,35,0.3);}
.btn-primary:disabled{opacity:0.45;cursor:not-allowed;}
#results{margin-top:36px;}
.results-header{display:flex;align-items:baseline;justify-content:space-between;margin-bottom:20px;}
.results-header h2{font-family:'Montserrat',sans-serif;font-size:1.1rem;font-weight:800;color:var(--accent);text-transform:uppercase;letter-spacing:0.05em;}
.results-count{font-size:0.78rem;color:var(--muted);font-weight:600;}
.candidates-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));gap:18px;}
.candidate-card{background:var(--surface);border:1px solid var(--border);border-radius:12px;padding:22px;transition:transform 0.2s,box-shadow 0.2s;animation:fadeUp 0.4s ease forwards;opacity:0;border-left:4px solid var(--border);}
.card-eligible{border-left-color:#1a9e5c;}
.card-review{border-left-color:var(--gold);}
.card-not{border-left-color:var(--danger);}
@keyframes fadeUp{from{opacity:0;transform:translateY(14px);}to{opacity:1;transform:translateY(0);}}
.candidate-top{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:14px;}
.candidate-name{font-family:'Montserrat',sans-serif;font-size:1rem;font-weight:700;color:var(--accent);}
.candidate-file{font-size:0.73rem;color:var(--muted);margin-top:2px;}
.badge{display:inline-flex;align-items:center;gap:5px;padding:4px 11px;border-radius:100px;font-size:0.72rem;font-weight:700;white-space:nowrap;font-family:'Montserrat',sans-serif;text-transform:uppercase;letter-spacing:0.04em;}
.badge-eligible{background:rgba(26,158,92,0.1);color:#1a9e5c;border:1px solid rgba(26,158,92,0.3);}
.badge-review{background:rgba(245,166,35,0.12);color:#b87800;border:1px solid rgba(245,166,35,0.4);}
.badge-not-eligible{background:rgba(208,2,27,0.08);color:var(--danger);border:1px solid rgba(208,2,27,0.25);}
.score-section{margin:12px 0;}
.score-label{display:flex;justify-content:space-between;font-size:0.77rem;color:var(--muted);margin-bottom:6px;}
.score-label strong{color:var(--accent);font-size:0.9rem;font-family:'Montserrat',sans-serif;font-weight:700;}
.score-bar{height:6px;background:var(--surface2);border-radius:100px;overflow:hidden;border:1px solid var(--border);}
.score-fill{height:100%;border-radius:100px;transition:width 1s ease;}
.score-high{background:linear-gradient(90deg,#1a9e5c,#2dd17a);}
.score-mid{background:linear-gradient(90deg,var(--gold),#ffd700);}
.score-low{background:linear-gradient(90deg,var(--danger),#ff6b6b);}
.skills-section{margin-top:12px;}
.skills-section p{font-size:0.7rem;color:var(--muted);margin-bottom:7px;text-transform:uppercase;letter-spacing:0.1em;font-family:'Montserrat',sans-serif;font-weight:600;}
.skills-tags{display:flex;flex-wrap:wrap;gap:5px;}
.skill-tag{font-size:0.7rem;padding:3px 9px;border-radius:5px;font-weight:600;}
.skill-match{background:rgba(0,48,135,0.08);color:var(--accent);border:1px solid rgba(0,48,135,0.18);}
.skill-miss{background:rgba(208,2,27,0.06);color:var(--danger);border:1px solid rgba(208,2,27,0.15);text-decoration:line-through;opacity:0.65;}
.summary-text{font-size:0.81rem;color:var(--muted);line-height:1.6;border-top:1px solid var(--border);margin-top:12px;padding-top:12px;}
.contact-btn{margin-top:14px;width:100%;background:var(--surface2);border:1.5px solid var(--border);color:var(--muted);border-radius:7px;padding:9px;font-family:'Open Sans',sans-serif;font-size:0.78rem;font-weight:600;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:6px;}
.contact-btn.eligible-contact{border-color:rgba(26,158,92,0.4);color:#1a9e5c;background:rgba(26,158,92,0.05);}
.spinner{display:inline-block;width:15px;height:15px;border:2px solid rgba(0,48,135,0.2);border-top-color:var(--accent);border-radius:50%;animation:spin 0.7s linear infinite;}
@keyframes spin{to{transform:rotate(360deg);}}
.scan-progress{background:var(--surface);border:1px solid var(--border);border-radius:10px;padding:18px 22px;margin-bottom:22px;display:none;box-shadow:var(--card-shadow);}
.scan-progress.active{display:block;}
.progress-label{font-size:0.82rem;color:var(--muted);margin-bottom:10px;font-weight:600;}
.progress-bar{height:5px;background:var(--surface2);border-radius:100px;overflow:hidden;}
.progress-fill{height:100%;background:linear-gradient(90deg,var(--accent),var(--accent2),var(--gold));border-radius:100px;transition:width 0.4s ease;}
.empty-state{text-align:center;padding:56px 20px;color:var(--muted);}
.empty-state .icon{font-size:2.8rem;margin-bottom:14px;opacity:0.35;}
.toast{position:fixed;bottom:28px;right:28px;z-index:100;background:var(--accent);border-radius:10px;padding:13px 20px;font-size:0.84rem;color:#fff;box-shadow:0 8px 24px rgba(0,48,135,0.35);transform:translateY(70px);opacity:0;transition:all 0.3s;}
.toast.show{transform:translateY(0);opacity:1;}
.section-divider{display:flex;align-items:center;gap:12px;margin:32px 0 20px;}
.section-divider span{font-size:0.72rem;color:var(--accent);white-space:nowrap;text-transform:uppercase;letter-spacing:0.12em;font-family:'Montserrat',sans-serif;font-weight:700;}
.section-divider::before,.section-divider::after{content:'';flex:1;height:2px;background:linear-gradient(90deg,var(--border),transparent);}
.section-divider::before{background:linear-gradient(90deg,transparent,var(--border));}
#syncNote{text-align:center;font-size:0.75rem;margin-top:10px;min-height:18px;font-style:italic;}
#syncNote.ok{color:#1a9e5c;}
#syncNote.err{color:var(--danger);}
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
    <div class="card-title"><span>💼</span> Descripción de la Vacante</div>

    <div class="form-group">
      <label>Nombre del cargo</label>
      <input type="text" id="jobTitle" placeholder="Ej: Soporte Técnico">
    </div>

    <div class="form-group">
      <label>Requisitos y descripción del cargo</label>
      <textarea id="jobDesc" rows="8" placeholder="Describe los requisitos del cargo, habilidades técnicas, experiencia mínima, formación académica, responsabilidades, etc."></textarea>
    </div>
  </div>

  <div class="card">
    <div class="card-title"><span>📄</span> Hojas de Vida</div>

    <div class="dropzone" id="dropzone" onclick="document.getElementById('fileInput').click()">
      <div class="dropzone-icon">📂</div>
      <p>Arrastra archivos aquí o <strong>haz clic para seleccionar</strong></p>
      <p style="margin-top:6px;font-size:0.75rem;">Soporta .txt, .pdf, .docx · Máx. 10 archivos</p>
    </div>

    <input type="file" id="fileInput" multiple accept=".txt,.pdf,.docx,.doc">
    <div class="file-list" id="fileList"></div>

    <button class="btn btn-primary" id="scanBtn" onclick="startScan()" disabled>
      <span class="btn-text">🚀 Iniciar Escaneo</span>
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
  const allowed = files.filter(f => /\.(txt|pdf|docx|doc)$/i.test(f.name));

  if(allowed.length < files.length){
    showToast('⚠️ Solo se permiten .txt, .pdf y .docx');
  }

  allowed.forEach(f => {
    if(uploadedFiles.find(u => u.file.name === f.name)) return;

    if(uploadedFiles.length >= 10){
      showToast('Máximo 10 hojas de vida');
      return;
    }

    uploadedFiles.push({
      file: f,
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
      const pdf = await pdfjsLib.getDocument({data: buffer}).promise;

      let text = '';

      for(let i = 1; i <= pdf.numPages; i++){
        const page = await pdf.getPage(i);
        const content = await page.getTextContent();
        text += content.items.map(item => item.str).join(' ') + '\n';
      }

      return text.trim();
    }

    if(ext === 'docx'){
      const buffer = await file.arrayBuffer();
      const result = await mammoth.extractRawText({arrayBuffer: buffer});
      return result.value.trim();
    }

    if(ext === 'doc'){
      return '';
    }

    return await file.text();

  }catch(error){
    console.warn('Error leyendo archivo:', error);
    return '';
  }
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
  document.getElementById('scanBtn').innerHTML = '<span class="spinner"></span> &nbsp;Analizando...';
  document.getElementById('syncNote').textContent = '';
  document.getElementById('syncNote').className = '';

  const results = [];

  for(let i = 0; i < uploadedFiles.length; i++){
    const {file} = uploadedFiles[i];

    document.getElementById('progressFill').style.width =
      Math.round((i / uploadedFiles.length) * 100) + '%';

    document.getElementById('progressLabel').textContent =
      `Analizando: ${file.name} (${i + 1} de ${uploadedFiles.length})...`;

    const cvText = await readFile(file);
    console.log('TEXTO EXTRAÍDO:', cvText);

    const result = await analyzeCV(file.name, cvText, jobTitle, jobDesc);

    results.push(result);
    renderCard(result, i);

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
  document.getElementById('scanBtn').innerHTML =
    '<span class="btn-text">🔄 Escanear de Nuevo</span>';

  showToast(`✅ Análisis completo: ${results.length} candidato(s) evaluado(s)`);
}

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
  const cleanCV = normalizeText(cvText);
  const cleanJob = normalizeText(jobTitle + ' ' + jobDesc);

  const name = extractName(cvText, filename);
  const email = extractEmail(cvText);
  const phone = extractPhone(cvText);

  const candidateSkills = detectCandidateSkills(cleanCV);
  const jobRequirements = extractJobRequirements(cleanJob);

  if(!cleanCV || cleanCV.length < 40){
    return {
      name,
      filename,
      status: 'review',
      score: 40,
      matched_skills: [],
      missing_skills: jobRequirements.slice(0, 8),
      summary: 'No se pudo extraer suficiente texto de esta hoja de vida. Puede ser un PDF escaneado como imagen.',
      contact_email: email,
      contact_phone: phone
    };
  }

  const matched = [];
  const missing = [];

  jobRequirements.forEach(req => {
    const reqClean = normalizeText(req);

    const found =
      candidateSkills.some(skill => {
        const skillClean = normalizeText(skill);
        return skillClean.includes(reqClean) || reqClean.includes(skillClean);
      }) || cleanCV.includes(reqClean);

    if(found){
      matched.push(req);
    }else{
      missing.push(req);
    }
  });

  const extraSkills = candidateSkills.filter(skill => !matched.includes(skill));
  const allMatched = [...matched, ...extraSkills];

  let score = 0;

  score += calculateEducationScore(cleanCV);
  score += calculateExperienceScore(cleanCV);
  score += calculateSkillsScore(matched, jobRequirements, candidateSkills);

  if(email) score += 3;
  if(phone) score += 2;

  score = Math.max(0, Math.min(100, Math.round(score)));

  let status = 'not_eligible';

  if(score >= 70){
    status = 'eligible';
  }else if(score >= 45){
    status = 'review';
  }

  const summary = buildSummary(name, jobTitle, score, allMatched, missing);

  return {
    name,
    filename,
    status,
    score,
    matched_skills: allMatched.slice(0, 10),
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
    .split('\n')
    .map(l => l.trim())
    .filter(l => l.length > 2);

  const ignored = [
    'contacto','celular','email','direccion','experiencia',
    'educacion','certificacion','habilidades','idiomas',
    'sobre mi','perfil','curriculum','hoja de vida'
  ];

  for(const line of lines.slice(0, 10)){
    const clean = normalizeText(line);

    if(ignored.some(word => clean.includes(word))) continue;
    if(line.includes('@')) continue;
    if(/\d{4}/.test(line)) continue;
    if(line.length > 55) continue;

    return line;
  }

  return filename.replace(/\.(pdf|docx?|txt)$/i, '').replace(/[-_]/g, ' ');
}

function detectCandidateSkills(text){
  const dictionary = {
    'python': ['python','programacion basica en python','curso python','python pro'],
    'sql': ['sql','base de datos','bases de datos','gestion de bases de datos','database'],
    'excel': ['excel','microsoft excel','paquete microsoft office'],
    'word': ['word','microsoft word'],
    'powerpoint': ['powerpoint','power point'],
    'office': ['office','microsoft office','paquete microsoft office'],
    'linux': ['linux','ndg linux','linux essentials','ndg linux essentials'],
    'aws': ['aws','amazon web services','gestion en la nube con aws','cloud','nube'],
    'redes': ['redes','networking','cisco','cisco networking basics'],
    'ciberseguridad': ['ciberseguridad','cybersecurity','seguridad informatica'],
    'inventario': ['inventario','stock','almacen','control de inventarios'],
    'logistica': ['logistica','despacho','carga','planificacion logistica'],
    'reportes': ['reporte','reportes','informes','registros operativos'],
    'atencion al cliente': ['atencion al cliente','servicio al cliente'],
    'comunicacion efectiva': ['comunicacion efectiva','comunicacion'],
    'trabajo en equipo': ['trabajo en equipo','equipo'],
    'ingles': ['ingles','english','avanzado'],
    'espanol': ['espanol','español','nativo'],
    'administracion': ['administracion','administrador','gestion'],
    'soporte tecnico': ['soporte tecnico','help desk','service desk','soporte'],
    'operaciones': ['operaciones','operativo','operativa'],
    'digitalizacion': ['digitalizacion','digital','sistemas digitales']
  };

  const found = [];

  Object.keys(dictionary).forEach(skill => {
    if(dictionary[skill].some(alias => text.includes(normalizeText(alias)))){
      found.push(skill);
    }
  });

  return found;
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
    if(jobText.includes(normalizeText(req))){
      requirements.push(req);
    }
  });

  if(jobText.includes('base de datos') && !requirements.includes('sql')){
    requirements.push('sql');
  }

  if(jobText.includes('cisco') && !requirements.includes('redes')){
    requirements.push('redes');
  }

  if(requirements.length === 0){
    requirements.push('comunicacion efectiva','trabajo en equipo','experiencia');
  }

  return [...new Set(requirements)];
}

function calculateEducationScore(cv){
  let score = 0;

  if(cv.includes('universidad')) score += 8;
  if(cv.includes('licenciatura')) score += 8;
  if(cv.includes('ciberseguridad')) score += 10;
  if(cv.includes('informatica')) score += 8;
  if(cv.includes('bachiller')) score += 6;
  if(cv.includes('certificacion') || cv.includes('curso')) score += 8;

  return Math.min(score, 25);
}

function calculateExperienceScore(cv){
  let score = 0;

  if(cv.includes('experiencia')) score += 8;
  if(cv.includes('practicante')) score += 8;
  if(cv.includes('administrador')) score += 8;
  if(cv.includes('auxiliar')) score += 6;
  if(cv.includes('operaciones')) score += 8;
  if(cv.includes('almacen')) score += 6;
  if(cv.includes('remoto')) score += 5;
  if(cv.includes('base de datos')) score += 8;

  return Math.min(score, 30);
}

function calculateSkillsScore(matched, requirements, candidateSkills){
  let score = 0;

  if(requirements.length > 0){
    score += (matched.length / requirements.length) * 35;
  }

  score += Math.min(candidateSkills.length * 5, 30);

  return Math.min(score, 45);
}

function buildSummary(name, jobTitle, score, matched, missing){
  const cargo = jobTitle || 'la vacante indicada';

  let text = `${name} presenta una compatibilidad de ${score}% para ${cargo}.`;

  if(matched.length){
    text += ` Destaca por conocimientos o experiencia en ${matched.slice(0,5).join(', ')}.`;
  }

  if(missing.length){
    text += ` Se recomienda validar en entrevista aspectos como ${missing.slice(0,3).join(', ')}.`;
  }else{
    text += ` El perfil cubre los principales requisitos definidos para el cargo.`;
  }

  return text;
}

function renderCard(r, idx){
  const grid = document.getElementById('candidatesGrid');
  const delay = idx * 120;

  const badgeClass =
    r.status === 'eligible' ? 'badge-eligible' :
    r.status === 'review' ? 'badge-review' :
    'badge-not-eligible';

  const badgeLabel =
    r.status === 'eligible' ? '✅ Elegible' :
    r.status === 'review' ? '⚠️ Revisar' :
    '❌ No Elegible';

  const scoreClass =
    r.score >= 70 ? 'score-high' :
    r.score >= 45 ? 'score-mid' :
    'score-low';

  const matchedTags = (r.matched_skills || []).slice(0, 6)
    .map(s => `<span class="skill-tag skill-match">${escapeHTML(s)}</span>`)
    .join('');

  const missingTags = (r.missing_skills || []).slice(0, 4)
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

  card.style.animationDelay = delay + 'ms';

  card.innerHTML = `
    <div class="candidate-top">
      <div>
        <div class="candidate-name">${escapeHTML(r.name || 'Candidato')}</div>
        <div class="candidate-file">${escapeHTML(r.filename || '')}</div>
      </div>
      <span class="badge ${badgeClass}">${badgeLabel}</span>
    </div>

    <div class="score-section">
      <div class="score-label">
        <span>Compatibilidad</span>
        <strong>${r.score}%</strong>
      </div>
      <div class="score-bar">
        <div class="score-fill ${scoreClass}" style="width:0%" data-target="${r.score}"></div>
      </div>
    </div>

    ${matchedTags || missingTags ? `
      <div class="skills-section">
        <p>Habilidades</p>
        <div class="skills-tags">${matchedTags}${missingTags}</div>
      </div>
    ` : ''}

    <p class="summary-text">${escapeHTML(r.summary || '')}</p>

    <button class="contact-btn ${r.status === 'eligible' ? 'eligible-contact' : ''}"
      onclick="copyContact('${escapeJS(r.contact_email || '')}','${escapeJS(r.contact_phone || '')}','${escapeJS(r.name || '')}')">
      ${escapeHTML(contactInfo)}
    </button>
  `;

  grid.appendChild(card);

  setTimeout(() => {
    const fill = card.querySelector('.score-fill');
    if(fill) fill.style.width = fill.dataset.target + '%';
  }, delay + 200);
}

function copyContact(email, phone, name){
  const info = [name, email, phone].filter(Boolean).join(' · ');

  if(info){
    navigator.clipboard.writeText(info).then(() => {
      showToast('📋 Info copiada al portapapeles');
    });
  }else{
    showToast('ℹ️ No hay datos de contacto en la hoja de vida');
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
