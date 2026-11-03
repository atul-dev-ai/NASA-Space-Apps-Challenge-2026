# Little Astronauts: Junior Astronaut Mission Trainer
**NASA Space Apps Challenge 2026 — Astro Squad**
*Complete Game Architecture, Art Bible, Game Mechanics & Technical Implementation Blueprint*

---

## 1. Executive Summary & Game Concept
* **Title**: Little Astronauts
* **Target Audience**: Children & Junior Explorers (Ages 7–14)
* **Genre**: Educational Space Exploration & Resource Management Simulation
* **Platform**: Modern Web Browsers (Chrome, Edge, Safari, Firefox) via WebGL / Three.js
* **Core Loop Philosophy**: `LEARN → EXPLORE → DECIDE → SURVIVE`
* **Core Objective**: Guide a 4-person crew through 30 Sols (Martian days) on a simulated outpost using real NASA weather & telemetry data while balancing life-support resources.

---

## 2. Visual Style & "Child-Friendly Mars" Art Bible

Jehetu eta children-focused game, Mars-er gloomy ba harsh look-er poriborte **Friendly Stylized Realism** (vibrant, warm, tactile, readable) use kora hobe:

### 2.1 Color Palette
* **Terrain & Ground**:
  * Rich Terracotta (`#C1440E`)
  * Warm Mars Sand (`#D97D54`)
  * Crater Shadow Auburn (`#7A260C`)
* **Atmosphere & Sky**:
  * Daytime Sky: Warm Pale Apricot (`#F4C29E`)
  * Solar Dusk: Soft Periwinkle & Violet (`#6B4C74`)
  * Night / Deep Space: Deep Indigo (`#0B0E14`) with bright twinkling stars
* **Base Architecture & Habitat**:
  * Outer Structure: Pearl White composite panels (`#F0F4F8`)
  * Transparent Domes: Soft Ice-Cyan glass (`#A8E6CF` with 40% opacity)
* **Resource UI Accents (High Contrast & Playful)**:
  * Oxygen ($O_2$): Bright Mint Cyan (`#00F0FF`)
  * Power ($\text{kWh}$): Electric Solar Amber (`#FFB800`)
  * Water ($H_2O$): Pure Aqua Blue (`#0088FF`)
  * Food: Fresh Sprout Green (`#39D353`)
  * Danger / Critical Warning: Neon Coral Red (`#FF3B30`)

### 2.2 Environment & 3D Assets (Three.js Low-to-Medium Poly)
1. **Martian Outpost**:
   * Interconnected circular bio-domes with transparent pressurized tunnels.
   * Hydroponic dome interior: bright visible green plants that bounce gently.
2. **Solar Panels & Wind Turbines**:
   * Friendly hexagonal solar array.
   * Accumulates fine red dust over time, which players can clean.
3. **The Rover**:
   * Rounded corners, chunky springy rover tires, and big friendly camera "eyes" (reminiscent of Curiosity & Wall-E).
   * Leaves low-gravity dust trails behind wheels when moving.
4. **Lighting & Particles**:
   * Ambient light + Warm Directional Sun Light ($0.43 \times \text{Earth Sunlight}$ luminosity).
   * Floating airborne micro-dust particles moving slowly to emphasize Mars gravity ($0.38g$).

---

## 3. Inside Rocket & Cockpit Interactive Animation Guide

Rocket-er cockpit ebong launch screen-ti bachader jonno highly immersive ebong joyful kora hobe:

### 3.1 Cockpit Visual Hierarchy
* **Central Windshield (Viewport)**:
  * Curved panoramic canopy looking out into space.
* **Flight Dashboard & Interactive Consoles**:
  * Big, tactile push buttons with round corners and embossed borders.
  * Interactive lever for "Thrust" and toggle switches with clicking sound effects.
  * Three glowing holographic circular dials for: `O2 Status`, `Thruster Heat`, and `Trajectory Target`.
* **The AI Advisor Hologram Screen**:
  * A retro-futuristic round screen showing a friendly floating robot mascot (`Astro-Bot`) that blinks and speaks during mission transitions.

### 3.2 Animation Timeline & Behavior
1. **Idle State**:
   * Soft pulsing console lights.
   * Floating personal items inside the cabin demonstrating weightlessness (e.g., floating star sticker, glowing mini-globe).
   * The astronaut suit arms on screen gently bob up and down.
