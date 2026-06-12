# FiveM Developer Portfolio

## Introduction

Hello! I'm an experienced FiveM developer with a strong background in creating custom ESX-based resources. I specialize in Lua scripting, database integration, and creating immersive roleplay features.

---

## Technical Skills

### **Languages & Frameworks**

- **Lua** (Advanced) - Client & Server-side FiveM scripting
- **JavaScript & Node.js** (Advanced) - NUI/UI development & Discord bot creation
- **Discord.js & Discord APIs** (Advanced) - Custom moderation, utility, and integration bots
- **MySQL** (Intermediate) - Database design & queries
- **ESX Legacy** (Advanced) - Framework development
- **Custom UI Development** (Advanced) - HTML/CSS/JS NUI interface design and framework integration

### **FiveM & Discord APIs/Systems**

- Native FiveM functions (GetEntityCoords, TriggerEvent, etc.)
- ESX callbacks & exports
- Database operations with oxmysql/MySQL-async
- NUI (NUI Window) development
- Discord.js REST API & Gateway connections
- Webhook integrations for server events & logs
- Custom event systems
- Performance optimization techniques
---

## Custom Resources Developed

### **1. ZF Weapons System** (`[zf-resources]/zf_weapons`)

**Type:** Weapon Balance & Combat Enhancement

**Features:**

- Custom damage multipliers per weapon
- Configurable recoil system with camera manipulation
- Holster/unholster animations with smooth transitions
- Weapon wheel disabling for inventory-based systems
- Reticle hiding for tactical gameplay
- Per-weapon configuration in config.lua

**Technical Highlights:**

```lua
-- Real-time weapon damage modification
SetWeaponDamageModifier(weapon, damageMult)
-- Custom recoil with camera manipulation
SetGameplayCamRelativePitch(p + (recoil + r), 1.2)
SetGameplayCamRelativeHeading(h + (math.random(-1, 1) * 0.05), 1.0)

```

**Files:** client/main.lua (71 lines), config.lua (28 lines)

---

### **2. ZF Store Robbery System** (`[scripts]/zf_robbery_stores`)

**Type:** Criminal Activity System

**Features:**

- Complete store robbery mechanics with progress bars
- Police count requirement system
- Database-persisted cooldowns (MySQL)
- Police alert system with blip notifications
- Configurable loot tables with random amounts
- Distance-based robbery cancellation
- Server-side validation & security

**Technical Highlights:**

```lua
-- Database integration for persistent cooldowns
MySQL.query('INSERT INTO zf_robbery_stores (store_id, cooldown_end) VALUES (?, ?) ON DUPLICATE KEY UPDATE cooldown_end = ?')
-- Police alert with custom notifications
TriggerClientEvent('vms_notify:Notification', xPlayer.source, 'POLICE', message, 8000, '#ff4444', 'fa-solid fa-bell')

```

**Files:** server/main.lua (138 lines), client/main.lua (140 lines), config.lua

---

### **3. ZF House Robbery System** (`[scripts]/zf_robbery_houses`)

**Type:** Criminal Activity System

**Features:**

- House robbery system similar to stores
- Individual house cooldowns
- Police alert integration
- Configurable loot per house
- Database persistence
- Exportable API for other resources

**Technical Highlights:**

```lua
-- Export system for external resource integration
exports['zf_robbery_houses'] = {
    getHouseCooldowns = function() return houseCooldowns end,
    isHouseOnCooldown = function(houseId) return os.time() < houseCooldowns[houseId] end
}

```

**Files:** server/main.lua (138 lines), client/main.lua, config.lua

---

### **4. ZF Loot/Search System** (`[zf-resources]/zf_loot`)

**Type:** World Interaction System

**Features:**

- ox_target integration for prop interaction
- Unique entity identification for non-networked props
- Search cooldown system (10 minutes per container)
- Custom search animations with props
- Bank/dealer NPCs with cash check system
- Configurable loot tables
- Progress bar integration with lib.progressBar

**Technical Highlights:**

```lua
-- Unique ID generation for non-networked entities
local function getEntityUniqueId(entity)
    local coords = GetEntityCoords(entity)
    return string.format("loot_%.1f_%.1f_%.1f", coords.x, coords.y, coords.z)
end
-- ox_target integration
exports.ox_target:addModel(Config.Objects, {
    name = 'zf_search_loot',
    icon = 'fa-solid fa-hand-holding',
    label = 'Search Container',
    onSelect = function(data) searchContainer(data.entity, getEntityUniqueId(data.entity)) end
})

```

