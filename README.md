<!doctype html>
<html lang="ru">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>VPN Mini App — шаблон</title>
<script src="https://telegram.org/js/telegram-web-app.js"></script>
<style>
:root{font-family:Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;}
body{margin:0;padding:20px;background:#f6f7fb;color:#111}
.card{background:white;border-radius:12px;padding:16px;box-shadow:0 6px 18px rgba(14,25,47,0.08);max-width:760px;margin:10px auto}
h1{font-size:20px;margin:0 0 12px}
.row{display:flex;gap:10px;align-items:center}
select,input,button{padding:10px;border-radius:8px;border:1px solid #e6e9ef}
button{cursor:pointer}
button.primary{background:#2563eb;color:white;border:0}
button.ghost{background:transparent}
.status{padding:8px;border-radius:8px;margin-top:12px}
.status.off{background:#fff1f0;color:#9b1c1c}
.status.on{background:#f0fdf4;color:#14532d}
pre{background:#0b1220;color:#cde9ff;padding:12px;border-radius:8px;overflow:auto}
.muted{color:#6b7280;font-size:13px}
</style>
</head>
<body>
<div class="card">
<h1>VPN — мини-приложение (шаблон)</h1>
<p class="muted">Это фронтенд-шаблон. Он не устанавливает VPN на устройстве — только запрашивает/показывает конфигурацию и отправляет команды боту/серверу.</p>


<div style="margin-top:12px">
<label>Выберите сервер</label>
<div class="row" style="margin-top:8px">
<select id="serverSelect"></select>
<button id="refreshServers" class="ghost">Обновить</button>
</div>
</div>


<div style="margin-top:14px" class="row">
<button id="connectBtn" class="primary">Подключиться</button>
<button id="disconnectBtn">Отключиться</button>
<div id="status" class="status off">Отключено</div>
</div>


<div style="margin-top:14px">
<h3>Конфигурация</h3>
<pre id="configArea">Нажмите "Подключиться", чтобы получить конфигурацию.</pre>
<div style="margin-top:8px" class="row">
<button id="copyConfig">Копировать конфиг</button>
<button id="sendToBot">Отправить боту</button>
</div>
</div>


<div style="margin-top:14px" class="muted">
<strong>Как это работает (шаблон):</strong>
<ul>
<li>Мини-приложение запрашивает список серверов у твоего бэкенда (API).</li>
<li>При нажатии "Подключиться" фронтенд просит бэкенд сгенерировать конфиг (WireGuard/ OpenVPN/ Shadowsocks и т.д.).</li>
<li>Ты копируешь конфиг и используешь его в клиенте VPN на устройстве, либо бэкенд отдаёт QR/скачиваемый файл.</li>
<li>Мини-приложение может отправлять данные боту через Telegram.WebApp.sendData(), чтобы бот сделал что-то от своего имени (например, выдал одноразовый токен).</li>
</ul>
</div>
</div>


<script>
// ИНИЦИАЛИЗАЦИЯ Telegram WebApp
const tg = window.Telegram.WebApp;
tg.expand();


// --- Настройки: заменить на ваши реальные API endpoints ---
const API_BASE = "https://example.com/api"; // <- заменить


// DOM
const serverSelect = document.getElementById('serverSelect');
const refreshBtn = document.getElementById('refreshServers');
const connectBtn = document.getElementById('connectBtn');
const disconnectBtn = document.getElementById('disconnectBtn');
const statusEl = document.getElementById('status');
const configArea = document.getElementById('configArea');
const copyBtn = document.getElementById('copyConfig');
const sendToBotBtn = document.getElementById('sendToBot');


let currentState = { connected:false, server:null, config:null };


function setStatus(connected, text){
currentState.connected = connected;
</html>
