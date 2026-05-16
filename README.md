<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Asistencia · Cervecería Nacional</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#f0f4ff;--white:#fff;--ink:#1a1a2e;--ink2:#666;
  --border:#e0e4f0;--accent:#2563eb;--accent-light:#eff6ff;
  --green:#16a34a;--green-light:#f0fdf4;
  --red:#dc2626;--red-light:#fef2f2;
  --yellow:#d97706;--yellow-light:#fffbeb;
  --orange:#ea580c;--orange-light:#fff7ed;
  --purple:#7c3aed;--purple-light:#f5f3ff;
  --shadow:0 2px 12px rgba(37,99,235,0.08);
  --shadow-lg:0 8px 40px rgba(37,99,235,0.12);
}
*{margin:0;padding:0;box-sizing:border-box;}
body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--ink);min-height:100vh;}

/* COLABORADOR */
#vistaColaborador{min-height:100vh;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:24px 16px;background:linear-gradient(160deg,#eff6ff 0%,#f0fdf4 100%);}
.register-card{background:var(--white);border-radius:24px;padding:32px 26px;width:100%;max-width:400px;box-shadow:var(--shadow-lg);border:1px solid var(--border);}
.brand{display:flex;flex-direction:column;align-items:center;gap:8px;margin-bottom:22px;}
.brand-icon{width:52px;height:52px;background:var(--accent);border-radius:14px;display:flex;align-items:center;justify-content:center;box-shadow:0 4px 14px rgba(37,99,235,0.3);}
.brand-name{font-size:1.1rem;font-weight:700;}
.brand-sub{font-size:0.78rem;color:var(--ink2);margin-top:-4px;}
.hora-badge{display:flex;flex-direction:column;align-items:center;background:var(--accent-light);border:1px solid #bfdbfe;border-radius:12px;padding:10px 16px;margin-bottom:20px;}
.hora-badge .time{font-family:'DM Mono',monospace;font-size:1.5rem;font-weight:500;color:var(--accent);}
.hora-badge .date{font-size:0.76rem;color:var(--ink2);}
.status-banner{border-radius:10px;padding:10px 14px;margin-bottom:16px;font-size:0.82rem;font-weight:600;text-align:center;display:none;}
.banner-orange{background:var(--orange-light);border:1px solid #fed7aa;color:var(--orange);}
.banner-purple{background:var(--purple-light);border:1px solid #ddd6fe;color:var(--purple);}
.field{margin-bottom:14px;}
.field label{display:block;font-size:0.78rem;font-weight:700;color:var(--ink2);margin-bottom:5px;letter-spacing:0.04em;text-transform:uppercase;}
.field input{width:100%;border:2px solid var(--border);border-radius:12px;padding:12px 15px;font-family:'DM Sans',sans-serif;font-size:1rem;color:var(--ink);transition:all 0.2s;}
.field input:focus{outline:none;border-color:var(--accent);box-shadow:0 0 0 3px rgba(37,99,235,0.1);}
.field input::placeholder{color:#bbb;}
.btn-register{width:100%;padding:14px;border:none;border-radius:12px;background:var(--accent);color:#fff;font-family:'DM Sans',sans-serif;font-size:1rem;font-weight:700;cursor:pointer;transition:all 0.2s;box-shadow:0 4px 14px rgba(37,99,235,0.3);}
.btn-register:hover{background:#1d4ed8;transform:translateY(-1px);}
.horario-note{background:var(--yellow-light);border:1px solid #fde68a;border-radius:10px;padding:10px 14px;font-size:0.8rem;color:var(--yellow);margin-top:14px;font-weight:500;text-align:center;}
.result-box{border-radius:12px;padding:14px;margin-top:14px;text-align:center;display:none;}
.result-box.ok{background:var(--green-light);border:1px solid #bbf7d0;color:var(--green);}
.result-box.warn{background:var(--yellow-light);border:1px solid #fde68a;color:var(--yellow);}
.result-box.err{background:var(--red-light);border:1px solid #fecaca;color:var(--red);}
.result-msg{font-size:0.95rem;font-weight:700;}
.result-sub{font-size:0.8rem;margin-top:3px;opacity:0.85;}
.sv-link{margin-top:16px;text-align:center;font-size:0.75rem;}
.sv-link a{color:#aaa;text-decoration:none;}
.sv-link a:hover{color:var(--accent);}

/* SUPERVISOR */
#vistaSupervisor{display:none;min-height:100vh;background:var(--bg);}
.sv-header{background:var(--white);border-bottom:1px solid var(--border);padding:0 20px;display:flex;align-items:center;justify-content:space-between;height:58px;position:sticky;top:0;z-index:100;}
.sv-logo{display:flex;align-items:center;gap:8px;font-weight:700;font-size:0.95rem;}
.sv-logo-icon{width:28px;height:28px;background:var(--accent);border-radius:7px;display:flex;align-items:center;justify-content:center;}
#svClock{font-family:'DM Mono',monospace;font-size:0.75rem;color:var(--ink2);}
.btn-out{background:none;border:1px solid var(--border);border-radius:8px;padding:5px 12px;font-family:'DM Sans',sans-serif;font-size:0.78rem;font-weight:600;cursor:pointer;color:var(--ink2);}
.btn-out:hover{border-color:var(--red);color:var(--red);}
.sv-main{max-width:1020px;margin:0 auto;padding:20px 16px;}
.sv-tabs{display:flex;gap:4px;margin-bottom:20px;background:var(--white);border:1px solid var(--border);border-radius:12px;padding:4px;}
.sv-tab{flex:1;padding:9px;border:none;border-radius:9px;font-family:'DM Sans',sans-serif;font-size:0.85rem;font-weight:600;cursor:pointer;color:var(--ink2);background:none;transition:all 0.15s;}
.sv-tab.active{background:var(--accent);color:#fff;}
.sv-panel{display:none;}
.sv-panel.active{display:block;}
.cron-card{background:var(--white);border:1px solid var(--border);border-radius:16px;padding:20px;box-shadow:var(--shadow);margin-bottom:16px;}
.cron-title{font-size:0.68rem;font-weight:700;letter-spacing:0.1em;text-transform:uppercase;color:var(--ink2);margin-bottom:14px;}
.cron-display{text-align:center;padding:10px 0 16px;}
.cron-big{font-family:'DM Mono',monospace;font-size:2.8rem;font-weight:700;color:var(--orange);}
.cron-big.stopped{color:var(--green);}
.cron-label{font-size:0.75rem;color:var(--ink2);margin-top:4px;}
.cron-milestones{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px;margin-bottom:16px;}
@media(max-width:480px){.cron-milestones{grid-template-columns:1fr;}}
.milestone{border-radius:10px;padding:12px;text-align:center;border:1px solid var(--border);}
.milestone.done{border-color:#bbf7d0;background:var(--green-light);}
.milestone.active{border-color:#fed7aa;background:var(--orange-light);}
.milestone.pending{background:#f9fafb;}
.milestone-icon{font-size:1.3rem;margin-bottom:4px;}
.milestone-label{font-size:0.72rem;font-weight:700;color:var(--ink2);text-transform:uppercase;letter-spacing:0.05em;}
.milestone.done .milestone-label{color:var(--green);}
.milestone.active .milestone-label{color:var(--orange);}
.milestone-time{font-family:'DM Mono',monospace;font-size:0.85rem;font-weight:600;margin-top:3px;color:var(--ink);}
.cron-btns{display:flex;gap:10px;flex-wrap:wrap;}
.btn-cron{flex:1;min-width:140px;padding:12px;border:none;border-radius:10px;font-family:'DM Sans',sans-serif;font-size:0.88rem;font-weight:700;cursor:pointer;transition:all 0.15s;}
.btn-cron:disabled{opacity:0.4;cursor:not-allowed;}
.btn-orange{background:var(--orange);color:#fff;}
.btn-orange:not(:disabled):hover{background:#c2410c;}
.btn-red{background:var(--red);color:#fff;}
.btn-red:not(:disabled):hover{background:#b91c1c;}
.btn-gray{background:var(--white);color:var(--ink2);border:1px solid var(--border);}
.btn-gray:hover{border-color:var(--red);color:var(--red);}
.control-card{background:var(--white);border:1px solid var(--border);border-radius:16px;padding:20px;box-shadow:var(--shadow);margin-bottom:16px;}
.control-title{font-size:0.68rem;font-weight:700;letter-spacing:0.1em;text-transform:uppercase;color:var(--ink2);margin-bottom:14px;}
.conductores-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:12px;}
.conductor-card{background:var(--white);border:2px solid var(--border);border-radius:14px;padding:16px;box-shadow:var(--shadow);transition:all 0.2s;}
.conductor-card.verificado{border-color:#bbf7d0;background:var(--green-light);}
.conductor-card.pendiente{border-color:#fed7aa;}
.conductor-header{display:flex;align-items:center;gap:10px;margin-bottom:12px;}
.conductor-avatar{width:38px;height:38px;border-radius:50%;background:var(--accent-light);color:var(--accent);display:flex;align-items:center;justify-content:center;font-weight:700;font-size:0.95rem;flex-shrink:0;}
.conductor-card.verificado .conductor-avatar{background:var(--green-light);color:var(--green);}
.conductor-nombre{font-weight:700;font-size:0.9rem;}
.conductor-status{font-size:0.72rem;color:var(--ink2);margin-top:1px;}
.conductor-card.verificado .conductor-status{color:var(--green);}
.verif-fields{display:flex;gap:8px;margin-bottom:10px;}
.verif-fields input{flex:1;border:1px solid var(--border);border-radius:8px;padding:7px 10px;font-family:'DM Sans',sans-serif;font-size:0.82rem;color:var(--ink);}
.verif-fields input:focus{outline:none;border-color:var(--accent);}
.btn-verif{width:100%;padding:9px;border:none;border-radius:9px;font-family:'DM Sans',sans-serif;font-size:0.85rem;font-weight:700;cursor:pointer;transition:all 0.15s;}
.btn-verif.pendiente{background:var(--orange);color:#fff;}
.btn-verif.pendiente:hover{background:#c2410c;}
.btn-verif.verificado{background:var(--green-light);color:var(--green);border:1px solid #bbf7d0;cursor:default;}
.verif-info{font-size:0.78rem;color:var(--green);margin-top:6px;font-family:'DM Mono',monospace;}
.stats-row{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:16px;}
@media(max-width:500px){.stats-row{grid-template-columns:1fr 1fr;}}
.stat{background:var(--white);border:1px solid var(--border);border-radius:12px;padding:14px;box-shadow:var(--shadow);}
.stat-n{font-size:0.63rem;font-weight:700;letter-spacing:0.08em;text-transform:uppercase;color:var(--ink2);}
.stat-v{font-size:1.7rem;font-weight:700;margin-top:2px;}
.c-blue{color:var(--accent);}.c-green{color:var(--green);}.c-yellow{color:var(--yellow);}.c-purple{color:var(--purple);}
.sv-card{background:var(--white);border:1px solid var(--border);border-radius:14px;padding:20px;box-shadow:var(--shadow);}
.sv-card-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:14px;flex-wrap:wrap;gap:8px;}
.sv-card-title{font-size:0.68rem;font-weight:700;letter-spacing:0.1em;text-transform:uppercase;color:var(--ink2);}
.filters{display:flex;gap:8px;margin-bottom:14px;flex-wrap:wrap;}
.filters input,.filters select{flex:1;min-width:110px;border:1px solid var(--border);border-radius:9px;padding:8px 11px;font-family:'DM Sans',sans-serif;font-size:0.83rem;background:var(--white);color:var(--ink);}
.filters input:focus,.filters select:focus{outline:none;border-color:var(--accent);}
.tbl-wrap{overflow-x:auto;}
table{width:100%;border-collapse:collapse;font-size:0.82rem;}
thead th{text-align:left;padding:9px 11px;font-size:0.63rem;font-weight:700;letter-spacing:0.08em;text-transform:uppercase;color:var(--ink2);border-bottom:2px solid var(--border);white-space:nowrap;}
tbody tr{border-bottom:1px solid var(--border);transition:background 0.1s;}
tbody tr:hover{background:var(--bg);}
tbody td{padding:11px 11px;white-space:nowrap;}
.empty{text-align:center;padding:40px;color:var(--ink2);font-size:0.875rem;white-space:normal;}
.pill{display:inline-flex;align-items:center;gap:3px;padding:3px 9px;border-radius:20px;font-size:0.7rem;font-weight:700;}
.pill-green{background:var(--green-light);color:var(--green);border:1px solid #bbf7d0;}
.pill-yellow{background:var(--yellow-light);color:var(--yellow);border:1px solid #fde68a;}
.pill-purple{background:var(--purple-light);color:var(--purple);border:1px solid #ddd6fe;}
.pill-orange{background:var(--orange-light);color:var(--orange);border:1px solid #fed7aa;}
.btn-sm{background:none;border:1px solid var(--border);border-radius:8px;padding:6px 13px;font-family:'DM Sans',sans-serif;font-size:0.78rem;font-weight:600;cursor:pointer;color:var(--ink2);transition:all 0.15s;}
.btn-sm:hover{border-color:var(--accent);color:var(--accent);}
.btn-sm.green{background:var(--green);color:#fff;border-color:var(--green);}
.btn-sm.danger{color:var(--red);border-color:#fca5a5;}
.modal-bg{position:fixed;inset:0;background:rgba(0,0,0,0.5);display:flex;align-items:center;justify-content:center;z-index:300;padding:20px;backdrop-filter:blur(6px);}
.modal-bg.hidden{display:none;}
.modal{background:var(--white);border-radius:20px;padding:30px;width:100%;max-width:340px;box-shadow:var(--shadow-lg);animation:popIn 0.2s ease;text-align:center;}
@keyframes popIn{from{transform:scale(0.9);opacity:0;}to{transform:scale(1);opacity:1;}}
.modal-icon{font-size:2.2rem;margin-bottom:10px;}
.modal h3{font-size:1.05rem;font-weight:700;margin-bottom:5px;}
.modal p{font-size:0.82rem;color:var(--ink2);margin-bottom:16px;}
.modal input{width:100%;border:2px solid var(--border);border-radius:10px;padding:11px 14px;font-family:'DM Mono',monospace;font-size:1rem;text-align:center;letter-spacing:0.2em;margin-bottom:6px;}
.modal input:focus{outline:none;border-color:var(--accent);}
.modal-err{color:var(--red);font-size:0.78rem;margin-bottom:10px;display:none;}
.modal-btns{display:flex;gap:8px;}
.modal-btns button{flex:1;padding:11px;border:none;border-radius:10px;font-family:'DM Sans',sans-serif;font-size:0.88rem;font-weight:600;cursor:pointer;}
.mbtn-primary{background:var(--accent);color:#fff;}
.mbtn-cancel{background:var(--border);color:var(--ink2);}
#toast{position:fixed;bottom:20px;right:20px;padding:12px 18px;border-radius:10px;font-size:0.84rem;font-weight:600;box-shadow:var(--shadow-lg);transform:translateY(60px);opacity:0;transition:all 0.25s;z-index:999;color:#fff;max-width:280px;}
#toast.show{transform:translateY(0);opacity:1;}
#toast.ok{background:var(--green);}
#toast.fail{background:var(--red);}
#toast.warn{background:var(--yellow);}
#toast.info{background:var(--accent);}
</style>
</head>
<body>

<!-- COLABORADOR -->
<div id="vistaColaborador">
  <div class="register-card">
    <div class="brand">
      <div class="brand-icon">
        <svg width="26" height="26" viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2.2">
          <path d="M17 21v-2a4 4 0 00-4-4H5a4 4 0 00-4 4v2"/>
          <circle cx="9" cy="7" r="4"/>
          <path d="M23 21v-2a4 4 0 00-3-3.87M16 3.13a4 4 0 010 7.75"/>
        </svg>
      </div>
      <div>
        <div class="brand-name">Cervecería Nacional</div>
        <div class="brand-sub">Registro de asistencia</div>
      </div>
    </div>
    <div class="hora-badge">
      <div class="time" id="horaActual">00:00:00</div>
      <div class="date" id="fechaActual">—</div>
    </div>
    <div class="status-banner banner-orange" id="bannerMatinal">🚛 Verificación de camiones en curso</div>
    <div class="status-banner banner-purple" id="bannerVerif">✅ Jornada finalizada</div>
    <div class="field">
      <label>Nombre completo</label>
      <input type="text" id="inputNombre" placeholder="Ej: María González" autocomplete="off">
    </div>
    <div class="field">
      <label>Número OP</label>
      <input type="text" id="inputOP" placeholder="Ej: OP-001" autocomplete="off"
        onkeydown="if(event.key==='Enter') registrar()">
    </div>
    <button class="btn-register" onclick="registrar()">✅ Registrar entrada</button>
    <div class="horario-note">🕖 Entrada: <strong>7:00 AM</strong> · Tolerancia: <strong>5 min</strong></div>
    <div class="result-box" id="resultBox">
      <div class="result-msg" id="resultMsg"></div>
      <div class="result-sub" id="resultSub"></div>
    </div>
    <div class="sv-link"><a href="#" onclick="abrirLogin();return false;">Acceso supervisor / coordinador →</a></div>
  </div>
</div>

<!-- SUPERVISOR -->
<div id="vistaSupervisor">
  <div class="sv-header">
    <div class="sv-logo">
      <div class="sv-logo-icon">
        <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2.5">
          <path d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2"/>
          <rect x="9" y="3" width="6" height="4" rx="1"/>
        </svg>
      </div>
      Panel Supervisor
    </div>
    <div id="svClock">—</div>
    <button class="btn-out" onclick="cerrarSesion()">Salir</button>
  </div>
  <div class="sv-main">
    <div class="sv-tabs">
      <button class="sv-tab active" onclick="goSvTab('tiempo',this)">⏱ Tiempo</button>
      <button class="sv-tab" onclick="goSvTab('asistencia',this)">👷 Asistencia</button>
    </div>

    <!-- TAB TIEMPO -->
    <div id="svPanel-tiempo" class="sv-panel active">
      <div class="cron-card">
        <div class="cron-title">⏱ Cronómetro de Jornada</div>
        <div class="cron-display">
          <div class="cron-big" id="cronBig">00:00:00</div>
          <div class="cron-label" id="cronLabel">El cronómetro inicia automáticamente a las 7:00 AM</div>
        </div>
        <div class="cron-milestones">
          <div class="milestone pending" id="ms1"><div class="milestone-icon">🕖</div><div class="milestone-label">Inicio (7:00 AM)</div><div class="milestone-time" id="ms1time">—</div></div>
          <div class="milestone pending" id="ms2"><div class="milestone-icon">🔔</div><div class="milestone-label">Matinal Finalizada</div><div class="milestone-time" id="ms2time">—</div></div>
          <div class="milestone pending" id="ms3"><div class="milestone-icon">🏁</div><div class="milestone-label">Cierre de Jornada</div><div class="milestone-time" id="ms3time">—</div></div>
        </div>
        <div class="cron-btns">
          <button class="btn-cron btn-orange" id="btnMatinal" onclick="finMatinal()" disabled>✅ Matinal Finalizada</button>
          <button class="btn-cron btn-red"    id="btnCierre"  onclick="cerrarJornada()" disabled>🏁 Cerrar Jornada</button>
          <button class="btn-cron btn-gray"   onclick="resetTodo()">🔄 Reiniciar</button>
        </div>
      </div>
      <div class="control-card">
        <div class="control-title">🚛 Verificación de Camiones</div>
        <div class="conductores-grid" id="conductoresGrid"></div>
      </div>
    </div>

    <!-- TAB ASISTENCIA -->
    <div id="svPanel-asistencia" class="sv-panel">
      <div class="stats-row">
        <div class="stat"><div class="stat-n">Total hoy</div><div class="stat-v c-blue"   id="sTotal">0</div></div>
        <div class="stat"><div class="stat-n">A tiempo</div> <div class="stat-v c-green"  id="sTiempo">0</div></div>
        <div class="stat"><div class="stat-n">Tarde</div>    <div class="stat-v c-yellow" id="sTarde">0</div></div>
        <div class="stat"><div class="stat-n">Verificados</div><div class="stat-v c-purple" id="sVerif">0</div></div>
      </div>
      <div class="sv-card">
        <div class="sv-card-header">
          <span class="sv-card-title">Registros de entrada</span>
          <div style="display:flex;gap:8px;flex-wrap:wrap;">
            <button class="btn-sm green"  onclick="exportExcel()">⬇ Exportar Excel</button>
            <button class="btn-sm danger" onclick="clearRecs()">🗑 Limpiar</button>
          </div>
        </div>
        <div class="filters">
          <input type="text" id="fText" placeholder="🔎 Nombre o OP..." oninput="renderTable()">
          <input type="date" id="fDate" oninput="renderTable()">
          <select id="fStatus" onchange="renderTable()">
            <option value="">Todos</option>
            <option value="A tiempo">A tiempo</option>
            <option value="Tarde">Tarde</option>
          </select>
        </div>
        <div class="tbl-wrap">
          <table>
            <thead><tr>
              <th>#</th><th>Nombre</th><th>N° OP</th><th>Entrada</th><th>Estado</th>
              <th>Fin Matinal</th><th>Camión</th><th>Ruta</th><th>Hora Verif.</th><th>Tiempo desde 7AM</th><th>Fecha</th>
            </tr></thead>
            <tbody id="tBody"></tbody>
          </table>
        </div>
      </div>
      <div class="sv-card" style="margin-top:16px;">
        <div class="sv-card-header"><span class="sv-card-title">🚛 Resumen por Conductor</span></div>
        <div class="tbl-wrap">
          <table>
            <thead><tr><th>Conductor</th><th>Camión</th><th>Ruta</th><th>Hora Verificación</th><th>Tiempo desde 7AM</th><th>Estado</th></tr></thead>
            <tbody id="tBodyConductores"></tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- Modal Login -->
<div id="modalLogin" class="modal-bg hidden">
  <div class="modal">
    <div class="modal-icon">🔐</div>
    <h3>Acceso Supervisor</h3>
    <p>Ingresa la clave para continuar</p>
    <input type="password" id="claveInput" placeholder="••••••" maxlength="20"
      onkeydown="if(event.key==='Enter') verificarClave()">
    <div id="claveError" class="modal-err">Clave incorrecta</div>
    <div class="modal-btns">
      <button class="mbtn-cancel" onclick="cerrarModal()">Cancelar</button>
      <button class="mbtn-primary" onclick="verificarClave()">Entrar</button>
    </div>
  </div>
</div>

<div id="toast"></div>

<script>
// ╔══════════════════════════════════════════════════════════════╗
// ║  REEMPLAZA CON LA URL DE TU APPS SCRIPT DE ASISTENCIA       ║
// ╚══════════════════════════════════════════════════════════════╝
const APPS_SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbyUb_8nGDWTbcTxYuQiOTZKlQUIMpCXNV6ZcU5CaYuOXkwRmJK-VZDrV7FI_5ZWSFQf/exec';

// ===== CONFIG =====
const HORA_ENTRADA   = 7;
const TOLERANCIA_MIN = 5;
const CLAVE          = '1234';
const CONDUCTORES    = [
  'Jonathan Perea','Pedro Ulloa','Martín Clark',
  'Humberto Vásquez','William De Gracia','Jaime Hernández',
  'Juan Ruiz','Fredy Campos','Ernesto Escobar'
];

// Reset diario
(function checkDailyReset(){
  const hoy=new Date().toDateString();
  const ult=localStorage.getItem('att_ultimo_dia');
  if(ult&&ult!==hoy){localStorage.removeItem('att_jornada');localStorage.removeItem('att_verifs');}
  localStorage.setItem('att_ultimo_dia',hoy);
})();

let records=JSON.parse(localStorage.getItem('att_recs')||'[]');
let jornada=JSON.parse(localStorage.getItem('att_jornada')||'null');
let verifs =JSON.parse(localStorage.getItem('att_verifs') ||'{}');

function saveRecs()   {localStorage.setItem('att_recs',   JSON.stringify(records));}
function saveJornada(){localStorage.setItem('att_jornada',JSON.stringify(jornada));}
function saveVerifs() {localStorage.setItem('att_verifs', JSON.stringify(verifs));}

setInterval(tickAll,1000); tickAll();
function tickAll(){
  const n=new Date();
  const h=n.toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit',second:'2-digit'});
  const d=n.toLocaleDateString('es-MX',{weekday:'long',day:'numeric',month:'long'});
  document.getElementById('horaActual').textContent=h;
  document.getElementById('fechaActual').textContent=d.charAt(0).toUpperCase()+d.slice(1);
  document.getElementById('svClock').textContent=n.toLocaleDateString('es',{weekday:'short',day:'2-digit',month:'short'})+' · '+h;
  if(!jornada&&n.getHours()===HORA_ENTRADA&&n.getMinutes()===0){
    const ini=new Date(n);ini.setSeconds(0,0);
    jornada={inicioTs:ini.toISOString(),matinalTs:null,cierreTs:null,tiempoTotal:null};
    saveJornada();syncCronUI();
  }
  if(jornada){
    const ini=new Date(jornada.inicioTs),fin=jornada.cierreTs?new Date(jornada.cierreTs):n;
    const diff=Math.floor((fin-ini)/1000);
    const el=document.getElementById('cronBig');
    el.textContent=formatSeg(diff);
    el.className='cron-big'+(jornada.cierreTs?' stopped':'');
  }
}
function formatSeg(s){return[Math.floor(s/3600),Math.floor((s%3600)/60),s%60].map(v=>v.toString().padStart(2,'0')).join(':');}
function getEstado(d){return d.getHours()*60+d.getMinutes()<=HORA_ENTRADA*60+TOLERANCIA_MIN?'A tiempo':'Tarde';}
function getRetraso(d){return Math.max(0,d.getHours()*60+d.getMinutes()-(HORA_ENTRADA*60+TOLERANCIA_MIN));}

function abrirLogin(){
  document.getElementById('claveInput').value='';
  document.getElementById('claveError').style.display='none';
  document.getElementById('modalLogin').classList.remove('hidden');
  setTimeout(()=>document.getElementById('claveInput').focus(),200);
}
function cerrarModal(){document.getElementById('modalLogin').classList.add('hidden');}
function verificarClave(){
  if(document.getElementById('claveInput').value===CLAVE){cerrarModal();abrirSupervisor();}
  else{document.getElementById('claveError').style.display='block';document.getElementById('claveInput').value='';}
}
function abrirSupervisor(){
  document.getElementById('vistaColaborador').style.display='none';
  document.getElementById('vistaSupervisor').style.display='block';
  syncCronUI();renderConductores();renderTable();renderConductoresTable();updateStats();
}
function cerrarSesion(){
  document.getElementById('vistaSupervisor').style.display='none';
  document.getElementById('vistaColaborador').style.display='flex';
}
function goSvTab(id,btn){
  document.querySelectorAll('.sv-panel').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.sv-tab').forEach(b=>b.classList.remove('active'));
  document.getElementById('svPanel-'+id).classList.add('active');btn.classList.add('active');
  if(id==='asistencia'){renderTable();renderConductoresTable();updateStats();}
  if(id==='tiempo'){syncCronUI();renderConductores();}
}

// ── REGISTRAR → guarda localmente Y envía a Google Sheets ────
async function registrar(){
  const nombre=document.getElementById('inputNombre').value.trim();
  const op=document.getElementById('inputOP').value.trim();
  if(!nombre){mostrarRes('err','⚠️ Falta tu nombre','Escribe tu nombre completo');return;}
  if(!op){mostrarRes('err','⚠️ Falta el N° OP','Escribe tu número OP');return;}
  const now=new Date(),hoy=now.toDateString();
  const yaMarcó=records.find(r=>r.op.toLowerCase()===op.toLowerCase()&&new Date(r.ts).toDateString()===hoy);
  if(yaMarcó){mostrarRes('warn','⚠️ Ya registraste hoy','Entrada a las '+yaMarcó.time);return;}
  if(!jornada&&now.getHours()===HORA_ENTRADA){
    const ini=new Date(now);ini.setMinutes(0);ini.setSeconds(0,0);
    jornada={inicioTs:ini.toISOString(),matinalTs:null,cierreTs:null,tiempoTotal:null};
    saveJornada();syncCronUI();
  }
  const estado=getEstado(now),retraso=getRetraso(now);
  const time=now.toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit',second:'2-digit'});
  const date=now.toLocaleDateString('es-MX');
  const rec={id:Date.now(),nombre,op:op.toUpperCase(),estado,retraso,date,time,ts:now.toISOString()};
  records.unshift(rec);saveRecs();
  if(estado==='A tiempo')mostrarRes('ok','✅ ¡Entrada registrada!',`Bienvenido/a ${nombre} · ${time}`);
  else mostrarRes('warn',`⚠️ Tarde ${retraso} min`,`${nombre} · ${time}`);
  document.getElementById('inputNombre').value='';
  document.getElementById('inputOP').value='';
  // Enviar a Google Sheets en segundo plano
  try{
    const p=new URLSearchParams({action:'add',nombre,op:op.toUpperCase(),estado,retraso,time,date});
    await fetch(APPS_SCRIPT_URL+'?'+p.toString());
  }catch(e){console.warn('Sheets no disponible:',e);}
}
function mostrarRes(tipo,msg,sub){
  const b=document.getElementById('resultBox');
  b.className='result-box '+tipo;b.style.display='block';
  document.getElementById('resultMsg').textContent=msg;
  document.getElementById('resultSub').textContent=sub;
  clearTimeout(window._rt);window._rt=setTimeout(()=>b.style.display='none',5000);
}

function finMatinal(){
  if(!jornada){toast('El cronómetro aún no ha iniciado (7:00 AM)','warn');return;}
  if(jornada.matinalTs){toast('Matinal ya fue registrada','warn');return;}
  if(!confirm('¿Confirmas que la matinal ha finalizado?'))return;
  jornada.matinalTs=new Date().toISOString();saveJornada();syncCronUI();
  toast('✅ Matinal finalizada · Cronómetro sigue corriendo','ok');
}
function cerrarJornada(){
  if(!jornada){toast('El cronómetro aún no ha iniciado','warn');return;}
  if(jornada.cierreTs){toast('La jornada ya fue cerrada','warn');return;}
  if(!confirm('¿Confirmas el cierre de jornada? El cronómetro se detendrá.'))return;
  const now=new Date(),ini=new Date(jornada.inicioTs);
  jornada.cierreTs=now.toISOString();jornada.tiempoTotal=formatSeg(Math.floor((now-ini)/1000));
  saveJornada();syncCronUI();
  document.getElementById('bannerMatinal').style.display='none';
  document.getElementById('bannerVerif').style.display='block';
  toast('🏁 Jornada cerrada · Tiempo total: '+jornada.tiempoTotal,'ok');
  renderConductoresTable();renderTable();
}
function syncCronUI(){
  const btnM=document.getElementById('btnMatinal'),btnC=document.getElementById('btnCierre');
  const label=document.getElementById('cronLabel');
  if(!jornada){
    label.textContent='El cronómetro inicia automáticamente a las 7:00 AM';
    btnM.disabled=true;btnC.disabled=true;
    ['ms1','ms2','ms3'].forEach(id=>{document.getElementById(id).className='milestone pending';});
    document.getElementById('ms1time').textContent='—';document.getElementById('ms2time').textContent='—';document.getElementById('ms3time').textContent='—';
    document.getElementById('bannerMatinal').style.display='none';document.getElementById('bannerVerif').style.display='none';return;
  }
  document.getElementById('ms1').className='milestone done';
  document.getElementById('ms1time').textContent=new Date(jornada.inicioTs).toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit',second:'2-digit'});
  if(jornada.matinalTs){document.getElementById('ms2').className='milestone done';document.getElementById('ms2time').textContent=new Date(jornada.matinalTs).toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit',second:'2-digit'});btnM.disabled=true;}
  else{document.getElementById('ms2').className='milestone active';document.getElementById('ms2time').textContent='En curso...';btnM.disabled=false;}
  if(jornada.cierreTs){document.getElementById('ms3').className='milestone done';document.getElementById('ms3time').textContent=new Date(jornada.cierreTs).toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit',second:'2-digit'});btnC.disabled=true;label.textContent='✅ Jornada cerrada · Tiempo total: '+jornada.tiempoTotal;}
  else{document.getElementById('ms3').className='milestone active';document.getElementById('ms3time').textContent='Pendiente';btnC.disabled=false;label.textContent=jornada.matinalTs?'🚛 Verificando camiones — cronómetro corriendo':'⏳ Esperando fin de matinal — cronómetro corriendo';}
  document.getElementById('bannerMatinal').style.display=(!jornada.cierreTs)?'block':'none';
  document.getElementById('bannerVerif').style.display=jornada.cierreTs?'block':'none';
}
function resetTodo(){
  if(!confirm('¿Reiniciar cronómetro y verificaciones? Los registros de asistencia NO se borran.'))return;
  jornada=null;verifs={};saveJornada();saveVerifs();syncCronUI();renderConductores();updateStats();renderConductoresTable();toast('🔄 Reiniciado','info');
}
function renderConductores(){
  const grid=document.getElementById('conductoresGrid');
  const hab=jornada&&!jornada.cierreTs;
  grid.innerHTML=CONDUCTORES.map(nombre=>{
    const v=verifs[nombre],ini=nombre.split(' ').map(p=>p[0]).join('').slice(0,2).toUpperCase();
    if(v)return`<div class="conductor-card verificado"><div class="conductor-header"><div class="conductor-avatar">${ini}</div><div><div class="conductor-nombre">${nombre}</div><div class="conductor-status">✅ Verificado</div></div></div><div class="verif-info">🚛 ${v.camion} &nbsp;·&nbsp; 📍 ${v.ruta}<br>⏰ ${v.horaVerif} &nbsp;·&nbsp; ⏱ ${v.tiempoDesde7}</div></div>`;
    const dis=!hab?'disabled':'';
    return`<div class="conductor-card pendiente"><div class="conductor-header"><div class="conductor-avatar">${ini}</div><div><div class="conductor-nombre">${nombre}</div><div class="conductor-status" style="color:var(--orange);">⏳ Pendiente</div></div></div><div class="verif-fields"><input type="text" placeholder="N° Camión" id="camion-${san(nombre)}" ${dis}><input type="text" placeholder="Ruta" id="ruta-${san(nombre)}" ${dis}></div><button class="btn-verif pendiente" ${dis} onclick="verificarConductor('${nombre}')">✅ Marcar verificado</button>${!hab?'<div style="font-size:0.72rem;color:#aaa;margin-top:6px;text-align:center;">Disponible cuando inicie la jornada</div>':''}</div>`;
  }).join('');
}
function san(n){return n.replace(/\s+/g,'-').replace(/[^a-zA-Z0-9-]/g,'');}
function verificarConductor(nombre){
  if(!jornada){toast('El cronómetro no ha iniciado','fail');return;}
  const camion=document.getElementById('camion-'+san(nombre))?.value.trim();
  const ruta=document.getElementById('ruta-'+san(nombre))?.value.trim();
  if(!camion){toast('Ingresa el número de camión','fail');return;}
  if(!ruta){toast('Ingresa la ruta','fail');return;}
  const now=new Date(),ini=new Date(jornada.inicioTs);
  verifs[nombre]={camion,ruta,horaVerif:now.toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit',second:'2-digit'}),tiempoDesde7:formatSeg(Math.floor((now-ini)/1000)),ts:now.toISOString()};
  saveVerifs();renderConductores();updateStats();renderConductoresTable();toast('✅ '+nombre+' verificado','ok');
}
function renderTable(){
  const ft=document.getElementById('fText').value.toLowerCase(),fd=document.getElementById('fDate').value,fs=document.getElementById('fStatus').value;
  const filtered=records.filter(r=>(!ft||r.nombre.toLowerCase().includes(ft)||r.op.toLowerCase().includes(ft))&&(!fd||r.ts.startsWith(fd))&&(!fs||r.estado===fs));
  const body=document.getElementById('tBody');
  if(!filtered.length){body.innerHTML=`<tr><td colspan="11" class="empty">Sin registros</td></tr>`;return;}
  body.innerHTML=filtered.map((r,i)=>{
    const pill=r.estado==='A tiempo'?`<span class="pill pill-green">✅ A tiempo</span>`:`<span class="pill pill-yellow">⚠️ Tarde ${r.retraso}m</span>`;
    const fm=jornada?.matinalTs?new Date(jornada.matinalTs).toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit'}):'—';
    const esC=CONDUCTORES.find(c=>c.toLowerCase()===r.nombre.toLowerCase()),v=esC?verifs[esC]:null;
    return`<tr><td style="color:var(--ink2);font-family:'DM Mono',monospace;font-size:0.73rem;">${i+1}</td><td><strong>${r.nombre}</strong></td><td style="font-family:'DM Mono',monospace;font-size:0.78rem;color:var(--accent);">${r.op}</td><td style="font-family:'DM Mono',monospace;font-size:0.82rem;font-weight:600;color:var(--green);">${r.time}</td><td>${pill}</td><td style="font-family:'DM Mono',monospace;font-size:0.78rem;">${fm}</td><td>${v?v.camion:'—'}</td><td>${v?v.ruta:'—'}</td><td style="font-family:'DM Mono',monospace;font-size:0.78rem;">${v?v.horaVerif:'—'}</td><td>${v?`<span class="pill pill-purple">⏱ ${v.tiempoDesde7}</span>`:'—'}</td><td style="font-family:'DM Mono',monospace;font-size:0.75rem;color:var(--ink2);">${r.date}</td></tr>`;
  }).join('');
}
function renderConductoresTable(){
  document.getElementById('tBodyConductores').innerHTML=CONDUCTORES.map(nombre=>{
    const v=verifs[nombre];
    return v?`<tr><td><strong>${nombre}</strong></td><td style="font-family:'DM Mono',monospace;">${v.camion}</td><td>${v.ruta}</td><td style="font-family:'DM Mono',monospace;">${v.horaVerif}</td><td><span class="pill pill-purple">⏱ ${v.tiempoDesde7}</span></td><td><span class="pill pill-green">✅ Verificado</span></td></tr>`:`<tr><td><strong>${nombre}</strong></td><td>—</td><td>—</td><td>—</td><td>—</td><td><span class="pill pill-orange">⏳ Pendiente</span></td></tr>`;
  }).join('');
}
function updateStats(){
  const hoy=new Date().toDateString(),hoyR=records.filter(r=>new Date(r.ts).toDateString()===hoy);
  document.getElementById('sTotal').textContent=hoyR.length;
  document.getElementById('sTiempo').textContent=hoyR.filter(r=>r.estado==='A tiempo').length;
  document.getElementById('sTarde').textContent=hoyR.filter(r=>r.estado==='Tarde').length;
  document.getElementById('sVerif').textContent=Object.keys(verifs).length;
}
function clearRecs(){if(!confirm('¿Borrar TODOS los registros?'))return;records=[];saveRecs();renderTable();updateStats();toast('Registros eliminados','fail');}
function exportExcel(){
  if(!records.length){toast('No hay registros','fail');return;}
  const BOM='\uFEFF';let csv=BOM+'REGISTRO DE ASISTENCIA · CERVECERÍA NACIONAL\n';
  if(jornada){csv+=`Inicio:,${new Date(jornada.inicioTs).toLocaleTimeString('es-MX')},Fin matinal:,${jornada.matinalTs?new Date(jornada.matinalTs).toLocaleTimeString('es-MX'):'—'},Cierre:,${jornada.cierreTs?new Date(jornada.cierreTs).toLocaleTimeString('es-MX'):'—'},Total:,${jornada.tiempoTotal||'—'}\n\n`;}
  csv+=['#','Nombre','N° OP','Hora Entrada','Estado','Min Retraso','Fin Matinal','Camión','Ruta','Hora Verificación','Tiempo desde 7AM','Fecha'].join(',')+'\n';
  records.forEach((r,i)=>{const fm=jornada?.matinalTs?new Date(jornada.matinalTs).toLocaleTimeString('es-MX',{hour:'2-digit',minute:'2-digit'}):'';const esC=CONDUCTORES.find(c=>c.toLowerCase()===r.nombre.toLowerCase()),v=esC?verifs[esC]:null;csv+=[i+1,`"${r.nombre}"`,r.op,r.time,r.estado,r.retraso||0,fm,v?v.camion:'',v?v.ruta:'',v?v.horaVerif:'',v?v.tiempoDesde7:'',r.date].join(',')+'\n';});
  const a=document.createElement('a');a.download=`Asistencia_${new Date().toLocaleDateString('es-MX').replace(/\//g,'-')}.csv`;a.href=URL.createObjectURL(new Blob([csv],{type:'text/csv;charset=utf-8;'}));a.click();toast('✅ Excel exportado','ok');
}
function toast(msg,type='ok'){const t=document.getElementById('toast');t.textContent=msg;t.className='show '+type;clearTimeout(t._t);t._t=setTimeout(()=>t.className='',3500);}

syncCronUI();
</script>
</body>
</html>
