# FiveM Developer Portfolio

## 👋 Introduction
Hello! I'm an experienced FiveM developer with a strong background in creating custom ESX-based resources. I specialize in Lua scripting, database integration, and creating immersive roleplay features.

---

## 🛠️ Technical Skills

### **Languages & Frameworks**
- **Lua** (Advanced) - Client & Server-side FiveM scripting
- **JavaScript** (Intermediate) - NUI/UI development
- **MySQL** (Intermediate) - Database design & queries
- **ESX Legacy** (Advanced) - Framework development
- **ox_target** (Advanced) - Interaction systems
- **ox_inventory** (Advanced) - Inventory integration

### **FiveM APIs & Systems**
- Native FiveM functions (GetEntityCoords, TriggerEvent, etc.)
- ESX callbacks & exports
- Database operations with oxmysql/MySQL-async
- NUI (NUI Window) development
- Custom event systems
- Performance optimization techniques

---

## 📦 Custom Resources Developed

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

### **5. GMTA SAMP Chat System** (`[chat]/gmto_samp`)
**Type:** Roleplay Chat Enhancement

**Features:**
- Comprehensive RP command system (/me, /do, /my, /say, /shout, /low, /carwhisper)
- Staff chat system with group-based permissions
- OOC chat with staff rank coloring
- Dice rolling system (1-3 dice)
- Coin flip system
- 911 emergency call system
- Help/announce commands
- Player kick functionality
- Distance-based chat ranges
- Language system support

**Technical Highlights:**
```lua
-- Group-based permission system
ESX.RegisterCommand('kick', {'mod', 'admin', 'management', 'developer'}, function(source, args, raw)
    -- Kick logic with reason support
end)

-- Distance-based chat with mask checking
maskCheck(source, message, chatType)
```

**Files:** server/sv_main.lua (3847 lines), client/cl_main.lua, config.lua, admin functions

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
- **adminplus-adminjail** - Admin jail system with Discord webhooks
- **Hawkkdown_LoadingScreen** - Custom loading screen
- **vms_notify** - Custom notification system

**Technical Highlights:**
- Complex UI integration with JavaScript
- Discord webhook integration for admin actions
- Custom NUI windows
- Database-driven systems
- Performance-optimized rendering

---

## 🏗️ Development Approach

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

## 📊 Project Statistics

- **Total Custom Resources:** 15+
- **Lines of Lua Code:** 5,000+
- **Database Tables:** 5+ custom tables
- **ESX Integration:** Full compatibility
- **ox_target Integration:** Multiple resources
- **Custom UI:** 5+ NUI interfaces

---

## 🎯 What I Can Build

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

---

## 🤝 Collaboration & Communication

- **Discord:** hawkkdown
- **GitHub:** https://github.com/futuristickg123-arch/fivem-developer-portfolio
- **Availability:** EST/8/10
- **Experience:** 3 years of FiveM development

---

## 📝 Why Choose Me?

1. **Proven Track Record** - Multiple production-ready resources
2. **Clean Code** - Maintainable and well-documented scripts
3. **Performance Focused** - Optimized for high player counts
4. **Security Conscious** - Server-side validation and anti-cheat
5. **Framework Expert** - Deep ESX Legacy knowledge
6. **Modern Stack** - ox_target, ox_inventory, lib notifications
7. **Custom UI** - JavaScript/NUI development skills
8. **Database Design** - Efficient MySQL schema design

---

## 🚀 Ready to Start

I'm available for:
- Custom resource development
- Script debugging & optimization
- Server setup & configuration
- System integration
- Code reviews & consultation

**Let's build something amazing together!** 🎮

---

*This portfolio showcases my actual FiveM development work. All scripts are original creations demonstrating my Lua programming skills and understanding of the FiveM ecosystem.*
