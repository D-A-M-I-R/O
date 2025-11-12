
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Juego de la Oca: Camino a la Inclusión</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
        }

        .header p {
            font-size: 1.1em;
            opacity: 0.9;
        }

        .content {
            padding: 40px;
        }

        .screen {
            display: none;
        }

        .screen.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .start-screen {
            text-align: center;
        }

        .start-screen h2 {
            color: #333;
            margin-bottom: 20px;
            font-size: 2em;
        }

        .features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }

        .feature-card {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
            padding: 20px;
            border-radius: 15px;
            text-align: center;
        }

        .feature-card.green {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
        }

        .feature-card.purple {
            background: linear-gradient(135deg, #a8edea 0%, #fed6e3 100%);
            color: #333;
        }

        .feature-card h3 {
            font-size: 1.5em;
            margin-bottom: 10px;
        }

        .feature-card p {
            font-size: 0.9em;
        }

        .btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 15px 40px;
            font-size: 1.1em;
            border-radius: 50px;
            cursor: pointer;
            margin: 10px;
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(102, 126, 234, 0.4);
        }

        .btn.secondary {
            background: #f0f0f0;
            color: #333;
        }

        .btn.secondary:hover {
            background: #e0e0e0;
        }

        .btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .session-screen {
            text-align: center;
            max-width: 700px;
            margin: 0 auto;
        }

        .session-screen h2 {
            color: #333;
            margin-bottom: 30px;
            font-size: 2em;
        }

        .session-code {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 30px;
            border-radius: 15px;
            margin: 20px 0;
        }

        .session-code h3 {
            font-size: 1.2em;
            margin-bottom: 10px;
            opacity: 0.9;
        }

        .code-display {
            font-size: 3em;
            font-weight: bold;
            letter-spacing: 10px;
            font-family: 'Courier New', monospace;
            margin: 20px 0;
        }

        .code-display.highlight {
            animation: pulse 1s infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .qr-container {
            background: white;
            padding: 20px;
            border-radius: 15px;
            margin: 20px 0;
            display: inline-block;
        }

        .qr-container h4 {
            color: #333;
            margin-bottom: 15px;
            font-size: 1.1em;
        }

        #qrcode {
            display: flex;
            justify-content: center;
        }

        .copy-btn {
            background: white;
            color: #667eea;
            padding: 10px 20px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-weight: bold;
            margin-top: 10px;
        }

        .copy-btn:hover {
            background: #f0f0f0;
        }

        .join-options {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin: 30px 0;
        }

        .option-card {
            background: #f9f9f9;
            padding: 20px;
            border-radius: 15px;
            border: 2px solid #ddd;
        }

        .option-card h4 {
            color: #667eea;
            margin-bottom: 15px;
            font-size: 1.1em;
        }

        .option-card p {
            color: #666;
            font-size: 0.9em;
            margin-bottom: 15px;
        }

        .code-input-group {
            margin: 20px 0;
        }

        .code-input-group label {
            display: block;
            margin-bottom: 10px;
            color: #333;
            font-weight: 500;
        }

        .code-input-group input {
            width: 100%;
            padding: 15px;
            font-size: 1.5em;
            text-align: center;
            letter-spacing: 5px;
            border: 3px solid #ddd;
            border-radius: 10px;
            text-transform: uppercase;
        }

        .code-input-group input:focus {
            outline: none;
            border-color: #667eea;
        }

        .status-message {
            margin: 20px 0;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
        }

        .status-message.success {
            background: #d4edda;
            color: #155724;
        }

        .status-message.error {
            background: #f8d7da;
            color: #721c24;
        }

        .status-message.waiting {
            background: #d1ecf1;
            color: #0c5460;
        }

        .setup-screen {
            max-width: 600px;
            margin: 0 auto;
        }

        .setup-screen h2 {
            color: #333;
            margin-bottom: 30px;
            text-align: center;
        }

        .player-setup {
            background: #f9f9f9;
            padding: 20px;
            margin-bottom: 20px;
            border-radius: 10px;
            border-left: 5px solid #667eea;
        }

        .player-setup h3 {
            color: #667eea;
            margin-bottom: 15px;
        }

        .form-group {
            margin-bottom: 15px;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
            color: #333;
            font-weight: 500;
        }

        .form-group input {
            width: 100%;
            padding: 10px;
            border: 2px solid #ddd;
            border-radius: 5px;
            font-size: 1em;
        }

        .form-group input:focus {
            outline: none;
            border-color: #667eea;
        }

        .profiles {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
            margin-bottom: 15px;
        }

        .profile-btn {
            padding: 10px;
            border: 2px solid #ddd;
            background: white;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.2s;
            text-align: left;
            font-size: 0.9em;
        }

        .profile-btn:hover {
            border-color: #667eea;
            background: #f0f4ff;
        }

        .profile-btn.selected {
            border-color: #667eea;
            background: #667eea;
            color: white;
        }

        .profile-emoji {
            font-size: 1.5em;
            margin-right: 5px;
        }

        .game-screen {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .game-header {
            background: #f9f9f9;
            padding: 20px;
            border-radius: 10px;
            border-left: 5px solid #667eea;
        }

        .current-player {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 15px;
        }

        .player-avatar {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2em;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }

        .player-info h3 {
            color: #333;
            margin-bottom: 5px;
        }

        .player-info p {
            color: #666;
            font-size: 0.9em;
        }

        .dice-section {
            text-align: center;
            padding: 20px;
            background: #f0f4ff;
            border-radius: 10px;
        }

        .dice {
            width: 80px;
            height: 80px;
            background: white;
            border: 3px solid #667eea;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3em;
            margin: 20px auto;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        .dice.rolling {
            animation: diceRoll 0.6s ease-in-out;
        }

        @keyframes diceRoll {
            0%, 100% { transform: rotateX(0) rotateY(0) rotateZ(0); }
            25% { transform: rotateX(180deg) rotateY(180deg) rotateZ(90deg); }
            50% { transform: rotateX(360deg) rotateY(360deg) rotateZ(180deg); }
            75% { transform: rotateX(180deg) rotateY(180deg) rotateZ(270deg); }
        }

        .board {
            display: grid;
            grid-template-columns: repeat(9, 1fr);
            gap: 10px;
            background: #f9f9f9;
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
        }

        .cell {
            aspect-ratio: 1;
            background: white;
            border: 2px solid #ddd;
            border-radius: 8px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.2s;
            position: relative;
            min-height: 60px;
        }

        .cell:hover {
            transform: scale(1.05);
        }

        .cell.start {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
        }

        .cell.penalty {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
            border: none;
        }

        .cell.advance {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            color: white;
            border: none;
        }

        .cell.finish {
            background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%);
            color: white;
            border: none;
            font-size: 1.5em;
        }

        .cell-number {
            font-size: 0.8em;
            opacity: 0.7;
        }

        .cell-icon {
            font-size: 1.5em;
        }

        .players-list {
            background: #f9f9f9;
            padding: 20px;
            border-radius: 10px;
            margin-top: 20px;
        }

        .players-list h3 {
            color: #333;
            margin-bottom: 15px;
        }

        .player-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 10px;
            background: white;
            margin-bottom: 10px;
            border-radius: 8px;
            border-left: 4px solid #667eea;
        }

        .player-item.current {
            background: #f0f4ff;
            border-left-color: #43e97b;
        }

        .player-name {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .player-position {
            color: #666;
            font-size: 0.9em;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            align-items: center;
            justify-content: center;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: white;
            padding: 40px;
            border-radius: 20px;
            max-width: 500px;
            width: 90%;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            animation: slideUp 0.3s ease-out;
        }

        @keyframes slideUp {
            from {
                transform: translateY(50px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }

        .modal-content h2 {
            color: #667eea;
            margin-bottom: 20px;
            text-align: center;
        }

        .modal-content p {
            color: #333;
            line-height: 1.6;
            margin-bottom: 20px;
            font-size: 1.1em;
        }

        .answer-hint {
            background: #f0f4ff;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
            border-left: 4px solid #667eea;
            display: none;
        }

        .answer-hint.show {
            display: block;
        }

        .answer-hint strong {
            color: #667eea;
        }

        .victory-screen {
            text-align: center;
        }

        .victory-screen h2 {
            color: #43e97b;
            font-size: 2.5em;
            margin-bottom: 20px;
        }

        .victory-message {
            background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%);
            color: white;
            padding: 30px;
            border-radius: 15px;
            margin: 20px 0;
            font-size: 1.2em;
        }

        .button-group {
            display: flex;
            gap: 10px;
            justify-content: center;
            flex-wrap: wrap;
        }

        .waiting-players {
            background: #f0f4ff;
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
        }

        .waiting-players h3 {
            color: #667eea;
            margin-bottom: 15px;
        }

        .player-badge {
            display: inline-block;
            background: #667eea;
            color: white;
            padding: 8px 15px;
            border-radius: 20px;
            margin: 5px;
            font-size: 0.9em;
        }

        @media (max-width: 768px) {
            .header h1 {
                font-size: 1.8em;
            }

            .board {
                grid-template-columns: repeat(6, 1fr);
            }

            .profiles {
                grid-template-columns: 1fr;
            }

            .content {
                padding: 20px;
            }

            .join-options {
                grid-template-columns: 1fr;
            }

            .code-display {
                font-size: 2em;
                letter-spacing: 5px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🎲 Juego de la Oca</h1>
            <p>Camino a la Inclusión</p>
        </div>

        <div class="content">
            <!-- Pantalla de inicio -->
            <div id="startScreen" class="screen active">
                <div class="start-screen">
                    <h2>Bienvenido al Juego de la Oca</h2>
                    <p style="color: #666; margin-bottom: 30px; font-size: 1.1em;">
                        Un juego educativo sobre inclusión social y convivencia intercultural.
                    </p>
                    
                    <div class="features">
                        <div class="feature-card">
                            <div style="font-size: 2em; margin-bottom: 10px;">👥</div>
                            <h3>6 Perfiles</h3>
                            <p>Diferentes situaciones de vulnerabilidad</p>
                        </div>
                        <div class="feature-card green">
                            <div style="font-size: 2em; margin-bottom: 10px;">🎯</div>
                            <h3>63 Casillas</h3>
                            <p>Un camino lleno de desafíos</p>
                        </div>
                        <div class="feature-card purple">
                            <div style="font-size: 2em; margin-bottom: 10px;">💭</div>
                            <h3>Reflexión</h3>
                            <p>Preguntas para pensar y aprender</p>
                        </div>
                    </div>

                    <button class="btn" onclick="startGame()">¡Comenzar a Jugar! 🚀</button>
                </div>
            </div>

            <!-- Pantalla de sesión -->
            <div id="sessionScreen" class="screen">
                <div class="session-screen">
                    <h2>¡Bienvenido a la Sesión!</h2>
                    
                    <div class="session-code">
                        <h3>Código de Sesión</h3>
                        <div class="code-display highlight" id="sessionCode">ABC123</div>
                        <button class="copy-btn" onclick="copyCode()">📋 Copiar Código</button>
                        <p style="font-size: 0.9em; margin-top: 15px;">Comparte este código con tus compañeros</p>
                    </div>

                    <div class="qr-container">
                        <h4>📱 Código QR - Escanea para unirte</h4>
                        <div id="qrcode"></div>
                        <p style="color: #666; font-size: 0.9em; margin-top: 10px;">Tus compañeros pueden escanear este código</p>
                    </div>

                    <div class="join-options">
                        <div class="option-card">
                            <h4>📱 Opción 1: Escanear QR</h4>
                            <p>Tus compañeros escanean el código QR con sus móviles</p>
                            <p style="font-size: 0.8em; color: #999;">Se abrirá automáticamente con el código ingresado</p>
                        </div>
                        <div class="option-card">
                            <h4>📝 Opción 2: Código Manual</h4>
                            <p>Comparte el código y tus compañeros lo ingresan manualmente</p>
                            <p style="font-size: 0.8em; color: #999;">Más rápido si no tienen cámara</p>
                        </div>
                    </div>

                    <div class="waiting-players">
                        <h3>Jugadores Conectados</h3>
                        <div id="connectedPlayers" style="min-height: 50px;">
                            <p style="color: #666;">Esperando jugadores...</p>
                        </div>
                    </div>

                    <button class="btn" id="startGameBtn" onclick="startGameWithPlayers()" style="display: none;">
                        🎮 Comenzar Partida
                    </button>

                    <button class="btn secondary" onclick="goToStart()" style="margin-top: 20px;">← Atrás</button>
                </div>
            </div>

            <!-- Pantalla de unirse -->
            <div id="joinScreen" class="screen">
                <div class="setup-screen">
                    <h2>Unirse a una Sesión</h2>
                    
                    <div style="background: #f0f4ff; padding: 20px; border-radius: 10px; margin-bottom: 30px;">
                        <p style="color: #667eea; font-weight: bold; margin-bottom: 10px;">📱 Opción 1: Escanea el código QR</p>
                        <p style="color: #666; font-size: 0.9em;">Pídele al anfitrión que comparta el código QR</p>
                    </div>

                    <div style="text-align: center; color: #999; margin: 20px 0;">O</div>

                    <div style="background: #fff3cd; padding: 20px; border-radius: 10px;">
                        <p style="color: #856404; font-weight: bold; margin-bottom: 15px;">📝 Opción 2: Ingresa el código manualmente</p>
                        <div class="code-input-group">
                            <label>Código de la sesión:</label>
                            <input type="text" id="sessionCodeInput" placeholder="ABC123" maxlength="6" onkeyup="checkCode()">
                        </div>

                        <div id="statusMessage"></div>

                        <button class="btn" id="joinBtn" onclick="joinSession()" style="display: none;">
                            ✓ Unirse
                        </button>
                    </div>

                    <button class="btn secondary" onclick="goToStart()" style="margin-top: 20px;">← Atrás</button>
                </div>
            </div>

            <!-- Pantalla de configuración del jugador -->
            <div id="playerSetupScreen" class="screen">
                <div class="setup-screen">
                    <h2>Tu Perfil</h2>
                    
                    <div class="player-setup">
                        <h3>Información del Jugador</h3>
                        <div class="form-group">
                            <label>Tu Nombre</label>
                            <input type="text" id="playerNameInput" placeholder="Escribe tu nombre">
                        </div>
                        <div class="form-group">
                            <label>Elige tu perfil</label>
                            <div class="profiles" id="profilesContainer"></div>
                        </div>
                    </div>

                    <div style="text-align: center; margin-top: 30px;">
                        <button class="btn" id="confirmPlayerBtn" onclick="confirmPlayerSetup()" style="display: none;">
                            ✓ Confirmar
                        </button>
                    </div>
                </div>
            </div>

            <!-- Pantalla del juego -->
            <div id="gameScreen" class="screen">
                <div class="game-screen">
                    <div class="game-header">
                        <div class="current-player">
                            <div class="player-avatar" id="currentPlayerAvatar">👤</div>
                            <div class="player-info">
                                <h3 id="currentPlayerName">Jugador</h3>
                                <p id="currentPlayerProfile">Perfil</p>
                            </div>
                        </div>
                        <div style="text-align: center;">
                            <p style="color: #666; margin-bottom: 10px;">Casilla actual</p>
                            <p style="font-size: 2em; color: #667eea; font-weight: bold;" id="currentPosition">1 / 63</p>
                        </div>
                    </div>

                    <div class="dice-section">
                        <p style="color: #666; margin-bottom: 10px;">Lanza el dado para avanzar</p>
                        <div class="dice" id="diceDisplay">🎲</div>
                        <button class="btn" id="rollDiceBtn" onclick="rollDice()">🎲 Lanzar Dado</button>
                    </div>

                    <div class="board" id="gameBoard"></div>

                    <div class="players-list">
                        <h3>Todos los Jugadores</h3>
                        <div id="playersList"></div>
                    </div>

                    <div style="text-align: center;">
                        <button class="btn secondary" onclick="goToStart()">🏠 Nuevo Juego</button>
                    </div>
                </div>
            </div>

            <!-- Pantalla de victoria -->
            <div id="victoryScreen" class="screen">
                <div class="victory-screen">
                    <h2>🎉 ¡Felicidades!</h2>
                    <div class="victory-message">
                        <p id="victoryMessage">¡Has llegado a la inclusión!</p>
                    </div>
                    <p style="color: #666; font-size: 1.1em; margin: 20px 0;">
                        Gracias por jugar y reflexionar sobre la importancia de la inclusión social.
                    </p>
                    <div class="button-group">
                        <button class="btn" onclick="startGame()">🔄 Jugar de Nuevo</button>
                        <button class="btn secondary" onclick="goToStart()">🏠 Ir al Inicio</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal de reflexión -->
    <div id="reflectionModal" class="modal">
        <div class="modal-content">
            <h2>💭 Momento de Reflexión</h2>
            <p id="reflectionQuestion">Pregunta de reflexión</p>
            <button class="btn secondary" onclick="toggleAnswer()" style="width: 100%; margin-bottom: 15px;">
                Ver respuesta sugerida para educadores
            </button>
            <div class="answer-hint" id="answerHint">
                <strong>Respuesta sugerida:</strong>
                <p id="answerText">Respuesta</p>
            </div>
            <button class="btn" onclick="closeReflectionModal()" style="width: 100%;">Continuar Juego ➡️</button>
        </div>
    </div>

    <script>
        // Datos del juego
        const PROFILES = [
            { name: '👩 Mujer inmigrante sin trabajo', emoji: '👩', description: 'Enfrenta discriminación laboral y de género' },
            { name: '👨 Hombre inmigrante', emoji: '👨', description: 'Busca oportunidades en un nuevo país' },
            { name: '♿ Persona con discapacidad', emoji: '♿', description: 'Enfrenta barreras de accesibilidad' },
            { name: '👨‍👩‍👧‍👦 Familia en situación económica difícil', emoji: '👨‍👩‍👧‍👦', description: 'Lucha por cubrir necesidades básicas' },
            { name: '🎓 Jóvenes sin acceso a educación', emoji: '🎓', description: 'Sin oportunidades de formación' },
            { name: '📄 Persona sin documentación', emoji: '📄', description: 'Sin papeles legales en el país' }
        ];

        const BOARD_CELLS = [
            { number: 1, type: 'start', name: 'SALIDA', icon: '🏁' },
            { number: 2, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 3, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 4, type: 'penalty', name: 'No consiguió empleo', icon: '⚠️' },
            { number: 5, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 6, type: 'advance', name: 'Ha encontrado trabajo', icon: '⭐' },
            { number: 7, type: 'penalty', name: 'Discriminación por género', icon: '⚠️' },
            { number: 8, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 9, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 10, type: 'penalty', name: 'Problemas para acceder a educación', icon: '⚠️' },
            { number: 11, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 12, type: 'advance', name: 'Ha conseguido papeles', icon: '⭐' },
            { number: 13, type: 'penalty', name: 'Falta de papeles', icon: '⚠️' },
            { number: 14, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 15, type: 'penalty', name: 'Dificultad para acceder a servicios de salud', icon: '⚠️' },
            { number: 16, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 17, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 18, type: 'penalty', name: 'Sin apoyo familiar', icon: '⚠️' },
            { number: 19, type: 'advance', name: 'Acceso a educación', icon: '⭐' },
            { number: 20, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 21, type: 'penalty', name: 'Vivienda precaria', icon: '⚠️' },
            { number: 22, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 23, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 24, type: 'penalty', name: 'Discriminación por discapacidad', icon: '⚠️' },
            { number: 25, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 26, type: 'advance', name: 'Recibe apoyo familiar', icon: '⭐' },
            { number: 27, type: 'penalty', name: 'Desempleo prolongado', icon: '⚠️' },
            { number: 28, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 29, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 30, type: 'penalty', name: 'Falta de transporte', icon: '⚠️' },
            { number: 31, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 32, type: 'advance', name: 'Participa en actividades comunitarias', icon: '⭐' },
            { number: 33, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 34, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 35, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 36, type: 'penalty', name: 'Exclusión social', icon: '⚠️' },
            { number: 37, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 38, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 39, type: 'penalty', name: 'Pérdida de documentos', icon: '⚠️' },
            { number: 40, type: 'advance', name: 'Mejora de vivienda', icon: '⭐' },
            { number: 41, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 42, type: 'penalty', name: 'Acceso limitado a cultura', icon: '⚠️' },
            { number: 43, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 44, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 45, type: 'penalty', name: 'Problemas económicos', icon: '⚠️' },
            { number: 46, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 47, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 48, type: 'penalty', name: 'Falta de apoyo social', icon: '⚠️' },
            { number: 49, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 50, type: 'advance', name: 'Acceso a servicios de salud', icon: '⭐' },
            { number: 51, type: 'penalty', name: 'Exclusión educativa', icon: '⚠️' },
            { number: 52, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 53, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 54, type: 'penalty', name: 'Discriminación cultural', icon: '⚠️' },
            { number: 55, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 56, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 57, type: 'penalty', name: 'Desinformación', icon: '⚠️' },
            { number: 58, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 59, type: 'advance', name: 'Apoyo social', icon: '⭐' },
            { number: 60, type: 'penalty', name: 'Malentendidos por lengua', icon: '⚠️' },
            { number: 61, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 62, type: 'neutral', name: 'Camino', icon: '🛤️' },
            { number: 63, type: 'finish', name: 'INCLUSIÓN', icon: '🎯' }
        ];

        const REFLECTION_QUESTIONS = [
            {
                question: '¿Has visto en tu barrio alguna situación donde alguien fue excluido o rechazado? ¿Qué pasó?',
                answer: 'Esta pregunta busca que reflexiones sobre la exclusión social en tu entorno cercano. La inclusión comienza reconociendo que existen personas en situaciones vulnerables en nuestras comunidades.'
            },
            {
                question: '¿Qué significa para ti ser incluido en un grupo o comunidad?',
                answer: 'La inclusión implica sentirse aceptado, valorado y tener oportunidades iguales. No es solo estar presente, sino ser parte activa de la comunidad.'
            },
            {
                question: '¿Cómo crees que se sentiría alguien sin documentación en tu país?',
                answer: 'Las personas sin documentación enfrentan miedo, inseguridad y limitaciones en acceso a servicios. La empatía nos ayuda a entender sus desafíos.'
            },
            {
                question: '¿Qué barreras enfrentan las personas con discapacidad en tu comunidad?',
                answer: 'Las barreras pueden ser físicas (escaleras, falta de rampas), sociales (discriminación) o de acceso (a educación, trabajo). Identificarlas es el primer paso para eliminarlas.'
            },
            {
                question: '¿Cómo podemos ayudar a jóvenes sin acceso a educación?',
                answer: 'Podemos apoyar a través de programas educativos, mentoría, becas o simplemente brindando oportunidades. La educación es clave para la inclusión social.'
            },
            {
                question: '¿Qué significa convivencia intercultural?',
                answer: 'Es la coexistencia respetuosa y enriquecedora de personas de diferentes culturas. Implica aprender unos de otros y valorar la diversidad.'
            },
            {
                question: '¿Cómo afecta la discriminación a las mujeres inmigrantes?',
                answer: 'Las mujeres inmigrantes enfrentan discriminación múltiple: por género, por origen. Esto limita sus oportunidades laborales y sociales.'
            },
            {
                question: '¿Qué recursos comunitarios conoces que ayuden a personas vulnerables?',
                answer: 'Pueden ser centros sociales, ONGs, programas de empleo, servicios de salud. Conocer estos recursos es importante para poder ayudar a otros.'
            },
            {
                question: '¿Cómo podemos crear una sociedad más inclusiva?',
                answer: 'A través de políticas inclusivas, educación, respeto a la diversidad, acceso igualitario a servicios y oportunidades, y solidaridad comunitaria.'
            },
            {
                question: '¿Qué rol juega la solidaridad en la inclusión social?',
                answer: 'La solidaridad es fundamental. Significa apoyar a otros, reconocer sus derechos y trabajar juntos por una sociedad más justa e inclusiva.'
            }
        ];

        // Estado del juego
        let gameState = {
            sessionCode: null,
            players: [],
            currentPlayerIndex: 0,
            gameStarted: false,
            diceRolling: false,
            playerName: null,
            playerProfile: null,
            selectedProfileIdx: null,
            isHost: false
        };

        // Funciones de navegación
        function startGame() {
            gameState.isHost = true;
            gameState.sessionCode = generateSessionCode();
            renderSessionScreen();
            showScreen('sessionScreen');
        }

        function generateSessionCode() {
            const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
            let code = '';
            for (let i = 0; i < 6; i++) {
                code += chars.charAt(Math.floor(Math.random() * chars.length));
            }
            return code;
        }

        function renderSessionScreen() {
            document.getElementById('sessionCode').textContent = gameState.sessionCode;
            generateQRCode();
            updateConnectedPlayers();
        }

        function generateQRCode() {
            const qrcodeDiv = document.getElementById('qrcode');
            qrcodeDiv.innerHTML = '';
            
            const currentURL = window.location.href.split('?')[0];
            const qrURL = currentURL + '?code=' + gameState.sessionCode;
            
            new QRCode(qrcodeDiv, {
                text: qrURL,
                width: 250,
                height: 250,
                colorDark: "#667eea",
                colorLight: "#ffffff",
                correctLevel: QRCode.CorrectLevel.H
            });
        }

        function updateConnectedPlayers() {
            const container = document.getElementById('connectedPlayers');
            if (gameState.players.length === 0) {
                container.innerHTML = '<p style="color: #666;">Esperando jugadores...</p>';
            } else {
                let html = '';
                gameState.players.forEach(player => {
                    html += `<div class="player-badge">${player.profile.emoji} ${player.name}</div>`;
                });
                container.innerHTML = html;
                
                if (gameState.players.length >= 2) {
                    document.getElementById('startGameBtn').style.display = 'inline-block';
                }
            }
        }

        function copyCode() {
            navigator.clipboard.writeText(gameState.sessionCode);
            alert('Código copiado: ' + gameState.sessionCode);
        }

        function checkCode() {
            const input = document.getElementById('sessionCodeInput').value.toUpperCase();
            const statusDiv = document.getElementById('statusMessage');
            const joinBtn = document.getElementById('joinBtn');

            if (input.length === 6) {
                if (input === gameState.sessionCode) {
                    statusDiv.innerHTML = '<div class="status-message success">✓ Código válido. ¡Puedes unirte!</div>';
                    joinBtn.style.display = 'inline-block';
                } else {
                    statusDiv.innerHTML = '<div class="status-message error">✗ Código inválido. Intenta de nuevo.</div>';
                    joinBtn.style.display = 'none';
                }
            } else {
                statusDiv.innerHTML = '';
                joinBtn.style.display = 'none';
            }
        }

        function joinSession() {
            const code = document.getElementById('sessionCodeInput').value.toUpperCase();
            if (code === gameState.sessionCode) {
                gameState.isHost = false;
                renderPlayerProfileSetup();
                showScreen('playerSetupScreen');
            }
        }

        function renderPlayerProfileSetup() {
            const container = document.getElementById('profilesContainer');
            container.innerHTML = '';

            PROFILES.forEach((profile, idx) => {
                const btn = document.createElement('button');
                btn.className = 'profile-btn';
                btn.innerHTML = `<span class="profile-emoji">${profile.emoji}</span> ${profile.name}`;
                btn.onclick = () => selectPlayerProfile(idx);
                container.appendChild(btn);
            });
        }

        function selectPlayerProfile(idx) {
            gameState.selectedProfileIdx = idx;
            
            const buttons = document.querySelectorAll('#profilesContainer .profile-btn');
            buttons.forEach((btn, i) => {
                btn.classList.toggle('selected', i === idx);
            });

            checkPlayerSetupComplete();
        }

        function checkPlayerSetupComplete() {
            const name = document.getElementById('playerNameInput').value.trim();
            const hasProfile = gameState.selectedProfileIdx !== null;
            const confirmBtn = document.getElementById('confirmPlayerBtn');

            if (name && hasProfile) {
                confirmBtn.style.display = 'inline-block';
            } else {
                confirmBtn.style.display = 'none';
            }
        }

        function confirmPlayerSetup() {
            const name = document.getElementById('playerNameInput').value.trim();
            if (!name || gameState.selectedProfileIdx === null) {
                alert('Por favor completa tu nombre y selecciona un perfil');
                return;
            }

            const profile = PROFILES[gameState.selectedProfileIdx];
            gameState.playerName = name;
            gameState.playerProfile = profile;

            gameState.players.push({
                name: name,
                profile: profile,
                position: 1,
                profileIndex: gameState.selectedProfileIdx
            });

            updateConnectedPlayers();
            
            if (gameState.isHost) {
                showScreen('sessionScreen');
            } else {
                const statusDiv = document.getElementById('statusMessage');
                statusDiv.innerHTML = '<div class="status-message waiting">✓ Te has unido a la sesión. Esperando a que el anfitrión inicie el juego...</div>';
                document.getElementById('confirmPlayerBtn').style.display = 'none';
                document.getElementById('playerSetupScreen').style.display = 'none';
            }
        }

        function startGameWithPlayers() {
            if (gameState.players.length < 2) {
                alert('Se necesitan al menos 2 jugadores para comenzar');
                return;
            }

            gameState.currentPlayerIndex = 0;
            gameState.gameStarted = true;
            renderGame();
            showScreen('gameScreen');
        }

        function renderGame() {
            const boardContainer = document.getElementById('gameBoard');
            boardContainer.innerHTML = '';
            
            BOARD_CELLS.forEach(cell => {
                const cellDiv = document.createElement('div');
                cellDiv.className = `cell ${cell.type}`;
                cellDiv.innerHTML = `
                    <div class="cell-number">${cell.number}</div>
                    <div class="cell-icon">${cell.icon}</div>
                `;
                
                const playersOnCell = gameState.players.filter(p => p.position === cell.number);
                if (playersOnCell.length > 0) {
                    const avatarsDiv = document.createElement('div');
                    avatarsDiv.style.display = 'flex';
                    avatarsDiv.style.gap = '3px';
                    avatarsDiv.style.marginTop = '5px';
                    playersOnCell.forEach(player => {
                        const avatar = document.createElement('div');
                        avatar.style.width = '20px';
                        avatar.style.height = '20px';
                        avatar.style.borderRadius = '50%';
                        avatar.style.display = 'flex';
                        avatar.style.alignItems = 'center';
                        avatar.style.justifyContent = 'center';
                        avatar.style.fontSize = '0.8em';
                        avatar.style.background = 'rgba(255, 255, 255, 0.3)';
                        avatar.textContent = player.profile.emoji;
                        avatarsDiv.appendChild(avatar);
                    });
                    cellDiv.appendChild(avatarsDiv);
                }
                
                boardContainer.appendChild(cellDiv);
            });

            updateCurrentPlayerDisplay();
            updatePlayersList();
        }

        function updateCurrentPlayerDisplay() {
            const player = gameState.players[gameState.currentPlayerIndex];
            document.getElementById('currentPlayerAvatar').textContent = player.profile.emoji;
            document.getElementById('currentPlayerName').textContent = player.name;
            document.getElementById('currentPlayerProfile').textContent = player.profile.description;
            document.getElementById('currentPosition').textContent = `${player.position} / 63`;
        }

        function updatePlayersList() {
            const listContainer = document.getElementById('playersList');
            listContainer.innerHTML = '';
            
            gameState.players.forEach((player, idx) => {
                const playerDiv = document.createElement('div');
                playerDiv.className = `player-item ${idx === gameState.currentPlayerIndex ? 'current' : ''}`;
                playerDiv.innerHTML = `
                    <div class="player-name">
                        <span>${player.profile.emoji}</span>
                        <strong>${player.name}</strong>
                    </div>
                    <div class="player-position">Casilla ${player.position}</div>
                `;
                listContainer.appendChild(playerDiv);
            });
        }

        function rollDice() {
            if (gameState.diceRolling) return;
            
            gameState.diceRolling = true;
            const diceDisplay = document.getElementById('diceDisplay');
            const rollDiceBtn = document.getElementById('rollDiceBtn');
            
            rollDiceBtn.disabled = true;
            diceDisplay.classList.add('rolling');
            
            let rolls = 0;
            const rollInterval = setInterval(() => {
                const randomDice = Math.floor(Math.random() * 6) + 1;
                diceDisplay.textContent = randomDice;
                rolls++;
                
                if (rolls > 10) {
                    clearInterval(rollInterval);
                    const finalDice = Math.floor(Math.random() * 6) + 1;
                    diceDisplay.textContent = finalDice;
                    diceDisplay.classList.remove('rolling');
                    
                    setTimeout(() => {
                        movePlayer(finalDice);
                        gameState.diceRolling = false;
                        rollDiceBtn.disabled = false;
                    }, 300);
                }
            }, 50);
        }

        function movePlayer(diceValue) {
            const player = gameState.players[gameState.currentPlayerIndex];
            let newPosition = player.position + diceValue;
            
            if (newPosition > 63) {
                newPosition = 63 - (newPosition - 63);
            }
            
            player.position = newPosition;
            
            renderGame();
            
            const randomQuestion = REFLECTION_QUESTIONS[Math.floor(Math.random() * REFLECTION_QUESTIONS.length)];
            showReflectionModal(randomQuestion);
        }

        function showReflectionModal(question) {
            document.getElementById('reflectionQuestion').textContent = question.question;
            document.getElementById('answerText').textContent = question.answer;
            document.getElementById('answerHint').classList.remove('show');
            document.getElementById('reflectionModal').classList.add('active');
        }

        function toggleAnswer() {
            document.getElementById('answerHint').classList.toggle('show');
        }

        function closeReflectionModal() {
            document.getElementById('reflectionModal').classList.remove('active');
            
            const player = gameState.players[gameState.currentPlayerIndex];
            
            if (player.position >= 63) {
                showVictoryScreen(player);
            } else {
                gameState.currentPlayerIndex = (gameState.currentPlayerIndex + 1) % gameState.players.length;
                updateCurrentPlayerDisplay();
                updatePlayersList();
            }
        }

        function showVictoryScreen(winner) {
            document.getElementById('victoryMessage').textContent = 
                `¡${winner.name} ha llegado a la INCLUSIÓN! 🎉`;
            showScreen('victoryScreen');
        }

        function showScreen(screenId) {
            document.querySelectorAll('.screen').forEach(screen => {
                screen.classList.remove('active');
            });
            document.getElementById(screenId).classList.add('active');
        }

        function goToStart() {
            gameState = {
                sessionCode: null,
                players: [],
                currentPlayerIndex: 0,
                gameStarted: false,
                diceRolling: false,
                playerName: null,
                playerProfile: null,
                selectedProfileIdx: null,
                isHost: false
            };
            showScreen('startScreen');
        }

        // Verificar si hay un código en la URL
        function checkURLCode() {
            const params = new URLSearchParams(window.location.search);
            const code = params.get('code');
            if (code) {
                gameState.sessionCode = code;
                // No pre-ingresamos el código, dejamos que el usuario lo escriba
                showScreen('joinScreen');
            }
        }

        // Inicializar
        document.addEventListener('DOMContentLoaded', function() {
            checkURLCode();
            const playerNameInput = document.getElementById('playerNameInput');
            if (playerNameInput) {
                playerNameInput.addEventListener('input', checkPlayerSetupComplete);
            }
        });
    </script>
</body>
</html>
