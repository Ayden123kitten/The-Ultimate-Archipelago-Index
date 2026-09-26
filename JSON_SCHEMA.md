````markdown
# The Ultimate Archipelago Index - JSON Documentation

This document outlines the required directory structure, schema, and all possible values for creating JSON files to populate The Ultimate Archipelago Index.

## 📁 Directory Structure

The website expects a specific folder layout to fetch and render data correctly:

```text
/
├── index.html
├── icon.png
└── games/
    ├── _list.json          # Registry of all game/tool JSON files
    ├── my_favorite_game.json
    └── useful_tool.json
```
````

---

## 1. The Registry File: `games/_list.json`

This file acts as an index for the website to know which individual JSON files to load.

- **Format**: A JSON array of strings.
- **Rule**: Each string must exactly match the filename of a valid JSON file located in the `games/` directory.

**Example:**

```json
["my_favorite_game.json", "useful_tool.json"]
```

---

## 2. Game/Tool Entry Schema

Each file listed in `_list.json` must be a valid JSON object following this schema.

### Root Fields

| Field            | Type   | Required | Description                                                                                         | Possible Values                                                                |
| ---------------- | ------ | -------- | --------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| `name`           | String | **Yes**  | The display name of the game or tool.                                                               | Any string (e.g., `"Minecraft"`, `"YAML Generator"`)                           |
| `type`           | String | **Yes**  | The category of the entry. Determines which filter tab it appears under.                            | `"Game"`, `"Tool"`                                                             |
| `implementation` | String | No\*     | The implementation type. _\*Highly recommended if `type` is `"Game"` to display the correct badge._ | `"Core"`, `"Custom"`, `"Manual"`                                               |
| `logo`           | String | No       | A URL pointing to the game/tool's logo or icon (square aspect ratio recommended).                   | Any valid image URL. Falls back to a default placeholder if omitted or broken. |
| `links`          | Object | No       | An object containing various useful URLs related to the entry.                                      | See _Links Object_ below                                                       |

---

### Links Object Fields

The `links` object can contain any combination of the following fields. If a field is omitted, its corresponding button will simply not be rendered on the UI card.

| Field         | Type   | Required | Description                                                                                                  |
| ------------- | ------ | -------- | ------------------------------------------------------------------------------------------------------------ |
| `support`     | String | No       | URL to a support Discord server, forum, or help page.                                                        |
| `setupGuide`  | String | No       | URL to a setup guide, tutorial, or wiki page.                                                                |
| `information` | String | No       | URL to additional information, readme, or documentation.                                                     |
| `apworld`     | Object | No       | Details for an Archipelago world package. See _Resource Object_ below.                                       |
| `mod`         | Object | No       | Details for a game mod. See _Resource Object_ below.                                                         |
| `trackers`    | Array  | No       | An array of tracker objects. _Note: A maximum of 5 trackers will be displayed._ See _Resource Object_ below. |

---

### Resource Object Schema (`apworld`, `mod`, or `trackers` items)

Objects used for `apworld`, `mod`, or individual items within the `trackers` array follow this strict structure:

| Field     | Type   | Required | Description                                                                                 |
| --------- | ------ | -------- | ------------------------------------------------------------------------------------------- |
| `url`     | String | **Yes**  | The download or destination URL for the resource.                                           |
| `version` | String | No       | A version string to display elegantly next to the button label (e.g., `"v1.2.3"`, `"1.0"`). |

> **Tip:** You can omit any `links` sub-field entirely if it does not apply to your game/tool. The renderer safely handles missing keys.

```

```
