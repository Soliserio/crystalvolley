::Note:: CrystalVolley by Soliserio is now TradeVolley.  This version is still usable with Crystals only.  

# CrystalVolley 

A Windower addon that automatically trades crystals and clusters from Inventory to a nearby Ephemeral Moogle.

CrystalVolley combines different elements and item types into trades of up to eight stacks, then continues until the items included at the start have been traded or a stop condition occurs.

## Features

- Supports all eight elemental crystal and cluster types.
- Mixes crystals and clusters in the same trade.
- Uses up to eight trade slots, with twelve or fewer items per slot.
- Selects the largest eligible stacks first.
- Supports individual characters and multiple local characters.
- Confirms Inventory changes before continuing.
- Starts without an added startup delay.
- Cancels after three continuous seconds of healing/kneeling.
- Uses the short command `//cv` throughout.

## Installation

1. Extract the release ZIP.
2. Place the `CrystalVolley` folder inside your `Windower/addons` folder.
3. Load the addon on each character you want to use:

```text
//lua load CrystalVolley
```

To load it automatically on future client launches, add this line to `Windower/scripts/init.txt`:

```text
lua load CrystalVolley
```

Loading the addon does not start trading.

## Commands

### Preview Inventory

Shows eligible crystals and clusters without trading:

```text
//cv preview
```

### Start on the Current Character

```text
//cv start
```

### Start on All Local Characters

Each participating character must have CrystalVolley loaded and be near an Ephemeral Moogle:

```text
//cv start all
```

### Check Status

Shows progress for the current character:

```text
//cv status
```

### Cancel the Current Character

```text
//cv cancel
```

### Cancel All Local Characters

```text
//cv cancel all
```

### Show Help

```text
//cv
```

The full `//crystalvolley` command also works in place of `//cv`.

## How Trading Works

Stand idle within six yalms of an Ephemeral Moogle, with game menus closed.

CrystalVolley includes the crystals and clusters present in **Inventory when the run starts**. It does not retrieve items from other bags or add newly acquired items to an active run.

Each exchange uses:

- Up to eight distinct Inventory stacks.
- Up to twelve items per slot.
- Up to ninety-six physical items in total.
- Different elements, crystals, and clusters together when available.

Partial stacks use their actual quantities. The largest eligible stacks are selected first.

After submitting a batch, CrystalVolley waits for the expected Inventory decrease for every included item type. The character must then be idle with menus closed before continuing. A three-second pause separates confirmed exchanges.

Each character operates independently. Additional batches continue until the starting Inventory quantities have been traded, unless the run is cancelled or stopped.

## Cancellation

Heal/kneel continuously for **three seconds** to cancel that character’s run.

Standing before three seconds resets the kneeling timer. The cancel commands stop the run immediately.

An already-sent trade may still finish after cancellation.

## Stop Conditions

CrystalVolley stops when:

- A trade remains unconfirmed for thirty seconds.
- The Ephemeral Moogle becomes unavailable or moves out of range.
- The character changes zones or enters combat.
- Unexpected Inventory changes occur.
- Remaining items are locked or unavailable.
- The user cancels the run.

Unconfirmed trades are not automatically retried.

The Moogle’s storage limits still apply. If a trade is refused or only partly accepted, check the NPC’s response before restarting.

Confirmation tracks items removed from Inventory; it does not independently verify the Moogle’s stored balance. Avoid running another trading or inventory-moving tool at the same time.

## Recommended: Use a Hotkey

**CrystalVolley works best when started with a hotkey.**

A hotkey lets you start trading without opening an in-game macro palette or typing into chat. Keep game menus closed when starting.

**Hotkeys are not bundled, installed, or configured automatically. Users must set up their own shortcut.** All commands remain available without a hotkey.

One suggested combination is:

**Windows + C + V**

Hold Windows and C, tap V, then release the keys. Configure your chosen hotkey tool to invoke the equivalent of:

```text
//cv start all
```

Check that the combination is available in your setup and only triggers while the game is active.

### Optional External Hotkey Integration

For external tools that support file writing, CrystalVolley can receive a local request through:

```text
CrystalVolley/hotkey_request.txt
```

The file must contain:

```text
UTC Unix timestamp in seconds:unique numeric token
```

Write the complete file atomically, without a byte-order mark or extra spaces.

Loaded clients sharing that addon folder accept fresh requests up to five seconds old and display **“Hotkey received.”** Previously seen requests and requests already present when the addon loads are ignored.

Receipt logs are written per character. No external keyboard helper or personal hotkey configuration is included in the release.

## Testing

Mixed eight-slot crystal-and-cluster trades and multi-character operation have been confirmed in-game.

Offline checks cover trade limits, mixed batches, confirmation, cancellation, stale requests, and duplicate requests.

External hotkey operation has been confirmed in the author’s setup. Users must configure and verify their own shortcuts.

---

Author: Soliserio
