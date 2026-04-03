<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <title>Stock Atelier QR</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    :root {
      --bg: #020617;
      --bg-alt: #020617;
      --card: #020617;
      --accent: #38bdf8;
      --accent-soft: rgba(56,189,248,0.12);
      --text: #e5e7eb;
      --muted: #9ca3af;
      --danger: #f97373;
      --success: #22c55e;
      --border: #1f2937;
    }
    * { box-sizing: border-box; }
    body {
      margin: 0;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "SF Pro Text", sans-serif;
      background:
        radial-gradient(circle at top, #1e293b 0, #020617 50%),
        radial-gradient(circle at bottom, #020617 0, #000 55%);
      color: var(--text);
      min-height: 100vh;
    }
    .app {
      max-width: 1180px;
      margin: 0 auto;
      padding: 16px 16px 24px;
    }
    header {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
      gap: 12px;
      margin-bottom: 16px;
    }
    .title-block h1 {
      font-size: 1.4rem;
      margin: 0;
      display: flex;
      align-items: center;
      gap: 8px;
      letter-spacing: 0.02em;
    }
    .badge {
      font-size: 0.7rem;
      padding: 2px 8px;
      border-radius: 999px;
      background: var(--accent-soft);
      color: var(--accent);
      border: 1px solid rgba(56,189,248,0.4);
    }
    .subtitle {
      font-size: 0.8rem;
      color: var(--muted);
      margin-top: 3px;
    }
    .actions {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
    }
    button, input {
      font-family: inherit;
    }
    .btn {
      border-radius: 999px;
      border: 1px solid var(--border);
      padding: 8px 14px;
      font-size: 0.85rem;
      background: rgba(15,23,42,0.92);
      color: var(--text);
      display: inline-flex;
      align-items: center;
      gap: 6px;
      cursor: pointer;
      transition: 0.12s ease;
      white-space: nowrap;
    }
    .btn-primary {
      background: linear-gradient(135deg, #38bdf8, #0ea5e9);
      border-color: #38bdf8;
      color: #0b1120;
      font-weight: 600;
    }
    .btn-primary:hover { filter: brightness(1.05); transform: translateY(-1px); }
    .btn-outline { background: transparent; }
    .btn-outline:hover {
      border-color: #4b5563;
      background: rgba(15,23,42,0.9);
    }
    .btn-danger {
      border-color: rgba(248,113,113,0.7);
      color: var(--danger);
      background: rgba(127,29,29,0.22);
    }

    main {
      display: grid;
      grid-template-columns: minmax(0, 2.1fr) minmax(0, 1.5fr);
      gap: 16px;
    }
    @media (max-width: 900px) {
      main { grid-template-columns: minmax(0, 1fr); }
    }

    .card {
      background: radial-gradient(circle at top left, #020617 0, #020617 55%);
      border-radius: 14px;
      border: 1px solid rgba(15,23,42,1);
      box-shadow:
        0 24px 60px rgba(15,23,42,0.9),
        inset 0 1px 0 rgba(148,163,184,0.02);
      padding: 14px;
      backdrop-filter: blur(24px);
    }
    .card-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 10px;
      margin-bottom: 10px;
    }
    .card-title {
      font-size: 0.9rem;
      font-weight: 600;
      letter-spacing: 0.02em;
    }
    .field { margin-bottom: 10px; }
    .field label {
      display: block;
      font-size: 0.75rem;
      color: var(--muted);
      margin-bottom: 3px;
    }
    .field input {
      width: 100%;
      padding: 7px 9px;
      border-radius: 8px;
      border: 1px solid var(--border);
      background: rgba(15,23,42,0.98);
      color: var(--text);
      font-size: 0.85rem;
    }
    .field input:focus {
      outline: none;
      border-color: var(--accent);
      box-shadow: 0 0 0 1px rgba(56,189,248,0.4);
    }

    .inventory-table {
      width: 100%;
      border-collapse: collapse;
      font-size: 0.8rem;
    }
    .inventory-table th, .inventory-table td {
      padding: 6px 6px;
      border-bottom: 1px solid rgba(31,41,55,1);
    }
    .inventory-table th {
      text-align: left;
      font-size: 0.75rem;
      color: var(--muted);
      font-weight: 500;
    }
    .inventory-table tbody tr:hover {
      background: rgba(15,23,42,0.96);
    }
    .tag {
      font-size: 0.7rem;
      padding: 2px 6px;
      border-radius: 999px;
      background: rgba(15,23,42,1);
      border: 1px solid rgba(31,41,55,1);
      color: var(--muted);
    }
    .qty-badge {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      min-width: 32px;
      padding: 2px 6px;
      border-radius: 999px;
      font-size: 0.75rem;
      font-weight: 600;
      background: rgba(15,23,42,0.9);
      border: 1px solid rgba(31,41,55,1);
    }
    .qty-low { border-color: rgba(248,113,113,0.8); color: var(--danger); }
    .qty-ok  { border-color: rgba(34,197,94,0.6);  color: var(--success); }

    .status-bar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 0.75rem;
      color: var(--muted);
      margin-top: 6px;
    }
    .status-dot {
      width: 8px;
      height: 8px;
      border-radius: 999px;
      background: #22c55e;
      box-shadow: 0 0 0 4px rgba(34,197,94,0.25);
      margin-right: 4px;
      display: inline-block;
    }
    .status-pill {
      border-radius: 999px;
      padding: 2px 8px;
      border: 1px dashed rgba(55,65,81,1);
      background: rgba(15,23,42,1);
    }

    .scan-box {
      border-radius: 10px;
      border: 1px solid rgba(31,41,55,1);
      background: radial-gradient(circle at top, rgba(15,23,42,0.92), #020617);
      padding: 10px;
      font-size: 0.8rem;
    }
    #reader {
      width: 100%;
      max-width: 360px;
      margin: 8px auto 0;
      border-radius: 10px;
      overflow: hidden;
    }
    .chip-row {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
      margin-bottom: 6px;
    }
    .chip {
      font-size: 0.7rem;
      padding: 2px 8px;
      border-radius: 999px;
      border: 1px solid rgba(31,41,55,1);
      background: rgba(15,23,42,1);
      color: var(--muted);
    }
    .muted { color: var(--muted); font-size: 0.75rem; }

    .qty-controls {
      display: flex;
      gap: 6px;
      margin-top: 4px;
    }
    .qty-controls input { max-width: 80px; }
    .small-btn {
      padding: 4px 8px;
      font-size: 0.75rem;
      border-radius: 999px;
      border: 1px solid rgba(31,41,55,1);
      background: rgba(15,23,42,0.92);
      color: var(--muted);
      cursor: pointer;
    }
    .small-btn:hover { border-color: rgba(55,65,81,1); }
    .small-btn.primary {
      border-color: var(--accent);
      color: var(--accent);
    }
  </style>
  <script src="https://unpkg.com/html5-qrcode" defer></script>
</head>
<body>
<div class="app">
  <header>
    <div class="title-block">
      <h1>Stock Atelier QR <span class="badge">MVP local</span></h1>
      <div class="subtitle">
        Scan un QR pour retrouver ou créer une référence, puis ajuste les quantités.
      </div>
    </div>
    <div class="actions">
      <button class="btn btn-outline" id="exportBtn">Exporter JSON</button>
      <button class="btn btn-outline" id="clearBtn">Réinitialiser le stock</button>
    </div>
  </header>

  <main>
    <!-- INVENTAIRE -->
    <section class="card">
      <div class="card-header">
        <div>
          <div class="card-title">Inventaire atelier</div>
          <div class="muted" id="summaryText"></div>
        </div>
        <div>
          <button class="btn btn-primary" id="addItemBtn">+ Nouvelle référence</button>
        </div>
      </div>

      <div class="field">
        <input type="text" id="searchInput" placeholder="Rechercher (nom, code, emplacement)..." />
      </div>

      <div style="max-height: 360px; overflow:auto; border-radius:10px; border:1px solid rgba(31,41,55,1);">
        <table class="inventory-table">
          <thead>
          <tr>
            <th>Référence</th>
            <th>Code</th>
            <th>Qté</th>
            <th>Emplacement</th>
            <th></th>
          </tr>
          </thead>
          <tbody id="inventoryBody"></tbody>
        </table>
      </div>

      <div class="status-bar">
        <div><span class="status-dot"></span><span>Stock stocké dans ce navigateur</span></div>
        <div class="status-pill" id="lastSaveText">Dernière sauvegarde : —</div>
      </div>
    </section>

    <!-- SCAN + FICHE -->
    <section class="card">
      <div class="card-header">
        <div>
          <div class="card-title">Scan QR & fiche article</div>
          <div class="muted">Scanne un QR ou saisis un code manuel pour l’ouvrir.</div>
        </div>
      </div>

      <div class="scan-box">
        <div class="chip-row">
          <span class="chip">Caméra : mobile conseillé</span>
          <span class="chip">QR = identifiant ou code article</span>
        </div>
        <div style="display:flex; gap:8px; align-items:center; margin-bottom:6px;">
          <button class="btn btn-outline" id="startScanBtn">Démarrer le scan</button>
          <button class="btn btn-outline" id="stopScanBtn" disabled>Arrêter</button>
        </div>
        <div class="field">
          <label for="manualCode">Ou code manuel</label>
          <input id="manualCode" placeholder="Saisir ou coller un code..." />
        </div>
        <button class="btn btn-primary" id="openCodeBtn">Ouvrir / créer à partir du code</button>
        <div id="reader"></div>
      </div>

      <div style="margin-top:12px; border-top:1px dashed rgba(31,41,55,1); padding-top:10px;">
        <div class="card-title" style="margin-bottom:4px;">Fiche article</div>
        <div class="muted" id="currentItemInfo">Aucun article sélectionné.</div>

        <div id="itemForm" style="display:none; margin-top:8px;">
          <div class="field">
            <label>Code (QR)</label>
            <input id="itemCode" readonly />
          </div>
          <div class="field">
            <label>Nom</label>
            <input id="itemName" placeholder="Ex : Vis M6x20 zinguée" />
          </div>
          <div class="field">
            <label>Emplacement</label>
            <input id="itemLocation" placeholder="Ex : R1-C2-Bac3" />
          </div>
          <div class="field">
            <label>Quantité</label>
            <div class="qty-controls">
              <input id="itemQty" type="number" min="0" />
              <button class="small-btn" data-delta="-1">-1</button>
              <button class="small-btn" data-delta="+1">+1</button>
              <button class="small-btn primary" data-delta="+10">+10</button>
            </div>
          </div>
          <div style="display:flex; gap:8px; margin-top:8px;">
            <button class="btn btn-primary" id="saveItemBtn">Enregistrer</button>
            <button class="btn btn-danger" id="deleteItemBtn">Supprimer</button>
          </div>
        </div>
      </div>
    </section>
  </main>
</div>

<script>
const STORAGE_KEY = "atelier_stock_qr_v1";

function loadInventory() {
  try {
    const raw = localStorage.getItem(STORAGE_KEY);
    if (!raw) return { items: [], lastSave: null };
    return JSON.parse(raw);
  } catch (e) {
    console.error(e);
    return { items: [], lastSave: null };
  }
}

function saveInventory(data) {
  data.lastSave = new Date().toISOString();
  localStorage.setItem(STORAGE_KEY, JSON.stringify(data));
  updateLastSaveText(data.lastSave);
}

let state = loadInventory();
let currentCode = null;
let qrScanner = null;

function formatDateIsoToShort(iso) {
  if (!iso) return "—";
  const d = new Date(iso);
  if (isNaN(d)) return "—";
  return d.toLocaleString("fr-FR", { dateStyle: "short", timeStyle: "short" });
}
function updateLastSaveText(iso) {
  document.getElementById("lastSaveText").textContent =
    "Dernière sauvegarde : " + formatDateIsoToShort(iso);
}

function updateSummary() {
  const count = state.items.length;
  const totalQty = state.items.reduce((s, it) => s + (Number(it.qty) || 0), 0);
  document.getElementById("summaryText").textContent =
    `${count} réf. | ${totalQty} pièces au total`;
}

function renderInventory(filterText = "") {
  const tbody = document.getElementById("inventoryBody");
  tbody.innerHTML = "";
  const f = filterText.toLowerCase();
  const items = [...state.items].sort((a,b)=>(a.name||"").localeCompare(b.name||""));

  for (const item of items) {
    if (f) {
      const hay = `${item.name||""} ${item.code||""} ${item.location||""}`.toLowerCase();
      if (!hay.includes(f)) continue;
    }
    const tr = document.createElement("tr");

    const tdName = document.createElement("td");
    tdName.textContent = item.name || "(sans nom)";

    const tdCode = document.createElement("td");
    tdCode.innerHTML = `<span class="tag">${item.code}</span>`;

    const tdQty = document.createElement("td");
    const qty = Number(item.qty) || 0;
    const spanQty = document.createElement("span");
    spanQty.className = "qty-badge " + (qty <= 0 ? "qty-low" : "qty-ok");
    spanQty.textContent = qty;
    tdQty.appendChild(spanQty);

    const tdLoc = document.createElement("td");
    tdLoc.textContent = item.location || "-";

    const tdActions = document.createElement("td");
    const btnOpen = document.createElement("button");
    btnOpen.textContent = "Ouvrir";
    btnOpen.className = "small-btn primary";
    btnOpen.onclick = () => openItemByCode(item.code);
    tdActions.appendChild(btnOpen);

    tr.appendChild(tdName);
    tr.appendChild(tdCode);
    tr.appendChild(tdQty);
    tr.appendChild(tdLoc);
    tr.appendChild(tdActions);
    tbody.appendChild(tr);
  }
  updateSummary();
}

function getItemByCode(code) {
  return state.items.find(it => it.code === code);
}

function openItemByCode(code) {
  currentCode = code;
  const item = getItemByCode(code);
  const info = document.getElementById("currentItemInfo");
  const form = document.getElementById("itemForm");
  const codeInput = document.getElementById("itemCode");
  const nameInput = document.getElementById("itemName");
  const locInput = document.getElementById("itemLocation");
  const qtyInput = document.getElementById("itemQty");

  codeInput.value = code;
  form.style.display = "block";

  if (item) {
    info.textContent = "Article existant.";
    nameInput.value = item.name || "";
    locInput.value = item.location || "";
    qtyInput.value = item.qty || 0;
  } else {
    info.textContent = "Nouvel article pour ce code.";
    nameInput.value = "";
    locInput.value = "";
    qtyInput.value = 0;
  }
}

function ensureNewItem(code) { openItemByCode(code); }

// événements
function attachEvents() {
  document.getElementById("searchInput").addEventListener("input", e => {
    renderInventory(e.target.value);
  });

  document.getElementById("addItemBtn").addEventListener("click", () => {
    const code = prompt("Code pour la nouvelle référence (ou vide pour ID auto) ?");
    if (code === null) return;
    const c = code.trim() || ("AUTO-" + Date.now());
    ensureNewItem(c);
  });

  document.getElementById("saveItemBtn").addEventListener("click", () => {
    const code = document.getElementById("itemCode").value.trim();
    if (!code) { alert("Code obligatoire."); return; }
    const name = document.getElementById("itemName").value.trim();
    const loc = document.getElementById("itemLocation").value.trim();
    const qty = Number(document.getElementById("itemQty").value || 0);
    let item = getItemByCode(code);
    if (item) {
      item.name = name;
      item.location = loc;
      item.qty = qty;
    } else {
      item = { code, name, location: loc, qty };
      state.items.push(item);
    }
    saveInventory(state);
    renderInventory(document.getElementById("searchInput").value);
    document.getElementById("currentItemInfo").textContent = "Article enregistré.";
  });

  document.getElementById("deleteItemBtn").addEventListener("click", () => {
    if (!currentCode) return;
    if (!confirm("Supprimer cette référence du stock ?")) return;
    state.items = state.items.filter(it => it.code !== currentCode);
    saveInventory(state);
    currentCode = null;
    document.getElementById("itemForm").style.display = "none";
    document.getElementById("currentItemInfo").textContent = "Aucun article sélectionné.";
    renderInventory(document.getElementById("searchInput").value);
  });

  document.querySelectorAll(".qty-controls .small-btn").forEach(btn => {
    btn.addEventListener("click", () => {
      const delta = Number(btn.dataset.delta || 0);
      const input = document.getElementById("itemQty");
      let val = Number(input.value || 0) + delta;
      if (val < 0) val = 0;
      input.value = val;
    });
  });

  document.getElementById("exportBtn").addEventListener("click", () => {
    const dataStr = "text/json;charset=utf-8," +
      encodeURIComponent(JSON.stringify(state, null, 2));
    const a = document.createElement("a");
    a.href = dataStr;
    a.download = "stock-atelier-qr.json";
    a.click();
  });

  document.getElementById("clearBtn").addEventListener("click", () => {
    if (!confirm("Réinitialiser tout le stock pour ce navigateur ?")) return;
    state = { items: [], lastSave: null };
    saveInventory(state);
    renderInventory();
    document.getElementById("itemForm").style.display = "none";
    document.getElementById("currentItemInfo").textContent = "Aucun article sélectionné.";
  });

  document.getElementById("openCodeBtn").addEventListener("click", () => {
    const code = document.getElementById("manualCode").value.trim();
    if (!code) { alert("Saisis un code d’abord."); return; }
    openItemByCode(code);
  });

  document.getElementById("startScanBtn").addEventListener("click", startScanner);
  document.getElementById("stopScanBtn").addEventListener("click", stopScanner);
}

// SCAN QR (html5-qrcode)
function startScanner() {
  const startBtn = document.getElementById("startScanBtn");
  const stopBtn = document.getElementById("stopScanBtn");
  if (qrScanner) return;
  if (!window.Html5Qrcode) {
    alert("Librairie html5-qrcode non chargée.");
    return;
  }
  const config = { fps: 10, qrbox: 220 };
  qrScanner = new Html5Qrcode("reader");
  qrScanner.start(
    { facingMode: "environment" },
    config,
    decodedText => {
      stopScanner();
      document.getElementById("manualCode").value = decodedText;
      openItemByCode(decodedText);
    },
    _err => {}
  ).then(() => {
    startBtn.disabled = true;
    stopBtn.disabled = false;
  }).catch(err => {
    console.error(err);
    alert("Impossible de démarrer la caméra.");
    qrScanner = null;
  });
}
function stopScanner() {
  const startBtn = document.getElementById("startScanBtn");
  const stopBtn = document.getElementById("stopScanBtn");
  if (!qrScanner) return;
  qrScanner.stop().then(() => {
    qrScanner.clear();
    qrScanner = null;
    startBtn.disabled = false;
    stopBtn.disabled = true;
  }).catch(err => console.error(err));
}

// INIT
document.addEventListener("DOMContentLoaded", () => {
  updateLastSaveText(state.lastSave);
  if (!state.items || !state.items.length) {
    state.items = [
      { code: "REF-0001", name: "Vis M6x20 zinguée", location: "R1-BAC1", qty: 150 },
      { code: "REF-0002", name: "Écrou M6",          location: "R1-BAC2", qty: 230 },
      { code: "REF-0003", name: "Gant nitrile L",    location: "EPI-AR1", qty: 40 }
    ];
    saveInventory(state);
  }
  attachEvents();
  renderInventory();
});
</script>
</body>
</html>