2. **Launch & Acceleration Animation**:
   * Screen Shake: Controlled Three.js camera vibration along the $Z$ and $Y$ axis ($0.05 \text{ to } 0.1$ amplitude).
   * Window Transition: Blue Earth atmosphere slowly stretches $\rightarrow$ Star trails form $\rightarrow$ Deep Indigo Space appears with Earth receding into the background.
3. **Arrival at Mars Orbit**:
   * Red Planet Mars slowly fills the circular window.
   * Atmospheric entry orange glow effect on the canopy edges.
   * Touchdown hydraulics decompression sound and cabin stabilization.

---

## 4. The 4-Stage Learning Arc (Levels 0–20)

Game-ti 4-ti progressive learning phase-e structured:

| Stage | Levels | Title | Learning Focus | Gameplay Tasks |
| :--- | :--- | :--- | :--- | :--- |
| **Stage 1** | Levels 0–5 | **Explore** | Sun, Moon, Earth, Solar System | Orbit interactive 3D planets, scan planet layers, learn scale and gravity. |
| **Stage 2** | Levels 6–10 | **Discover** | Rockets, Spacesuits, Rovers, NASA Missions | Assemble a staged rocket, suit up the astronaut with correct thermal layers, test drive rover on obstacle test track. |
| **Stage 3** | Levels 11–18 | **Understand** | Life in Space, Gravity, Mars Atmosphere, Radiation | Calculate daily human needs, radiation shielding placement, atmospheric pressure comparisons. |
| **Stage 4** | Levels 19–20 | **Lead** | Outpost Commander Certification | Design your own base layout, configure power grid, and start the 30-Sol Mars Survival Mission. |

---

## 5. The Core Survival Loop: 30 Sols on Mars

Proti Martian Sol (day) 3-ti definite action phase-e chole:

### 5.1 Phase 1: READ (NASA Telemetry Influx)
* Daily Morning Report pops up on the Outpost Monitor.
* Parameters imported from simulated/cached NASA feeds:
  * **Temperature ($T_{min}, T_{max}$)**: e.g., $-75^\circ\text{C} \text{ to } -15^\circ\text{C}$
  * **Wind Speed & Dust Opacity ($\tau$)**: Determines solar panel efficiency.
  * **Atmospheric Pressure**: Dictates dome seal strain.
  * **Solar Radiation / UV Index**: Restricts EVA (Extra-Vehicular Activity) hours.

### 5.2 Phase 2: PLAN (Resource Balancing)
* The player has a 4-person crew:
  * **Commander**, **Engineer**, **Biologist**, **Geologist**.
* Daily baseline crew consumption:
  * $\text{Oxygen} = 4 \times 0.84\text{ kg} = 3.36\text{ kg/sol}$
  * $\text{Water} = 4 \times 2.5\text{ L} = 10\text{ L/sol}$
  * $\text{Food} = 4 \times 2000\text{ kcal} = 8000\text{ kcal/sol}$
  * $\text{Base Life-Support Power} = 15\text{ kWh/sol}$
* Player assigns power sliders:
  * Life Support (Oxygen Generator + Thermal Heating)
  * Hydroponic Lighting (Food production)
  * Water Recycling System
  * Research Lab & Communications Array

### 5.3 Phase 3: ACT (Maintenance & Mission Decisions)
* Player selects 2 actions per Sol:
  1. *Clean Solar Array* (Boost power generation after dust storm).
  2. *Harvest Hydroponic Bay* (Replenish Food pantry).
  3. *Conduct Rover Geology Run* (Discover underground ice $\rightarrow$ Water bonus).
  4. *Base Reinforcement* (Prevent pressure leaks).
* Consequence Engine triggers random Sol events (e.g., "Dust Storm approaching in 2 Sols", "Heater malfunction in Dormitory").

---

## 6. System Architecture & NASA Data Pipeline

```
[ NASA Open APIs / Datasets ]
  ├── Perseverance MEDA (Weather, Temp, Wind, Dust)
  ├── Curiosity REMS & InSight (Pressure, Soil Temp)
  ├── Curiosity RAD & NASA DONKI (Radiation & Solar Events)
  └── NASA LRO (Lunar Albedo / Lighting)
                │
                ▼
      [ Python Pipeline ]
        • Data Cleaning & Normalization
        • Fallback Synthetic Generator (if offline)
        • Formats into structured daily JSON profiles
                │
                ▼
      [ Web App Frontend (Three.js + Vanilla JS / React) ]
        ├── 3D Viewport Engine (Canvas, Shaders, Models)
        ├── Game State Manager (30 Sols, Crew Stats, Resources)
        ├── Interactive HUD & Cockpit Glassmorphism UI
        └── AI Mission Advisor (Contextual Rule Engine)
```

