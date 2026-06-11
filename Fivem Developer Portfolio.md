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


### **6. Hawkk Resource Suite** (`[Hawkk]/`)

**Type:** Multi-Feature Resource Collection

**Resources Include:**

- **hawkkdown_armory** - Custom gun shop with gunsmith attachment system
- **hawkkdown_housing** - Housing system with interior loading
- **hawkkdown_basketball** - Basketball mini-game with scoring
- **hawkkdown_phone** - Phone UI with apps
- **hawkkdown_redzone** - Redzone PvP system
- **hawkkdown_trap** - Trap house mechanics
- **Hawkkdown_LoadingScreen** - Custom loading screen

**Technical Highlights:**

- Complex UI integration with JavaScript
- Discord webhook integration for admin actions
- Custom NUI windows
- Database-driven systems
- Performance-optimized rendering
---

### **7. Custom Discord Bots**

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
- **GitHub:** https://github.com/futuristickg123-arch/fivem-developer-portfolio
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
