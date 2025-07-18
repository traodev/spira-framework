# Spira

🎮 **Spira** is a lightweight, full-custom Minecraft development framework built from scratch — no external dependencies, no fluff, just raw plugin power.

This framework is ideal for Spigot developers who want **full control** over their codebase, while maintaining clean structure and reusability.

---

## ✨ Features

* ⚙️ **Modular architecture** — separate core systems: GUIs, events, utilities, etc.
* 🧱 **Dynamic GUI builder** — one class per GUI with multiple actions, intuitive API
* 🔁 **Custom event manager** — define, trigger, and listen to internal events
* 🛡️ **Built-in permissions system** — lightweight, flexible permission manager with per-player nodes, groups, and hierarchical inheritance
* 🗂️ **Flexible data backend** — choose between YAML, JSON, SQL, or NoSQL databases for permission and data storage
* 🧰 **Helper classes** — ItemBuilder, ChatUtils, TimerUtils, and more
* 🧪 **Built-in logging/debug tools** — for tracing plugin behavior

---

## 📦 Repository

**GitHub:** [github.com/traodev/spira-framework](https://github.com/traodev/spira-framework)

```
git clone https://github.com/traodev/spira-framework.git
```

---

## 🚀 Getting Started

1. Add Spira as a module in your plugin project
2. Use the framework to build clean and scalable systems

### Example: GUI System

```java
public class RewardGUI extends SpiraGUI {
    public RewardGUI(Player player) {
        super(3, "Choose your reward");

        setItem(11, new ItemBuilder(Material.DIAMOND)
                .setName("Shiny Reward")
                .addLore("Click to claim!")
                .build(),
            p -> p.sendMessage("§aYou got a diamond!"));

        setItem(15, new ItemBuilder(Material.EMERALD)
                .setName("Mystery Reward")
                .build(),
            p -> {
                p.getInventory().addItem(new ItemStack(Material.EMERALD));
                p.sendMessage("§bMystery emerald given!");
            });

        open(player);
    }
}
```

### Example: Advanced Permission System

Spira includes a permission system with support for:

* Player-specific permissions
* Group-based inheritance
* Default groups
* Wildcard and nested node support
* **Customizable backend:** YAML, JSON, SQL, or NoSQL

```java
if (!SpiraPermissions.has(player, "gui.reward.claim")) {
    player.sendMessage("§cYou don't have permission to claim this reward.");
    return;
}
```

#### Example: Configuring the Backend

```java
SpiraPermissions.setBackend(StorageType.NOSQL); // or SQL, YAML, JSON
```

Backends are hot-swappable and modular — implement your own if needed.

#### Example: YAML Permission Configuration

```yaml
users:
  27bd17c2-3a45-4c59-920e-abc123def456:
    groups:
      - default
    permissions:
      - gui.reward.claim

groups:
  default:
    permissions:
      - gui.help.*
  moderator:
    permissions:
      - gui.reward.*
      - moderation.*
```

Permissions are loaded at runtime and can be refreshed dynamically. Custom logic can override or extend the default permission resolution.

---

## 💡 Philosophy

Spira is not just a helper library. It’s a **developer-first framework**:

* Full source code control
* No reliance on external plugins (Vault, PlaceholderAPI, etc.)
* Ideal for custom servers or learning deep Spigot internals

Use Spira if you want to **understand, control, and extend** everything yourself.