**Files:** client/main.lua (80 lines), server/main.lua, config.lua

---


### **5. Hawkk Resource Suite** (`[Hawkk]/`)

**Type:** Multi-Feature Resource Collection

**Resources Include:**

- **hawkk_loadingscreen** - Premium glassmorphic loading screen with synced music player and YouTube API video backgrounds
- **hawkk_trap** - Trap house drug cooking and packaging mechanics with private routing instances
- **hawkkdown_admin** - Fully optimized admin menu and server administration commands
- **hawkkdown_backpack** - Dynamic equippable backpack storage with custom props and movement speed debuffs
- **hawkkdown_carbreak** - Cinematic car break-in, window smashing, lockpicking QTE minigames, and search loot tables
- **hawkkdown_carmenu** - Glassmorphic vehicle cockpit controller with seatbelts, cruise limits, and underglow neons
- **hawkkdown_chains** - Hood-style chain snatching with custom attachments, break multipliers, and fence sell NPCs
- **hawkkdown_cornerdealing** - Fully integrated NPC drug corner dealing with pathing, police busts, price negotiations, and rival gang robberies
- **hawkkdown_dispatch** - Reliable police notification alerts, mapping blips, and call routing
- **hawkkdown_forgedcheck** - Criminal check forging system with bank teller interaction and dumpster searching
- **hawkkdown_graffiti** - Canvas drawing editor to spray custom DUI text/images onto FiveM world surfaces
- **hawkkdown_gsr** - Realistic Gunshot Residue detection, washing locations, and police GSR kits
- **hawkkdown_gunjam** - Realistic weapon jamming rates, unjamming progress anims, and skill check minigames
- **hawkkdown_keyfob** - Interactive floating keyfob widget controlling locks, engine, neons, trunk/doors, and suspension heights
- **hawkkdown_kidnapping** - Roleplay kidnapping script allowing players to zip-tie, intimidate, and stuff players/NPCs into car trunks
- **hawkkdown_lean** - Drug mixing system with disabled locomotion and glassmorphic HUD bars
- **hawkkdown_noclip** - Ultra-smooth admin flight/noclip utilities
- **hawkkdown_nocrosshair** - Lightweight crosshair remover for immersive roleplay servers
- **hawkkdown_perc** - Medical pill consumption script with custom screen filters and movement effects
- **hawkkdown_scale** - Syncable ped scale and height management system with feet/cm metrics and silhouettes

**Technical Highlights:**

- Complex UI integration with JavaScript
- Discord webhook integration for admin actions
- Custom NUI windows
- Database-driven systems
- Performance-optimized rendering
- ox_target integration for modern interactions
- ox_lib progress bars and notifications
- Modular design for easy expansion

---

### **6. Hawkkdown Chain Snatching System** (`[Hawkk]/hawkkdown_chains`)

**Type:** Hood-Style Criminal Activity System

**Features:**

- Wearable chain system with visible props attached to player
- Multiple chain tiers (Fake, Silver, Gold, Diamond, Gang chains)
- ox_target interaction to snatch chains from other players
- Success/fail chance system with modifiers (behind target, weapon, running, vehicle)
- Chain break chance during snatch attempts
- Snatch and victim reaction animations
- Cooldown system to prevent spam
- Anti-abuse checks (combat logging, safezones)
- Discord webhook logging for chain snatches
- Sell NPCs for chains with dirty money option
- Modular design for future expansion (reputation, gang systems, crafting)

**Technical Highlights:**

```lua
-- Chain prop attachment to player
AttachEntityToEntity(chainProp, playerPed, chain.bone, 
    chain.offset.x, chain.offset.y, chain.offset.z,
    chain.rotation.x, chain.rotation.y, chain.rotation.z,
    true, true, false, true, 0, true)
-- Dynamic success chance calculation
local chance = Config.Snatch.successChance
if math.abs(angle - heading) < 90 or math.abs(angle - heading) > 270 then
    chance = chance + Config.Snatch.behindBonus
end
```

**Files:** fxmanifest.lua, config.lua, client/main.lua (399 lines), server/main.lua (244 lines), html/

---

### **7. Hawkkdown GSR System** (`[Hawkk]/hawkkdown_gsr`)

**Type:** Evidence & Police Investigation System

**Features:**