### Daily Sol JSON Data Contract
```json
{
  "sol": 14,
  "nasa_source": "Perseverance MEDA",
  "weather": {
    "temperature_min_c": -82,
    "temperature_max_c": -18,
    "wind_speed_mps": 14.5,
    "dust_optical_depth": 0.85,
    "uv_radiation_level": "MODERATE"
  },
  "event": {
    "id": "SOLAR_FLARE_WARNING",
    "title": "Minor Solar Flare Incoming",
    "description": "Radiation levels spiking. EVA missions outside the dome are risky today.",
    "power_penalty_pct": 10
  }
}
```

---

## 7. Complete Starter Implementation (HTML5 + Three.js)

Tomader project start korar jonno eikhane ekta complete, fully-functional single-file prototype dewa holo ja direct browser-e run korbe:
* Mars 3D terrain ebong dome visualize kore.
* Real-time 30-Sol resource tracker (Oxygen, Water, Power, Food).
* Interactive Next-Sol step-by-step game loop.

```html:Interactive Game Prototype:index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Little Astronauts: 30 Sols on Mars</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; user-select: none; }
    body {
      background-color: #0b0e14;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      overflow: hidden;
      color: #fff;
    }
    #canvas-container { position: absolute; top: 0; left: 0; width: 100vw; height: 100vh; z-index: 1; }
    
    /* Top Mission Bar */
    .top-bar {
      position: absolute; top: 15px; left: 50%; transform: translateX(-50%);
      z-index: 10; display: flex; gap: 20px;
      background: rgba(18, 24, 38, 0.85);
      border: 2px solid #d97d54; border-radius: 30px;
      padding: 10px 30px; backdrop-filter: blur(10px);
      box-shadow: 0 8px 32px rgba(0,0,0,0.5);
    }
    .stat-badge { text-align: center; }
    .stat-badge .label { font-size: 11px; text-transform: uppercase; color: #a0aec0; letter-spacing: 1px; }
    .stat-badge .val { font-size: 18px; font-weight: bold; color: #00f0ff; }
    .stat-badge .val.power { color: #ffb800; }
    .stat-badge .val.food { color: #39d353; }
    .stat-badge .val.water { color: #0088ff; }

    /* Left Control & Advisor Window */
    .ui-panel {
      position: absolute; top: 90px; left: 20px; width: 340px;
      z-index: 10; background: rgba(15, 20, 32, 0.9);
      border: 1px solid rgba(217, 125, 84, 0.4);
      border-radius: 16px; padding: 20px; backdrop-filter: blur(8px);
    }
    .panel-title { font-size: 16px; font-weight: bold; color: #f4c29e; margin-bottom: 12px; display: flex; justify-content: space-between; }
    .telemetry-card {
      background: rgba(193, 68, 14, 0.15); border-left: 4px solid #c1440e;
      padding: 10px; border-radius: 6px; font-size: 13px; margin-bottom: 15px;
    }
    .advisor-bubble {
      background: rgba(0, 240, 255, 0.08); border: 1px dashed #00f0ff;
      border-radius: 10px; padding: 12px; font-size: 13px; color: #e2e8f0; line-height: 1.4;
      margin-bottom: 15px;
    }
    
    /* Action Buttons */
    .btn-group { display: flex; flex-direction: column; gap: 8px; }
    button.action-btn {
      background: #c1440e; color: #fff; border: none; padding: 10px 14px;
      border-radius: 8px; font-size: 13px; font-weight: 600; cursor: pointer;
      transition: all 0.2s; display: flex; justify-content: space-between;
    }
    button.action-btn:hover { background: #e05316; transform: translateY(-1px); }
    button.next-sol-btn {
      background: #00f0ff; color: #0b0e14; border: none; padding: 12px;
      border-radius: 8px; font-size: 15px; font-weight: bold; cursor: pointer;
      width: 100%; margin-top: 15px; text-transform: uppercase; letter-spacing: 1px;
    }
    button.next-sol-btn:hover { background: #66f6ff; box-shadow: 0 0 15px rgba(0, 240, 255, 0.4); }
  </style>
</head>
<body>

  <!-- Top Resource Bar -->
  <div class="top-bar">
    <div class="stat-badge"><div class="label">Sol Cycle</div><div class="val" id="sol-display">1 / 30</div></div>
    <div class="stat-badge"><div class="label">Oxygen ($O_2$)</div><div class="val" id="o2-display">100%</div></div>
    <div class="stat-badge"><div class="label">Power</div><div class="val power" id="power-display">100%</div></div>
    <div class="stat-badge"><div class="label">Water</div><div class="val water" id="water-display">100%</div></div>
    <div class="stat-badge"><div class="label">Food</div><div class="val food" id="food-display">100%</div></div>
  </div>

  <!-- Left Interaction HUD -->
  <div class="ui-panel">
    <div class="panel-title">
      <span>AI MISSION ADVISOR</span>
      <span style="color:#00f0ff;">ONLINE</span>
    </div>

    <div class="telemetry-card" id="telemetry-box">
      <strong>Mars Weather (MEDA Sim):</strong><br>
      • Temp: -64°C | Wind: 8.2 m/s<br>
      • Dust Optical Depth: Low
    </div>

    <div class="advisor-bubble" id="advisor-speech">
      "Welcome Commander! Our 4-person crew has landed. Allocate daily base power and make sure our life support stays green!"
    </div>

    <div class="panel-title">DAILY ACTIONS (Select 1 per Sol)</div>
    <div class="btn-group">
      <button class="action-btn" onclick="performAction('clean_solar')">
        <span>Clean Solar Panels</span><span>+Power</span>
      </button>
      <button class="action-btn" onclick="performAction('greenhouse')">
        <span>Tend Hydroponic Dome</span><span>+Food</span>
      </button>
      <button class="action-btn" onclick="performAction('ice_extraction')">
        <span>Extract Subsurface Ice</span><span>+Water</span>
      </button>
    </div>

    <button class="next-sol-btn" onclick="advanceSol()">Advance to Next Sol →</button>
  </div>

  <div id="canvas-container"></div>

  <script>
    // --- 1. Three.js Friendly Mars Scene Setup ---
    const container = document.getElementById('canvas-container');
    const scene = new THREE.Scene();
    scene.background = new THREE.Color(0xd97d54);
    scene.fog = new THREE.FogExp2(0xd97d54, 0.015);

    const camera = new THREE.PerspectiveCamera(60, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.set(0, 15, 30);
    camera.lookAt(0, 2, 0);

    const renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.shadowMap.enabled = true;
    container.appendChild(renderer.domElement);

    // Warm Directional Sunlight
    const sunLight = new THREE.DirectionalLight(0xffecd0, 1.2);
    sunLight.position.set(20, 40, 20);
    sunLight.castShadow = true;
    scene.add(sunLight);

    const ambientLight = new THREE.AmbientLight(0x7a260c, 0.8);
    scene.add(ambientLight);

    // Stylized Mars Ground Terrain
    const groundGeo = new THREE.PlaneGeometry(200, 200, 32, 32);
    const groundMat = new THREE.MeshStandardMaterial({ color: 0xc1440e, roughness: 0.9 });
    const ground = new THREE.Mesh(groundGeo, groundMat);
    ground.rotation.x = -Math.PI / 2;
    ground.receiveShadow = true;
    scene.add(ground);

    // Central Martian Bio-Dome
    const domeGeo = new THREE.SphereGeometry(6, 32, 16, 0, Math.PI * 2, 0, Math.PI / 2);
    const domeMat = new THREE.MeshPhysicalMaterial({
      color: 0xa8e6cf,
      transparent: true,
      opacity: 0.5,
      roughness: 0.1,
      transmission: 0.8
    });
    const dome = new THREE.Mesh(domeGeo, domeMat);
    dome.position.set(0, 0, 0);
    scene.add(dome);

    // Greenery Inside Dome (Hydroponics)
    const plantGeo = new THREE.ConeGeometry(0.8, 2, 8);
    const plantMat = new THREE.MeshStandardMaterial({ color: 0x39d353 });
    for(let i = -3; i <= 3; i += 2) {
      for(let j = -3; j <= 3; j += 2) {
        if(Math.sqrt(i*i + j*j) < 4.5) {
          const plant = new THREE.Mesh(plantGeo, plantMat);
          plant.position.set(i, 1, j);
          scene.add(plant);
        }
      }
    }

    // Solar Panel Arrays
    const solarGeo = new THREE.BoxGeometry(4, 0.2, 2);
    const solarMat = new THREE.MeshStandardMaterial({ color: 0x1a365d, metalness: 0.8, roughness: 0.2 });
    for(let k = 0; k < 3; k++) {
      const panel = new THREE.Mesh(solarGeo, solarMat);
      panel.position.set(-14 + (k * 5), 1, -8);
      panel.rotation.x = 0.3;
      scene.add(panel);
    }

    // Floating Low-Gravity Dust Particles
    const dustCount = 200;
    const dustGeo = new THREE.BufferGeometry();
    const dustPos = new Float32Array(dustCount * 3);
    for(let p = 0; p < dustCount * 3; p += 3) {
      dustPos[p] = (Math.random() - 0.5) * 60;
      dustPos[p+1] = Math.random() * 20;
      dustPos[p+2] = (Math.random() - 0.5) * 60;
    }
    dustGeo.setAttribute('position', new THREE.BufferAttribute(dustPos, 3));
    const dustMat = new THREE.PointsMaterial({ color: 0xf4c29e, size: 0.2, transparent: true, opacity: 0.6 });
    const dustSystem = new THREE.Points(dustGeo, dustMat);
    scene.add(dustSystem);

    // --- 2. Game State & Logic ---
    let gameState = {
      sol: 1,
      o2: 100,
      power: 100,
      water: 100,
      food: 100,
      actionTaken: false
    };

    function updateUI() {
      document.getElementById('sol-display').innerText = `${gameState.sol} / 30`;
      document.getElementById('o2-display').innerText = `${Math.round(gameState.o2)}%`;
      document.getElementById('power-display').innerText = `${Math.round(gameState.power)}%`;
      document.getElementById('water-display').innerText = `${Math.round(gameState.water)}%`;
      document.getElementById('food-display').innerText = `${Math.round(gameState.food)}%`;
    }

    window.performAction = function(type) {
      if(gameState.actionTaken) {
        document.getElementById('advisor-speech').innerText = "You've already taken an action for this Sol! Advance to next Sol.";
        return;
      }
      if(type === 'clean_solar') {
        gameState.power = Math.min(100, gameState.power + 15);
        document.getElementById('advisor-speech').innerText = "Solar panels swept! Power generation boosted for the base.";
      } else if(type === 'greenhouse') {
        gameState.food = Math.min(100, gameState.food + 15);
        document.getElementById('advisor-speech').innerText = "Hydroponic crops harvested! Crew food supplies restocked.";
      } else if(type === 'ice_extraction') {
        gameState.water = Math.min(100, gameState.water + 15);
        document.getElementById('advisor-speech').innerText = "Rover excavated subsurface ice! Water reserves increased.";
      }
      gameState.actionTaken = true;
      updateUI();
    };

    window.advanceSol = function() {
      if(gameState.sol >= 30) {
        alert("🎉 Mission Accomplished! You survived 30 Sols on Mars! You are now a Certified Junior Astronaut.");
        location.reload();
        return;
      }

      gameState.sol += 1;
      gameState.actionTaken = false;

      // Daily 4-Person Crew Baseline Resource Consumption
      gameState.o2 -= 2.5;
      gameState.water -= 3.0;
      gameState.food -= 2.8;
      gameState.power -= 2.0;

      // Random Mars Event Simulation
      const events = [
        { text: "Clear weather today! Solar arrays operating smoothly.", impact: () => {} },
        { text: "Mild dust storm! Solar power generation dropped.", impact: () => { gameState.power -= 8; } },
        { text: "Thermal regulator spike! Water cooling used extra reserves.", impact: () => { gameState.water -= 5; } }
      ];
      const ev = events[Math.floor(Math.random() * events.length)];
      ev.impact();

      document.getElementById('telemetry-box').innerHTML = `<strong>Mars Weather (Sol ${gameState.sol}):</strong><br>• Temp: ${-60 - Math.floor(Math.random() * 20)}°C<br>• Status: ${ev.text}`;
      document.getElementById('advisor-speech').innerText = `Sol ${gameState.sol} begins! Keep critical reserves above 20%.`;

      // Failure Condition Check
      if(gameState.o2 <= 0 || gameState.water <= 0 || gameState.food <= 0 || gameState.power <= 0) {
        alert("⚠️ Mission Critical Failure! Base resources were depleted. Try again, Commander!");
        location.reload();
      }

      updateUI();
    };

    // --- 3. Animation Render Loop ---
    function animate() {
      requestAnimationFrame(animate);
      dome.rotation.y += 0.001; // gentle rotation
      
      // Floating dust motion
      const positions = dustGeo.attributes.position.array;
      for(let i = 1; i < dustCount * 3; i += 3) {
        positions[i] -= 0.02;
        if(positions[i] < 0) positions[i] = 20;
      }
      dustGeo.attributes.position.needsUpdate = true;

      renderer.render(scene, camera);
    }
    animate();

    window.addEventListener('resize', () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    });
  </script>
</body>
</html>