# CreeperLauncher 🟩

A custom Minecraft launcher for cracked / offline play, built with CreeperAuth support so you can actually show your skin and connect to online servers without a Mojang account. No bullshit, no subscriptions, just Minecraft.

> **Download the latest release →** [Releases page](../../releases/latest)

---

## What even is this?

Basically I got tired of using sketchy TLauncher so I built my own. It's a WPF desktop app for Windows that lets you:

- Launch any version of Minecraft (1.5 all the way up to 1.21+)
- Log in with **CreeperAuth** — a custom auth system I made so you can actually authenticate on servers without a paid Mojang account
- Manage multiple accounts (offline and CreeperAuth)
- Handle mods, resource packs, and saves all per-account so nothing clashes
- Upload and switch between multiple skins with a proper wardrobe system
- See your skin in a 3D viewer on the website

It's not trying to be the next big launcher. It's a personal project that grew into something usable, so I'm sharing it.

---

## Features

**Launching**
- Downloads and launches any Minecraft version automatically
- Installs Fabric mod loader with one click
- Auto-detects your Java installation and picks the right version for whichever Minecraft version you're launching
- Per-account game directories — each account has its own saves, screenshots, options, etc. so nothing overwrites anything
- Configurable RAM, resolution, and fullscreen

**Accounts**
- Offline accounts for singleplayer and LAN (no auth needed)
- CreeperAuth accounts for online cracked server play with real skin support
- Multiple accounts, switch between them easily
- Each account shows its type (Offline / CreeperAuth) with a colour-coded badge

**Mods**
- Shared mods folder — add mods once, they apply to all profiles automatically
- Enable/disable mods without deleting them (disabled mods go to a separate folder)
- Syncs mods into the per-profile directory before each launch so Minecraft actually finds them under `--gameDir`
- Open the mods folder directly from the launcher

**Skins**
- Upload custom 64×64 PNG skins
- Skin wardrobe — save multiple skins, name them, and switch between them with one click
- Classic (Steve) and Slim (Alex) arm model support
- 3D rotating skin viewer on the CreeperAuth website

**Other**
- Crash detection — reads the game log after exit and shows you what went wrong in plain English
- Resource pack manager
- Version browser with search
- Settings: Java path, RAM allocation, screen size, fullscreen toggle

---

## Download & Install

1. Go to the [Releases page](../../releases/latest)
2. Download `CreeperLauncher.exe`
3. Run it — no installer, no setup wizard, it just opens

All game files go into `%AppData%\MCLauncher\` automatically.

**Requirements:**
- Windows 10 or Windows 11 (64-bit)
- [.NET 6.0 Runtime](https://dotnet.microsoft.com/download/dotnet/6.0) or higher — if you don't have it, Windows will prompt you with a link
- Java 17 or Java 21 for playing Minecraft (the launcher will detect it automatically, or you can set the path manually in Settings)

> ⚠️ **Windows SmartScreen warning** — you'll probably see "Windows protected your PC" the first time you run it. This is because the exe isn't signed with a paid code-signing certificate. Click **More info** → **Run anyway**. The source code is all here if you want to check it.

---

## CreeperAuth — what is it and do I need it?

CreeperAuth is a custom Minecraft authentication server I built to go with this launcher. It's what lets you have a persistent username and UUID, show your skin to other players, and connect to cracked servers that have authentication set up.

**You don't need it for singleplayer or LAN.** Just make an offline account and you're good.

If you want the full online experience with skins and auth:

1. Register at [creeperauth.netlify.app](https://creeperauth.netlify.app) — pick a username, upload a skin if you want
2. In the launcher, go to the **Accounts** tab → **CreeperAuth** tab
3. Paste in the auth URL: `https://creeperauth.cyberlifegamingyt15.workers.dev`
4. Enter your CreeperAuth username and password
5. Hit **Sign In**

Your account will appear in the accounts list with a green CreeperAuth badge. Select it, hit Launch.

---

## Getting skins to work in multiplayer

This needs two mods. Download them and drop them in the launcher's Mods tab:

| Mod | Why you need it |
|-----|----------------|
| [CustomSkinLoader](https://modrinth.com/mod/customskinloader) | Loads your skin from CreeperAuth and shows it to other players. Without this everyone looks like default Steve. |
| [OfflineSkins](https://modrinth.com/mod/offlineskins) | Shows other players' skins when you're on a cracked server. Without it, other people look like Steve to you. |
| [Fabric API](https://modrinth.com/mod/fabric-api) | Required by both of the above. |

Get the **Fabric 1.21.1** versions of all three. Drop them in the launcher's Mods tab and they'll sync automatically every time you launch.

The launcher also writes a `CustomSkinLoader/Config.json` file to your profile directory automatically when you launch with a CreeperAuth account, so the mod knows where to fetch skins from. You don't need to configure it manually.

> ⚠️ **Use Java 17 or Java 21.** Java 26 crashes with Fabric mods due to bytecode changes introduced in newer Java versions. If the game crashes immediately on launch, this is almost always the reason. Set the correct Java path in the launcher's Settings tab.

---

## Where does it store stuff?

```
%AppData%\MCLauncher\
  accounts.json              ← saved accounts (including CreeperAuth tokens)
  settings.json              ← launcher config (RAM, Java path, etc.)
  mods\                      ← shared mods folder — manage from the launcher
  mods\disabled\             ← disabled mods park here out of Minecraft's reach
  profiles\
    {account-id}\            ← one folder per account
      saves\                 ← that account's worlds
      mods\                  ← synced from shared mods on each launch
      screenshots\
      options.txt
      CustomSkinLoader\      ← skin config auto-written by launcher
        Config.json
        LocalSkin\skins\     ← active skin PNG copied here for OfflineSkins mod
```

Minecraft itself installs into the normal `.minecraft` directory as always.

---

## Known issues

- **Windows only.** It's WPF so Linux and Mac aren't an option without a full rewrite.
- **Java 26 breaks Fabric mods.** Use Java 17 or 21. This is the most common cause of crashes.
- **Can't join paid/official online-mode servers.** CreeperAuth is not Mojang. Servers running `online-mode=true` without authlib-injector will reject you. Look for cracked servers (they'll say `online-mode=false`) or run your own.
- **Skins require CustomSkinLoader on both sides.** If the other player doesn't have it installed they won't see your skin, and you won't see theirs.

---

## The CreeperAuth website

The website for account management, skin uploads, the public player gallery, and docs is at [creeperauth.netlify.app](https://creeperauth.netlify.app). The [docs page](https://creeperauth.netlify.app/docs.html) has everything about setup, mod downloads, and troubleshooting.

If you want to run your own private CreeperAuth instance (for a friend group, a server community, etc.) the docs explain how to set up your own Cloudflare Worker + Firebase backend from scratch for free.

---

*Started as a way to learn WPF, turned into something I actually use daily. If it works for you too, that's great.*