- Shooting detection with weapon-based residue levels
- Different residue amounts per weapon class (pistol = medium, AR = heavy)
- Suppressor reduces residue by 30%
- Residue decay over time (5% per minute)
- Washing system with ox_target (sink, shower, ocean, water bottle)
- Different washing effectiveness (sink 40%, shower 90%, ocean 70%)
- Police GSR testing with `/testgsr [playerId]` command
- GSR test kit item requirement
- Residue levels (Light, Medium, Heavy) with thresholds
- Anti-abuse checks (combat, cuffed, dead, spam prevention)
- Server-side GSR backup decay timer
- Database persistence for GSR status

**Technical Highlights:**

```lua
-- Real-time shooting detection
if IsPedShooting(playerPed) then
    local weaponData = Config.GSR.weaponClasses[weaponName]
    local residueAmount = weaponData.amount
    if hasSuppressor then
        residueAmount = residueAmount * (1 - Config.GSR.suppressorReduction)
    end
    currentGSR = math.min(100, currentGSR + residueAmount)
end
-- ox_target washing locations
exports.ox_target:addSphereZone({
    coords = location.coords,
    radius = 1.5,
    options = {{name = 'wash_sink', icon = 'fa-solid fa-faucet', label = 'Wash Hands'}}
})
```

**Files:** fxmanifest.lua, config.lua, client/main.lua (234 lines), server/main.lua (137 lines)
---

### **8. Hawkkdown Gun Jam System** (`[Hawkk]/hawkkdown_gunjam`)

**Type:** Realistic Weapon Mechanics System

**Features:**

- Weapon-specific jam chances based on realism (pistols more reliable than cheap weapons)
- Progressive jam chance that increases with each shot fired
- Maximum jam chance cap to prevent frustration
- Unjamming mechanics with progress bar animation
- Press E or use /unjam command to fix jammed weapons
- Anti-abuse protection (vehicle, dead, cuffed, combat restrictions)
- Custom hood-style purple/black UI notifications
- Admin command /resetjam [playerid] for troubleshooting
- Server-side cleanup on player disconnect
- Optimized performance with minimal resource impact

**Technical Highlights:**

```lua
-- Progressive jam calculation
local jamChance = Config.WeaponJamChances[weaponName]
jamChance = jamChance + (shotsFired * Config.JamChance.perShotIncrease)
jamChance = math.min(jamChance, Config.JamChance.maxChance)
if math.random() < jamChance then
    isJammed = true
    DisableWeaponFire(true)
end
-- Unjamming with progress bar
if lib.progressBar({
    duration = Config.Unjamming.duration,
    label = 'Unjamming Weapon...',
    disable = {move = true, car = true, combat = true}
}) then
    isJammed = false
    DisableWeaponFire(false)
end
```

**Files:** fxmanifest.lua, config.lua, client/main.lua (180 lines), server/main.lua (25 lines)

### **9. Hawkk Loading Screen** (`[Hawkk]/hawkk_loadingscreen`)

**Type:** Dynamic Server UI Entry

**Features:**

- Top branding banner with wings logo and server community link.
- Synced background music player with YouTube API integrations.
- Member rosters with circular staff avatars and custom roles.
- Smooth FiveM load state progress events synchronization.
- Glassmorphic media control HUD (play, pause, volume sliders).

**Technical Highlights:**

```javascript
// YouTube IFrame Player integration
window.onYouTubeIframeAPIReady = function() {
    player = new YT.Player('bg-video', {
        videoId: 'tYjPXFlZlq8',
        playerVars: { 'autoplay': 1, 'controls': 0, 'mute': 0 },
        events: { 'onReady': onPlayerReady }
    });
};
```

**Files:** fxmanifest.lua, index.html, style.css, script.js

---

### **10. Hawkk Trap House System** (`[Hawkk]/hawkk_trap`)

**Type:** Private Routing & Drug Processing System

**Features:**

- Buying trap houses from an NPC dealer.
- Instanced private interior spaces (each house running its own routing bucket).
- Drug cooking and packaging minigames.
- Synced boombox audio playing YouTube/custom links inside the instance.

**Technical Highlights:**

```lua
-- Routing bucket instancing
SetPlayerRoutingBucket(playerId, trapHouseBucketId)
-- Cook drug interaction point check
if #(playerCoords - cookCoords) < 1.5 then
    startCookingMinigame()
end
```

**Files:** config.lua, client/main.lua, server/main.lua, traphouses.lua, cords.lua

---

### **11. Hawkkdown Admin Management** (`[Hawkk]/hawkkdown_admin`)

**Type:** Server Administration Utility

**Features:**

