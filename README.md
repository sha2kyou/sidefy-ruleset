# sidefy-ruleset

Sidefy rule sets built with SideScript, used to **filter, color, highlight, and organize events**.

This repository is meant to:
- Provide **shareable preset rules** for Sidefy users
- Showcase **SideScript best practices** and example patterns
- Serve as a **playground** for designing and iterating on rule logic

## 📁 File Structure

```text
sidefy-ruleset/
  ├── README.md        # Documentation for this repository
  ├── LICENSE          # License information
  ├── info.json        # Metadata for this ruleset collection
  └── <ruleset-name>/  # Example ruleset folder (optional, one or more)
      ├── info.json    # Metadata for this ruleset
      ├── rules.sidescript # SideScript rules for this ruleset
```

### info.json (ruleset)

Each ruleset folder should contain an `info.json` file with the following structure:

```json
{
  "name": "Tax & Duty Events",
  "version": "0.1.0",
  "author": "Sidefy Team"
}
```

### rules.sidescript

Each ruleset folder should contain a `rules.sidescript` file that defines event rules using SideScript syntax. SideScript is a small domain-specific language for defining event rules in Sidefy.

`rules.sidescript` can contain one or more rules in the following format:

```text
IF <condition>
  [AND|OR <condition>...]
THEN <action>
  [<action>...];
```

### Fields

| Field    | Description                            |
| -------- | -------------------------------------- |
| `title`  | Event title                            |
| `content`| Event content                          |
| `origin` | Origin                                 |
| `source` | Plugin                                 |
| `anywhere`| Event title, content, origin or plugin |

### Operators

| Operator              | Description       |
| --------------------- | ----------------- |
| EQUALS                | Equals            |
| NOT EQUALS            | Not equals        |
| CONTAINS              | Contains          |
| NOT CONTAINS          | Not contains      |
| CONTAINS_ANY          | Contains any      |
| NOT CONTAINS_ANY      | Not contains any  |
| CONTAINS_ALL          | Contains all      |
| NOT CONTAINS_ALL      | Not contains all  |
| MATCHES_TOKEN         | Token matches     |
| NOT MATCHES_TOKEN     | Token not matches |
| MATCHES_REGEX         | Regex match       |
| NOT MATCHES_REGEX     | Regex not match   |

### Actions

| Action              | Value Type    | Description                   |
| ------------------- | ------------- | ----------------------------- |
| SET color =         | "#RRGGBB"     | Event color                   |
| SET symbol =        | "symbol.name" | SF Symbol icon                |
| SET PINNED          |               | Pin to top                    |
| SET HIDDEN          |               | Hide event                    |
| HIGHLIGHT...WITH... |               | Highlight keywords with color |
| REPLACE...WITH...   |               | Replace text content          |

Multiple `SET` properties can be combined after a single `SET` keyword, separated by commas. Both of the following forms are valid:

1. Combined `SET` properties in a single action:

```text
IF title CONTAINS_ANY ["tax", "duty"]
THEN SET color = "#7f7f7f", symbol = "dollarsign.circle.fill", PINNED
```

2. Multiple `SET` actions on separate lines:

```text
IF title CONTAINS_ANY ["tax", "duty"]
THEN SET color = "#7f7f7f"
SET symbol = "dollarsign.circle.fill"
SET PINNED
```
