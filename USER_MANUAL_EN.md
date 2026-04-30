# My Golf League User Manual (English)

## 1. App Overview
My Golf League is a mobile app for managing golf tournaments by year, entering monthly scores, and checking rankings.

## 2. Main Functions
- Create and manage tournaments
- Add and edit players
- Enter monthly scores
- View rankings in Gross and Net mode

## 3. Caution
- The app stores tournament data as files on your phone.
- If you delete the app, all saved data is permanently removed.

## 4. Screen Guide

### 4.1 Home Screen
- Tap `+ New` to create a tournament.
- Existing tournaments are shown as cards.

<img src="SampleData/phone/phone1.png" alt="Home screen" width="280" />

<img src="SampleData/phone/phone4.png" alt="Tournament list" width="280" />

### 4.2 Create Tournament
- Enter `Tournament Name` and `Year`.
- Tap `New Tournament` to start with an empty player list.
- Tap `Import Players` to copy players from the previous year if available.

<img src="SampleData/phone/phone2.png" alt="Create tournament" width="280" />

### 4.3 Player Management
- Tap `Add Player` to add a new player.
- Enter player name, group, and previous handicap/average.
- Use `Edit` on a player card to update player information.

<img src="SampleData/phone/phone3.png" alt="Add player popup" width="280" />

<img src="SampleData/phone/phone5.png" alt="Player list and edit" width="280" />

### 4.4 Score Entry
- Select a month.
- Enter each player's score.
- Tap `Save Scores`.

<img src="SampleData/phone/phone6.png" alt="Score entry" width="280" />

### 4.5 Rankings
- Select month and mode (`Gross` or `Net`).
- `Gross`: lower score is better.
- `Net`: compares gross score against reference average.

<img src="SampleData/phone/phone7.png" alt="Rankings screen" width="280" />

## 5. Typical Workflow
1. Create a tournament from the home screen.
2. Add players in `Player Info`.
3. Open `Score Entry` and save monthly scores.
4. Open `Rankings` to review results.

## 6. Notes
- Tournament data is stored as JSON files in app local storage.
- Empty score input removes that month's score for the player.
- Net ranking for players without a valid reference can be excluded depending on month/data.

## 7. How Reference Handicap Average Is Calculated (Detailed)
In Net mode, the app uses a dynamic reference average (`Ref Avg`) for each player.

### 7.1 Formula
`RefAvg(month) = (LastYearAverage + Sum of prior played month scores) / (number of prior played months + 1)`

`Net = GrossScore - RefAvg`

### 7.2 Step-by-step example
- Last year average: `84.6`
- April score (first entered month): `85.0`
- May score: `82.0`

For April:
- Prior played months: none
- `RefAvg = (84.6 + 0) / (0 + 1) = 84.6`
- `Net = 85.0 - 84.6 = +0.4`

For May:
- Prior played month scores: April `85.0`
- `RefAvg = (84.6 + 85.0) / (1 + 1) = 84.8`
- `Net = 82.0 - 84.8 = -2.8`

### 7.3 New player rule
- If a player has no `LastYearAverage` and is in their first entered month, `Ref Avg` cannot be calculated.
- In this case, the player can be excluded from Net ranking for that month.
