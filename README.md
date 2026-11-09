# Passport Control

A multiplayer flag quiz for learning the flags of every country. A flag appears with four countries to choose from. The faster you pick the right one, the more points you get.

The whole game is a single `index.html` with the flag images in `flags/`. It runs on GitHub Pages and needs no server or build step.

## How to Play

- **Host a game:** creates a room with a 4-letter code, an invite link and a QR code. The host plays too.
- **Join a game:** enter the code, or open the invite link or QR code.
- **Solo practice:** same rules, no room needed.
- **Study the flags:** browse every flag by continent, or search for a country by name.

Everyone picks a name and an emoji avatar. The language (English or Greek) is set per device, so players in the same game can use different languages.

## Game Settings

The host chooses:

- **Flags:** Standard (197 countries: the UN members, Vatican City, Palestine, Kosovo and Taiwan) or Extended (248, adding territories with their own flag and the four UK home nations).
- **Continents:** any combination of Europe, Asia, Africa, North America, South America and Oceania. Transcontinental countries such as Russia, Turkey and Egypt count under both of their continents.
- **Rounds:** 10, 20, 30 or every flag in the selection.
- **Time per flag:** 5, 10, 15 or 20 seconds.
- **Difficulty:** Easy uses random wrong answers. Hard prefers flags that look alike, such as Chad and Romania or Indonesia and Monaco.

## Scoring

- A correct answer scores 1000 points if instant, dropping to 500 at the buzzer.
- A wrong answer costs 250 points. A total never goes below 0.
- No answer scores 0.
- From the third correct answer in a row, each correct answer adds a 100-point streak bonus.

After each flag, every screen shows the correct country and the standings, then the next flag starts. The host can pause between flags. At the end, each player gets a list of the flags they missed.

## How Multiplayer Works

Players connect directly to the host's browser over WebRTC, using [PeerJS](https://peerjs.com/). The free public PeerJS server only introduces the devices to each other. The host's browser runs the game, picks the flags and keeps the score. Each device times its own answers from the moment the flag appears on its screen, so a slow connection doesn't cost points.

Things to know:

- All players need an internet connection.
- The game ends if the host closes the tab. The page asks the device to keep the screen awake during a game.
- A player who drops out (for example, a phone that locked) can rejoin with the invite link and keeps their score.
- A few strict networks, such as some school or office Wi-Fi, block this kind of connection.

All networking code is in the `Net` module in `index.html`. Replacing PeerJS with another service, such as Firebase, means reimplementing only that module.

## Running Locally

Serve the folder over HTTP and open it in a browser:

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000>. Two browser tabs can play against each other.

## Credits

- Flag images: [flagcdn.com](https://flagcdn.com), based on Wikimedia Commons.
- Country names: Unicode CLDR, with some names shortened or simplified.
- Fonts: Fira Sans, Fira Sans Extra Condensed and Fira Mono from Google Fonts.
- QR codes: [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator).