- Administrative action dashboard (spectating, player teleports).
- Real-time command executor logging and discord notifications.
- Lightweight group permissions (ESX groups integration).

**Technical Highlights:**

```lua
-- Teleport admin to target player ped
SetEntityCoords(ped, targetCoords.x, targetCoords.y, targetCoords.z, false, false, false, false)
```

**Files:** client/main.lua, server/main.lua, config.lua

---

### **12. Hawkkdown Backpack Storage** (`[Hawkk]/hawkkdown_backpack`)

**Type:** Inventory Upgrade & Player Debuff System

**Features:**

- Equippable custom props matching backpack size models.
- Slot and weight expansion modifications based on size.
- Weight-based character movement speed debuffs.

**Technical Highlights:**

```lua
-- Attach prop to ped bone (Spine bone)
AttachEntityToEntity(prop, ped, GetPedBoneIndex(ped, 24818), 
    offset.x, offset.y, offset.z, rot.x, rot.y, rot.z, 
    true, true, false, true, 2, true)
```

**Files:** client/visual.lua, client/speed.lua, client/main.lua, server/main.lua

---

### **13. Hawkkdown Cinematic Carbreak** (`[Hawkk]/hawkkdown_carbreak`)

**Type:** Advanced Vehicle Robbery System

**Features:**

- Unique lockpicking lock sequence with top-down focused cameras.
- Window smash particle effects, audio triggers, and smoke.
- Glovebox searches yielding random loot items based on configurations.
- Police notifications upon failures or alarm triggers.

**Technical Highlights:**

```lua
-- Cinematic camera interpolation looking down on vehicle
local cam = CreateCam("DEFAULT_SCRIPTED_CAMERA", true)
SetCamCoord(cam, camCoords.x, camCoords.y, camCoords.z)
PointCamAtEntity(cam, vehicle, 0.0, 0.0, 0.0, true)
RenderScriptCams(true, true, 1000, true, true)
```

**Files:** client/main.lua, server/main.lua, config.lua

---

### **14. Hawkkdown Vehicle Menu Panel** (`[Hawkk]/hawkkdown_carmenu`)

**Type:** Glassmorphic Vehicle Controller

**Features:**

- Speedometer SVG gauges and RPM bars.
- Dynamic seatbelt toggle checks (fails result in windshield ejects at high speed).
- Cruise speed locks and fine-tuning.
- Custom neon lighting controllers.

**Technical Highlights:**

```lua
-- Seatbelt ejection calculations
if speedDiff > Config.Seatbelt.EjectSpeed and not seatbeltOn then
    local ejectForce = velocity * Config.Seatbelt.EjectForce
    SetEntityVelocity(ped, ejectForce.x, ejectForce.y, ejectForce.z)
end
```

**Files:** client/seatbelt.lua, client/cruise.lua, client/neon.lua, client/hud.lua, ui/index.html, ui/style.css, ui/script.js

---

### **15. Hawkkdown Corner Dealing** (`[Hawkk]/hawkkdown_cornerdealing`)

**Type:** Dynamic Drug Distribution System

**Features:**

- Dealing sessions (`/corner`) validating drugs inventory.
- Walking and driving buyers spawning out of sight and pathing to dealer.
- Context menu options (Sell, Price Negotiation, Decline).
- Hostile gang robberies and police sweeps checking line-of-sight.

**Technical Highlights:**

```lua
-- NPC vehicle driver pathing to dealer coordinates
TaskVehicleDriveToCoord(buyerPed, vehicle, dealerCoords.x, dealerCoords.y, dealerCoords.z, 
    15.0, 0, GetHashKey(model), 786603, 2.0, true)
```

**Files:** client/main.lua, server/main.lua, config.lua

---

### **16. Hawkkdown Police Dispatch System** (`[Hawkk]/hawkkdown_dispatch`)

**Type:** Crime Reporting & Mapping Blip System

**Features:**

- Mapping GPS coordinates, blips, and route drawing for officers.
- Organized client notifications showing caller details.

**Technical Highlights:**

```lua
-- Police alert map blip creation
local blip = AddBlipForCoord(coords.x, coords.y, coords.z)
SetBlipSprite(blip, 161)
SetBlipColour(blip, 1)
```

**Files:** client/main.lua, server/main.lua, config.lua

---

### **17. Hawkkdown Forged Checks** (`[Hawkk]/hawkkdown_forgedcheck`)

**Type:** Financial Crime & Loot System

**Features:**

- Bank teller menus for check forgery cashing.
- Dumpster searching with ox_target, clean entity ID filters, and loot.

