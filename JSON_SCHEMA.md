# The Ultimate Archipelago Index - JSON Documentation

This document outlines the required directory structure, schema, and all possible values for creating JSON files to populate The Ultimate Archipelago Index.

---

## 1. The Registry File: `games/_list.json`

This file acts as an index for the website to know which individual JSON files to load.

- **Format**: A JSON array of strings.
- **Rule**: Each string must exactly match the filename of a valid JSON file located in the `games/` directory.

**Example:**

```json
["game_1.json", "game_2.json", "tool_1.json", "tool_2.json"]
```

---

## 2. Game/Tool Entry Schema

Each file listed in `_list.json` must be a valid JSON object following this schema.

### Root Fields

| Field          | Type    | Required | Description                                                                                                      | Possible Values                                                                |
| -------------- | ------- | -------- | ---------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| name           | String  | Yes      | The display name of the game or tool.                                                                            | Any string (e.g., "Minecraft", "YAML Generator")                               |
| type           | String  | Yes      | The category of the entry. Determines which filter tab it appears under.                                         | "Game", "Tool"                                                                 |
| implementation | String  | No\*     | The implementation type. \*Highly recommended if `type` is "Game" to display the correct badge.                  | "Core", "Custom", "Manual"                                                     |
| afterDark      | Boolean | No       | Indicates whether the game contains 18+ or mature content. Only applicable and filterable when `type` is "Game". | `true`, `false` (defaults to `false` if omitted)                               |
| logo           | String  | No       | A URL pointing to the game/tool's logo or icon (square aspect ratio recommended).                                | Any valid image URL. Falls back to a default placeholder if omitted or broken. |
| links          | Object  | No       | An object containing various useful URLs related to the entry.                                                   | See Links Object below                                                         |

---

### Links Object Fields

The `links` object can contain any combination of the following fields. If a field is omitted, its corresponding button will simply not be rendered on the UI card.

| Field         | Type   | Required | Description                                                                                         |
| ------------- | ------ | -------- | --------------------------------------------------------------------------------------------------- |
| `support`     | String | No       | URL to a support Discord thread or server.                                                          |
| `setupGuide`  | String | No       | URL to a setup guide page.                                                                          |
| `information` | String | No       | URL to additional information or documentation.                                                     |
| `apworld`     | Object | No       | Latest release of an Archipelago world package. See _Resource Object_ below.                        |
| `mod`         | Object | No       | Latest release of a game mod. See _Resource Object_ below.                                          |
| `trackers`    | Array  | No       | A list of trackers. _Note: A maximum of 5 trackers will be displayed._ See _Resource Object_ below. |

---

### Resource Object Schema (`apworld`, `mod`, or `trackers` items)

Objects used for `apworld`, `mod`, or individual items within the `trackers` array follow this strict structure:

| Field     | Type   | Required | Description                                                              |
| --------- | ------ | -------- | ------------------------------------------------------------------------ |
| `url`     | String | **Yes**  | The download or destination URL for the resource.                        |
| `version` | String | No       | A string to display next to the button label (e.g., `"Beta"`, `"Fork"`). |

> **Tip:** You can omit any `links` sub-field entirely if it does not apply to your game/tool. The renderer safely handles missing keys.
