---
sidebar_position: 3
---

# Color Codes

Use `&` codes in the `Display` option to add colors and formatting to entity names.

## Usage

```yaml
my_entity:
  Display: '&c&lFire Demon'  # Red, bold
```

## Colors

| Code | Color | Hex |
|------|-------|-----|
| `&0` | Black | #000000 |
| `&1` | Dark Blue | #0000AA |
| `&2` | Dark Green | #00AA00 |
| `&3` | Dark Aqua | #00AAAA |
| `&4` | Dark Red | #AA0000 |
| `&5` | Dark Purple | #AA00AA |
| `&6` | Gold | #FFAA00 |
| `&7` | Gray | #AAAAAA |
| `&8` | Dark Gray | #555555 |
| `&9` | Blue | #5555FF |
| `&a` | Green | #55FF55 |
| `&b` | Aqua | #55FFFF |
| `&c` | Red | #FF5555 |
| `&d` | Light Purple | #FF55FF |
| `&e` | Yellow | #FFFF55 |
| `&f` | White | #FFFFFF |

## Formatting

| Code | Effect |
|------|--------|
| `&l` | **Bold** |
| `&o` | *Italic* |
| `&n` | <u>Underline</u> |
| `&m` | ~~Strikethrough~~ |
| `&k` | Obfuscated (random characters) |
| `&r` | Reset all formatting |

## Examples

```yaml
# Simple color
Display: '&cRed Name'

# Bold color
Display: '&c&lBold Red'

# Multiple colors
Display: '&6Gold &c&lFire &6Dragon'

# Reset in middle
Display: '&c&lBold Red &rNormal Text'

# All formatting
Display: '&5&l&oFancy Purple'
```

## Common Combinations

| Display | Result |
|---------|--------|
| `'&c&lBoss Name'` | Bold red (bosses) |
| `'&a&lFriendly'` | Bold green (friendly) |
| `'&7Common Mob'` | Gray (common) |
| `'&e&lRare Mob'` | Bold yellow (rare) |
| `'&5&lLegendary'` | Bold purple (legendary) |
| `'&b&oMystic'` | Italic aqua (magical) |

## Notes

- Always wrap Display values in quotes when using `&`
- Formatting codes (`&l`, `&o`, etc.) should come after color codes
- Use `&r` to reset all formatting mid-string
