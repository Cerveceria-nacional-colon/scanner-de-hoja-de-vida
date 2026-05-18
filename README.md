<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Cervecería Nacional — Escáner de Hojas de Vida</title>
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700;800&family=Open+Sans:wght@300;400;600&display=swap" rel="stylesheet">
<style>
  :root {
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
  .file-item .file-icon{font-size:1rem;}
  .file-item .file-name{flex:1;color:var(--text);overflow:hidden;text-overflow:ellipsis;white-space:nowrap;}
  .file-item .file-size{color:var(--muted);font-size:0.73rem;}
  .file-item .remove-btn{background:none;border:none;color:var(--muted);cursor:pointer;font-size:1rem;padding:2px 6px;border-radius:4px;transition:color 0.2s;}
  .file-item .remove-btn:hover{color:var(--danger);}
  .btn{display:inline-flex;align-items:center;gap:8px;padding:12px 24px;border-radius:8px;font-family:'Montserrat',sans-serif;font-size:0.85rem;font-weight:700;cursor:pointer;border:none;transition:all 0.2s;text-transform:uppercase;letter-spacing:0.06em;}
  .btn-primary{background:linear-gradient(135deg,var(--gold),var(--gold2));color:var(--accent);width:100%;justify-content:center;padding:14px;box-shadow:0 3px 12px rgba(245,166,35,0.3);}
  .btn-primary:hover{transform:translateY(-1px);box-shadow:0 6px 20px rgba(245,166,35,0.45);}
  .btn-primary:disabled{opacity:0.45;cursor:not-allowed;transform:none;box-shadow:none;}
  #results{margin-top:36px;}
  .results-header{display:flex;align-items:baseline;justify-content:space-between;margin-bottom:20px;}
  .results-header h2{font-family:'Montserrat',sans-serif;font-size:1.1rem;font-weight:800;color:var(--accent);text-transform:uppercase;letter-spacing:0.05em;}
  .results-count{font-size:0.78rem;color:var(--muted);font-weight:600;}
  .candidates-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));gap:18px;}
  .candidate-card{background:var(--surface);border:1px solid var(--border);border-radius:12px;padding:22px;transition:transform 0.2s,box-shadow 0.2s;animation:fadeUp 0.4s ease forwards;opacity:0;border-left:4px solid var(--border);}
  .candidate-card.card-eligible{border-left-color:#1a9e5c;}
  .candidate-card.card-review{border-left-color:var(--gold);}
  .candidate-card.card-not{border-left-color:var(--danger);}
  .candidate-card:hover{transform:translateY(-3px);box-shadow:0 8px 28px rgba(0,48,135,0.12);}
  @keyframes fadeUp{from{opacity:0;transform:translateY(14px);}to{opacity:1;transform:translateY(0);}}
  .candidate-top{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:14px;}
  .candidate-name{font-family:'Montserrat',sans-serif;font-size:1rem;font-weight:700;color:var(--accent);}
  .candidate-file{font-size:0.73rem;color:var(--muted);margin-top:2px;}
  .badge{display:inline-flex;align-items:center;gap:5px;padding:4px 11px;border-radius:100px;font-size:0.72rem;font-weight:700;white-space:nowrap;font-family:'Montserrat',sans-serif;text-transform:uppercase;letter-spacing:0.04em;}
  .badge-eligible{background:rgba(26,158,92,0.1);color:#1a9e5c;border:1px solid rgba(26,158,92,0.3);}
  .badge-not-eligible{background:rgba(208,2,27,0.08);color:var(--danger);border:1px solid rgba(208,2,27,0.25);}
  .badge-review{background:rgba(245,166,35,0.12);color:#b87800;border:1px solid rgba(245,166,35,0.4);}
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
  .contact-btn{margin-top:14px;width:100%;background:var(--surface2);border:1.5px solid var(--border);color:var(--muted);border-radius:7px;padding:9px;font-family:'Open Sans',sans-serif;font-size:0.78rem;font-weight:600;cursor:pointer;transition:all 0.2s;display:flex;align-items:center;justify-content:center;gap:6px;}
  .contact-btn:hover{border-color:var(--accent2);color:var(--accent2);background:rgba(0,82,204,0.04);}
  .contact-btn.eligible-contact{border-color:rgba(26,158,92,0.4);color:#1a9e5c;background:rgba(26,158,92,0.05);}
  .contact-btn.eligible-contact:hover{background:rgba(26,158,92,0.1);}
  .spinner{display:inline-block;width:15px;height:15px;border:2px solid rgba(0,48,135,0.2);border-top-color:var(--accent);border-radius:50%;animation:spin 0.7s linear infinite;}
  @keyframes spin{to{transform:rotate(360deg);}}
  .scan-progress{background:var(--surface);border:1px solid var(--border);border-radius:10px;padding:18px 22px;margin-bottom:22px;display:none;box-shadow:var(--card-shadow);}
  .scan-progress.active{display:block;}
  .progress-label{font-size:0.82rem;color:var(--muted);margin-bottom:10px;font-weight:600;}
  .progress-bar{height:5px;background:var(--surface2);border-radius:100px;overflow:hidden;}
  .progress-fill{height:100%;background:linear-gradient(90deg,var(--accent),var(--accent2),var(--gold));border-radius:100px;transition:width 0.4s ease;animation:progressShimmer 1.5s ease infinite;}
  @keyframes progressShimmer{0%,100%{opacity:1;}50%{opacity:0.7;}}
  .empty-state{text-align:center;padding:56px 20px;color:var(--muted);}
  .empty-state .icon{font-size:2.8rem;margin-bottom:14px;opacity:0.35;}
  .empty-state p{font-size:0.88rem;line-height:1.6;}
  .toast{position:fixed;bottom:28px;right:28px;z-index:100;background:var(--accent);border:1px solid rgba(255,255,255,0.1);border-radius:10px;padding:13px 20px;font-size:0.84rem;color:#fff;box-shadow:0 8px 24px rgba(0,48,135,0.35);transform:translateY(70px);opacity:0;transition:all 0.3s;display:flex;align-items:center;gap:10px;}
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
        <input type="text" id="jobTitle" placeholder="Ej: Operario de Producción" />
      </div>
      <div class="form-group">
        <label>Requisitos y descripción del cargo</label>
        <textarea id="jobDesc" rows="8" placeholder="Describe los requisitos del cargo, habilidades técnicas, experiencia mínima, formación académica, responsabilidades, etc.

Ejemplo:
- 2+ años de experiencia en planta de producción
- Manejo de montacargas (deseable)
- Disponibilidad para turnos rotativos
- Bachillerato completo
- Trabajo en equipo"></textarea>
      </div>
    </div>

    <div class="card">
      <div class="card-title"><span>📄</span> Hojas de Vida</div>
      <div class="dropzone" id="dropzone" onclick="document.getElementById('fileInput').click()">
        <div class="dropzone-icon">📂</div>
        <p>Arrastra archivos aquí o <strong>haz clic para seleccionar</strong></p>
        <p style="margin-top:6px;font-size:0.75rem;">Soporta .txt, .pdf (texto), .docx · Máx. 10 archivos</p>
      </div>
      <input type="file" id="fileInput" multiple accept=".txt,.pdf,.docx,.doc" />
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
      <div class="progress-bar"><div class="progress-fill" id="progressFill" style="width:0%"></div></div>
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
// ── URL del Apps Script (ya insertada) ────────────────────────
const APPS_SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbxoolrNmLBBP0HFnW-byzIHsZG8xfhoptMnfp4nGoji8f5G5BOV99KiNPCIKvuAimOQ/exec';

let uploadedFiles = [];

// Drag & drop
const dropzone = document.getElementById('dropzone');
dropzone.addEventListener('dragover', e=>{e.preventDefault();dropzone.classList.add('drag-over');});
dropzone.addEventListener('dragleave', ()=>dropzone.classList.remove('drag-over'));
dropzone.addEventListener('drop', e=>{
  e.preventDefault();dropzone.classList.remove('drag-over');
  handleFiles(Array.from(e.dataTransfer.files));
});
document.getElementById('fileInput').addEventListener('change', e=>{
  handleFiles(Array.from(e.target.files));e.target.value='';
});

function handleFiles(files){
  const allowed=files.filter(f=>/\.(txt|pdf|docx|doc)$/i.test(f.name));
  if(allowed.length<files.length)showToast('⚠️ Solo se permiten .txt, .pdf y .docx');
  allowed.forEach(f=>{
    if(uploadedFiles.find(u=>u.file.name===f.name))return;
    if(uploadedFiles.length>=10){showToast('Máximo 10 hojas de vida');return;}
    uploadedFiles.push({file:f,id:Date.now()+Math.random()});
  });
  renderFileList();
}
function renderFileList(){
  const list=document.getElementById('fileList');
  list.innerHTML=uploadedFiles.map(u=>`
    <div class="file-item">
      <span class="file-icon">📄</span>
      <span class="file-name">${u.file.name}</span>
      <span class="file-size">${(u.file.size/1024).toFixed(1)} KB</span>
      <button class="remove-btn" onclick="removeFile('${u.id}')">✕</button>
    </div>`).join('');
  document.getElementById('scanBtn').disabled=uploadedFiles.length===0;
}
function removeFile(id){
  uploadedFiles=uploadedFiles.filter(u=>String(u.id)!==String(id));
  renderFileList();
}

async function readFile(file){
  return new Promise(resolve=>{
    if(file.type==='application/pdf'){
      const r=new FileReader();
      r.onload=()=>{
        const extracted=r.result.replace(/[^\x20-\x7E\n\r\t áéíóúñÁÉÍÓÚÑüÜ]/g,' ').replace(/\s{3,}/g,'\n').trim();
        resolve(extracted.length>100?extracted:`[Archivo PDF: ${file.name}]`);
      };
      r.readAsBinaryString(file);
    } else {
      const r=new FileReader();
      r.onload=()=>resolve(r.result);
      r.readAsText(file,'UTF-8');
    }
  });
}

async function startScan(){
  const jobTitle=document.getElementById('jobTitle').value.trim();
  const jobDesc =document.getElementById('jobDesc').value.trim();
  if(!jobDesc){showToast('⚠️ Por favor describe la vacante');return;}
  if(!uploadedFiles.length){showToast('⚠️ Sube al menos una hoja de vida');return;}

  document.getElementById('emptyState').style.display='none';
  document.getElementById('resultsHeader').style.display='none';
  document.getElementById('candidatesGrid').innerHTML='';
  document.getElementById('scanProgress').classList.add('active');
  document.getElementById('scanBtn').disabled=true;
  document.getElementById('scanBtn').innerHTML='<span class="spinner"></span> &nbsp;Analizando...';
  document.getElementById('syncNote').textContent='';
  document.getElementById('syncNote').className='';

  const results=[];
  for(let i=0;i<uploadedFiles.length;i++){
    const{file}=uploadedFiles[i];
    document.getElementById('progressFill').style.width=Math.round((i/uploadedFiles.length)*100)+'%';
    document.getElementById('progressLabel').textContent=`Analizando: ${file.name} (${i+1} de ${uploadedFiles.length})...`;
    const cvText=await readFile(file);
    const result=await analyzeCV(file.name,cvText,jobTitle,jobDesc);
    results.push(result);
    renderCard(result,i);
    await guardarEnSheets(result,jobTitle);
  }

  document.getElementById('progressFill').style.width='100%';
  setTimeout(()=>document.getElementById('scanProgress').classList.remove('active'),600);

  const eligible=results.filter(r=>r.status==='eligible').length;
  const review  =results.filter(r=>r.status==='review').length;
  document.getElementById('resultsHeader').style.display='flex';
  document.getElementById('resultsCount').textContent=
    `${eligible} elegible(s) · ${review} en revisión · ${results.length-eligible-review} no elegible(s)`;
  document.getElementById('scanBtn').disabled=false;
  document.getElementById('scanBtn').innerHTML='<span class="btn-text">🔄 Escanear de Nuevo</span>';
  showToast(`✅ Análisis completo: ${results.length} candidato(s) evaluado(s)`);
}

// ── Guardar en Sheets con no-cors (fix CORS GitHub Pages → Apps Script) ──
async function guardarEnSheets(r,puesto){
  const note=document.getElementById('syncNote');
  try{
    const params=new URLSearchParams({
      action:           'addCV',
      nombre:           r.name            ||'',
      email:            r.contact_email   ||'',
      puesto:           puesto             ||'',
      score:            r.score           ||0,
      estado:           r.status          ||'',
      habilidades_match:(r.matched_skills ||[]).join(', '),
      habilidades_falta:(r.missing_skills ||[]).join(', '),
      resumen:          r.summary         ||'',
      contacto_email:   r.contact_email   ||'',
      contacto_tel:     r.contact_phone   ||'',
      archivo:          r.filename        ||''
    });
    // mode:'no-cors' necesario para llamadas desde GitHub Pages a Apps Script
    await fetch(APPS_SCRIPT_URL+'?'+params.toString(),{method:'GET',mode:'no-cors'});
    note.textContent='✅ Guardado en Google Sheets';
    note.className='ok';
  }catch(e){
    note.textContent='⚠️ No se pudo conectar con Sheets';
    note.className='err';
    console.warn('Sheets error:',e);
  }
}

async function analyzeCV(filename,cvText,jobTitle,jobDesc){
  const prompt=`Eres un experto en Recursos Humanos de Cervecería Nacional en Panamá. Analiza la hoja de vida para la vacante indicada y responde SOLO con JSON válido, sin texto adicional ni backticks.

VACANTE: ${jobTitle||'No especificado'}
DESCRIPCIÓN:
${jobDesc}

HOJA DE VIDA (${filename}):
${cvText.substring(0,3000)}

JSON requerido:
{
  "name": "Nombre completo (usa nombre del archivo si no aparece)",
  "status": "eligible",
  "score": 75,
  "matched_skills": ["habilidad1"],
  "missing_skills": ["habilidad2"],
  "summary": "2-3 oraciones sobre el candidato y su idoneidad.",
  "contact_email": null,
  "contact_phone": null
}

Reglas: status="eligible" si score>=70, "review" si 45-69, "not_eligible" si <45.`;

  try{
    const response=await fetch('https://api.anthropic.com/v1/messages',{
      method:'POST',
      headers:{'Content-Type':'application/json'},
      body:JSON.stringify({
        model:'claude-sonnet-4-20250514',
        max_tokens:1000,
        messages:[{role:'user',content:prompt}]
      })
    });
    const data=await response.json();
    const raw=data.content.map(b=>b.text||'').join('').trim();
    const parsed=JSON.parse(raw.replace(/```json|```/g,'').trim());
    parsed.filename=filename;
    return parsed;
  }catch(err){
    const nameGuess=filename.replace(/\.(pdf|docx?|txt)$/i,'').replace(/[-_]/g,' ');
    return{name:nameGuess,filename,status:'review',score:50,matched_skills:[],missing_skills:[],summary:'No se pudo analizar este archivo. Revísalo manualmente.',contact_email:null,contact_phone:null};
  }
}

function renderCard(r,idx){
  const grid=document.getElementById('candidatesGrid');
  const delay=idx*120;
  const badgeClass=r.status==='eligible'?'badge-eligible':r.status==='review'?'badge-review':'badge-not-eligible';
  const badgeLabel=r.status==='eligible'?'✅ Elegible':r.status==='review'?'⚠️ Revisar':'❌ No Elegible';
  const scoreClass=r.score>=70?'score-high':r.score>=45?'score-mid':'score-low';
  const matchedTags=(r.matched_skills||[]).slice(0,6).map(s=>`<span class="skill-tag skill-match">${s}</span>`).join('');
  const missingTags=(r.missing_skills||[]).slice(0,4).map(s=>`<span class="skill-tag skill-miss">${s}</span>`).join('');
  const contactInfo=r.contact_email||r.contact_phone
    ?`📧 ${r.contact_email||''} ${r.contact_phone?'· 📞 '+r.contact_phone:''}`
    :'📋 Ver hoja de vida para contacto';
  const card=document.createElement('div');
  card.className='candidate-card '+(r.status==='eligible'?'card-eligible':r.status==='review'?'card-review':'card-not');
  card.style.animationDelay=delay+'ms';
  card.innerHTML=`
    <div class="candidate-top">
      <div>
        <div class="candidate-name">${r.name||'Candidato'}</div>
        <div class="candidate-file">${r.filename}</div>
      </div>
      <span class="badge ${badgeClass}">${badgeLabel}</span>
    </div>
    <div class="score-section">
      <div class="score-label"><span>Compatibilidad</span><strong>${r.score}%</strong></div>
      <div class="score-bar"><div class="score-fill ${scoreClass}" style="width:0%" data-target="${r.score}"></div></div>
    </div>
    ${matchedTags||missingTags?`<div class="skills-section"><p>Habilidades</p><div class="skills-tags">${matchedTags}${missingTags}</div></div>`:''}
    <p class="summary-text">${r.summary}</p>
    <button class="contact-btn ${r.status==='eligible'?'eligible-contact':''}"
      onclick="copyContact('${r.contact_email||''}','${r.contact_phone||''}','${(r.name||'').replace(/'/g,'')}')">
      ${contactInfo}
    </button>`;
  grid.appendChild(card);
  setTimeout(()=>{const fill=card.querySelector('.score-fill');if(fill)fill.style.width=fill.dataset.target+'%';},delay+200);
}

function copyContact(email,phone,name){
  const info=[name,email,phone].filter(Boolean).join(' · ');
  if(info)navigator.clipboard.writeText(info).then(()=>showToast('📋 Info copiada al portapapeles'));
  else showToast('ℹ️ No hay datos de contacto en la hoja de vida');
}

function showToast(msg){
  const t=document.getElementById('toast');
  t.textContent=msg;t.classList.add('show');
  clearTimeout(t._timer);t._timer=setTimeout(()=>t.classList.remove('show'),3500);
}
</script>
</body>
</html>