**Technical Highlights:**

```lua
-- Dumpster non-networked unique coordinates identification
local function getDumpsterId(entity)
    local c = GetEntityCoords(entity)
    return ("dumpster_%.2f_%.2f"):format(c.x, c.y)
end
```

**Files:** client/bank.lua, client/dumpster.lua, server/main.lua

---

### **18. Hawkkdown Graffiti System** (`[Hawkk]/hawkkdown_graffiti`)

**Type:** Artistic Custom Surface Spraying

**Features:**

- HTML NUI canvas editor (custom brush, eraser, clear).
- ImgBB base64 image uploading and database caching.
- Synced DUI projection textures rendering onto world surface vectors.

**Technical Highlights:**

```lua
-- DUI world projection drawing
DrawSpritePoly(coords1, coords2, coords3, coords4, 
    "graffiti_dui", textureName, 
    0.0, 0.0, 1.0, 1.0, 
    255, 255, 255, 255)
```

**Files:** client/render.lua, client/dui_manager.lua, ui/index.html, server/main.lua

---

### **19. Hawkkdown Keyfob System** (`[Hawkk]/hawkkdown_keyfob`)

**Type:** Interactive Vehicle Fob Widget

**Features:**

- Handheld keyfob widget.
- Locks/unlocks, neon underglow presets, engine startup/shutdown.
- Door and trunk/hood toggles, suspension height adjustments.
- Panic sirens alerting officers.

**Technical Highlights:**

```lua
-- Suspension height offsets adjustment
SetVehicleSuspensionHeight(vehicle, suspensionHeight)
```

**Files:** client/nui.lua, client/vehicle.lua, client/doors.lua, ui/index.html, ui/style.css, ui/script.js

---

### **20. Hawkkdown Kidnapping** (`[Hawkk]/hawkkdown_kidnapping`)

**Type:** Roleplay Hostage Management

**Features:**

- Zip-tie interactions restraining movement.
- Intimidating players/NPCs and forcing hands-up anims.
- Stuffing players into vehicle trunks.

**Technical Highlights:**

```lua
-- Attach ped inside vehicle trunk bone coordinates
AttachEntityToEntity(ped, vehicle, GetEntityBoneIndexByName(vehicle, "trunk"), 
    0.0, -1.0, 0.5, 0.0, 0.0, 0.0, 
    true, true, false, true, 2, true)
```

**Files:** client/main.lua, server/main.lua, config.lua

---

### **21. Hawkkdown Lean Mixing** (`[Hawkk]/hawkkdown_lean`)

**Type:** Drug Mixing Minigame & HUD

**Features:**

- Lean mixing progress overlays.
- Restricting speed/sprints and jumping actions.
- Dynamic screen filter corrective actions.

**Technical Highlights:**

```lua
-- Disable jumping and movement during mixing thread loop
DisableControlAction(0, 22, true) -- Jump
DisableControlAction(0, 21, true) -- Sprint
```

**Files:** client/mixing.lua, html/index.html, html/style.css, html/script.js

---

### **22. Hawkkdown Noclip Command** (`[Hawkk]/hawkkdown_noclip`)

**Type:** Administrative Fly Locomotion

**Features:**

- Vector math flying translations.
- Configurable speed steps and overlays showing positions.

**Technical Highlights:**

```lua
-- Update coordinate vectors based on camera angle vector calculations
local nextCoords = currentCoords + (direction * speed)
SetEntityCoordsNoOffset(ped, nextCoords.x, nextCoords.y, nextCoords.z, true, true, true)
```

**Files:** client/main.lua, config.lua

---

### **23. Hawkkdown Crosshair Remover** (`[Hawkk]/hawkkdown_nocrosshair`)

**Type:** Immersive HUD Modification

**Features:**

- Automatically disabling the screen reticle when aiming.

**Technical Highlights:**

```lua
-- Reticle hiding HUD component frame check
HideHudComponentThisFrame(14)
```

**Files:** client/main.lua

---

### **24. Hawkkdown Prescription Pills** (`[Hawkk]/hawkkdown_perc`)

**Type:** Consumable Effects System

**Features:**

- Screen flash filters, color corrections, and camera shakes.
- Sprint speed overrides.

**Technical Highlights:**

```lua
-- Apply screen aesthetic filter effect on consumer ped
StartScreenEffect("DrugsDrivingIn", 0, true)
```

**Files:** client/main.lua, config.lua

---

### **25. Hawkkdown Ped Scale Menu** (`[Hawkk]/hawkkdown_scale`)

