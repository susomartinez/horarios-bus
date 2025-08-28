<script>
    // Paradas favoritas hardcodeadas
    const paradasFavoritas = [
        { id: 20111, nome: "Cunqueiro (hospital de día)" },
        { id: 6570, nome: "Pizarro dirección centro (nº 65)" },
        { id: 2040, nome: "Avenida de Madrid (Fogar)" },
        { id: 4280, nome: "Detrás da Avenida de Madrid (Emilia Pardo Bazán)" },
        { id: 6550, nome: "Pizarro dirección Calvario (nº 10)" }
    ];
    
    let numeroParada = '';
    
    function redirigirAParada(paradaId) {
        if (paradaId) {
            // Redirección directa á páxina de Vitrasa
            window.location.href = `http://infobus.vitrasa.es:8002/Default.aspx?parada=${paradaId}`;
        }
    }
    
    function buscarParada() {
        if (numeroParada) {
            redirigirAParada(numeroParada);
        }
    }
    
    // Para permitir buscar con Enter
    function handleKeyPress(e) {
        if (e.key === 'Enter') {
            buscarParada();
        }
    }
</script>

<div class="container">
    <header>
        <h1>🚌 Horarios</h1>
    </header>
    
    <div class="busqueda">
        <div class="input-group">
            <input 
                type="text" 
                bind:value={numeroParada}
                placeholder="Introduce o número de parada"
                on:keypress={handleKeyPress}
            />
            <button on:click={buscarParada} class="buscar-btn">
                → Ver Horarios
            </button>
        </div>
    </div>
    
    <div class="paradas-favoritas">
        <h2>📍 Paradas Frecuentes</h2>
        <div class="lista-paradas">
            {#each paradasFavoritas as parada}
                <button 
                    class="parada-btn"
                    on:click={() => redirigirAParada(parada.id)}
                    title="Ver horarios da parada {parada.id}"
                >
                    <span class="parada-nome">{parada.nome}</span>
                    <span class="parada-numero">{parada.id}</span>
                </button>
            {/each}
        </div>
    </div>
    
    <footer>
        <p>Horarios proporcionados por <a href="http://www.vitrasa.es" target="_blank">Vitrasa</a></p>
    </footer>
</div>

<style>
    .container {
        max-width: 600px;
        margin: 0 auto;
        padding: 20px;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        min-height: 100vh;
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        color: white;
    }
    
    header {
        text-align: center;
        margin-bottom: 30px;
    }
    
    header h1 {
        margin: 0;
        font-size: 2.5em;
        text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
    }
    
    .busqueda {
        background: rgba(255, 255, 255, 0.1);
        padding: 25px;
        border-radius: 15px;
        margin-bottom: 30px;
        backdrop-filter: blur(10px);
    }
    
    .input-group {
        display: flex;
        gap: 10px;
    }
    
    input {
        flex: 1;
        padding: 15px;
        border: none;
        border-radius: 8px;
        font-size: 16px;
        background: rgba(255, 255, 255, 0.9);
        color: #333;
    }
    
    input:focus {
        outline: none;
        box-shadow: 0 0 0 3px rgba(255, 255, 255, 0.5);
    }
    
    .buscar-btn {
        padding: 15px 20px;
        background: #ff6b6b;
        color: white;
        border: none;
        border-radius: 8px;
        font-size: 16px;
        font-weight: bold;
        cursor: pointer;
        transition: transform 0.2s;
    }
    
    .buscar-btn:hover {
        transform: translateY(-2px);
        background: #ff5252;
    }
    
    .paradas-favoritas {
        background: rgba(255, 255, 255, 0.1);
        padding: 25px;
        border-radius: 15px;
        backdrop-filter: blur(10px);
    }
    
    .paradas-favoritas h2 {
        margin-top: 0;
        text-align: center;
        font-size: 1.5em;
    }
    
    .lista-paradas {
        display: grid;
        gap: 12px;
    }
    
    .parada-btn {
        display: flex;
        align-items: center;
        gap: 15px;
        padding: 18px;
        background: rgba(255, 255, 255, 0.15);
        border: 1px solid rgba(255, 255, 255, 0.2);
        border-radius: 10px;
        color: white;
        cursor: pointer;
        transition: all 0.3s ease;
        text-align: left;
    }
    
    .parada-btn:hover {
        background: rgba(255, 255, 255, 0.25);
        transform: translateX(5px);
    }
    
    .parada-numero {
        font-size: 1em;
        font-weight: bold;
        padding: 8px 12px;
        min-width: 60px;
        text-align: center;
    }
    
    .parada-nome {
        flex: 1;
        font-size: 1.3em;
    }
    
    footer {
        text-align: center;
        margin-top: 40px;
        opacity: 0.8;
        font-size: 0.9em;
    }
    
    footer a {
        color: #ffd700;
        text-decoration: none;
    }
    
    footer a:hover {
        text-decoration: underline;
    }
    
    /* Responsive */
    @media (max-width: 480px) {
        .container {
            padding: 15px;
        }
        
        .input-group {
            flex-direction: column;
        }
        
        header h1 {
            font-size: 2em;
        }
        
        .parada-btn {
            flex-direction: column;
            gap: 8px;
            text-align: center;
        }
        
        .parada-numero {
            min-width: auto;
        }
    }
</style>