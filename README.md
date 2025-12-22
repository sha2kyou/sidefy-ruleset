# sidefy-ruleset

Sidefy rule sets built with SideQL, used to **filter, color, highlight, and organize events**.

This repository is meant to:
- Provide **shareable preset rules** for Sidefy users
- Showcase **SideQL best practices** and example patterns
- Serve as a **playground** for designing and iterating on rule logic

## SideQL Syntax

SideQL is a small domain-specific language for defining event rules in Sidefy.

```text
IF <condition>
  [AND|OR <condition>...]
THEN <action>
  [<action>...]
```

### Fields

| Field          | Description        |
|----------------|--------------------|
| `title`        | Event title        |
| `content`      | Event content      |
| `titleOrContent` | Title or content |
| `origin`       | Origin             |
| `source`       | Plugin / source    |

### Operators

| Operator            | Description              |
|---------------------|--------------------------|
| `EQUALS`            | Equals                   |
| `NOT_EQUALS`        | Not equals               |
| `CONTAINS`          | Contains                 |
| `NOT_CONTAINS`      | Not contains             |
| `CONTAINS_ANY`      | Contains any of list     |
| `CONTAINS_ALL`      | Contains all of list     |
| `NOT_CONTAINS_ANY`  | Does not contain any     |
| `NOT_CONTAINS_ALL`  | Does not contain all     |
| `MATCHES`           | Regex match              |
| `NOT_MATCHES`       | Regex not match          |

### Actions

| Action                     | Value Type  | Description                |
|----------------------------|------------|----------------------------|
| `SET color = "#RRGGBB"`    | String     | Set event color            |
| `SET symbol = "name"`      | String     | Set SF Symbol icon         |
| `SET PINNED`               | –          | Pin event to the top       |
| `SET HIDDEN`               | –          | Hide event                 |
| `HIGHLIGHT [...] WITH "color"` | Array + String | Highlight keywords with color |
| `REPLACE [...] WITH "text"`    | Array + String | Replace matching text content  |

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