**Type:** Ped Scale Synchronization

**Features:**

- Synced height adjustments with feet/cm labels.
- Live 3D silhouetted overlays.

**Technical Highlights:**

```lua
-- Synchronize ped scale transformation matrix
SetPedScale(ped, scaleValue)
```

**Files:** client/main.lua, server/main.lua, config.lua

---

### **26. Custom Discord Bots**

**Type:** Advanced Discord Integration & Automation

**Featured Bots:**

- **NMF Cleaner & Moderation Bot** - Multi-functional utility bot for community management, ticket systems, auto-moderation, and server logs.
- **Supreme Music Bot** - High-quality, low-latency music bot featuring playlist queuing, voice channel controls, and interactive dashboard support.
- **Starlight Bot** - Custom community engagement bot with leveling systems, economy games, and detailed role management.
- **FiveM Server Integrations** - Custom bots that link Discord to the FiveM MySQL database to check player playtime, retrieve live server status, sync VIP/Whitelists, and log in-game actions directly to administrative channels.

**Technical Highlights:**

- Full Discord.js API integration using Node.js
- Secure webhooks and database synchronizations (oxmysql to Bot REST requests)
- Interactive components like custom buttons, select menus, and modals
- Error handling, rate limit handling, and API caching for high availability
- Multi-guild capabilities and slash command architectures
---

## Development Approach

### **Code Quality**

- Clean, readable code with proper indentation
- Comprehensive error handling with pcall
- Modular design for easy maintenance
- Configuration files for easy customization
- Proper resource cleanup on stop

### **Performance Optimization**

- Efficient database queries with proper indexing
- Client-side distance checks to reduce server load
- Cooldown systems to prevent spam
- Thread management with Citizen.CreateThread
- Memory management with proper cleanup

### **Security Best Practices**

- Server-side validation for all critical actions
- Anti-cheat considerations in movement/combat systems
- Proper permission checks using ESX groups
- SQL injection prevention with parameterized queries
- Event validation and source verification
---

## Project Statistics

- **Total Custom Resources & Bots:** 20+
- **Lines of Lua/JS Code:** 8,000+
- **Database Tables:** 8+ custom tables
- **ESX Integration:** Full compatibility
- **Custom UI Development:** Multiple NUI interfaces
- **Custom UI / NUI:** 5+ interfaces
- **Discord Bot Implementations:** 5+ custom bots built from scratch
---

## What I Can Build

### **Criminal Systems**

- Robbery systems (stores, houses, banks, jewelry)
- Drug manufacturing & distribution
- Black market trading
- Gang territory systems
- Heist coordination

### **Legal Jobs**

- Custom job scripts
- Business management
- Economy systems
- Property ownership
- Vehicle dealerships

### **Quality of Life**

- Custom chat systems
- Inventory enhancements
- Vehicle modifications
- Housing systems
- Phone applications

### **Admin Tools**

- Admin menus
- Ban/kick systems
- Player management
- Server monitoring
- Discord integration

### **Discord & Bot Integration**

- Advanced moderation and auto-mod bots
- In-game log-to-Discord webhook dispatchers
- In-game to Discord account linking systems (role sync, whitelisting)
- Interactive web dashboards and dashboard-bot communication
- Music, economy, and ticket management bots
---

## Collaboration & Communication

- **Discord:** hawkkdown|hopeinmyhood_
- **GitHub:** https://github.com/Hawkkdown/fivem-developer-portfolio
- **Availability:** EST/8/10
- **Experience:** 3 years of FiveM development
---

## Why Choose Me?

1. **Proven Track Record** - Multiple production-ready resources

2. **Clean Code** - Maintainable and well-documented scripts

3. **Performance Focused** - Optimized for high player counts

4. **Security Conscious** - Server-side validation and anti-cheat

5. **Framework Expert** - Deep ESX Legacy knowledge

6. **Modern Stack** - Custom UI Development, ox_lib, and UI/UX styling

7. **Custom UI** - JavaScript/NUI development skills

8. **Database Design** - Efficient MySQL schema design

9. **Discord Bot Expert** - Developer of top-tier, custom Discord bots integrated with game databases

---

## Ready to Start

I'm available for:

- Custom resource development
- Script debugging & optimization
- Server setup & configuration
- System integration
- Code reviews & consultation

**Let's build something amazing together!**

---

*This portfolio showcases my actual FiveM development work. All scripts are original creations demonstrating my Lua programming skills and understanding of the FiveM ecosystem.*
