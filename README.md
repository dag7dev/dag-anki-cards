# dag-anki-cards
This repository contains Anki cards in markdown format. The cards are organized in decks, one deck for each `.md` file. Each deck contains cards for a specific topic.

All cards are in English, except where otherwise specified.

## Disclaimer
All cards are derivative works of:
- my notes
- papers
- websites
- public documents (e.g. Google Docs, pdf...) that I have access to

The cards are provided as-is, without any warranty. Me and the original authors of the documents from which I took the cards are not responsible for any damage caused by the cards or any improper use of the cards. We are not liable in case you fail to learn anything because you relied on these cards, or in case of misinterpretation of the cards, or in case of any other problem. **Use at your own risk.**
Do not use these cards if you don't agree with the above.

## Content
- `Biometrics.md`: cards about biometric systems (e.g. fingerprint, iris, face recognition)
  - They are in Italian
- `Distributed Systems.md`: cards about distributed systems (e.g. paxos, consensus, fault tolerance...)
- `Blockchain.md`: cards about blockchain (e.g. bitcoin, ethereum, smart contracts...)
  - Missing arguments
    - Algorand: I won't add them. Sorry. Feel free to add them yourself.
    - Rug Pull - Defi and Dex: they're already covered by distributed systems cards
    - IPFS: that seminar was about IPFS cryptography, that is veery very long and complex.

Feel free to add the cards you need or modify the existing ones.

## How to use (for Anki users)
1. Download the [Anki desktop app](https://apps.ankiweb.net/).
2. Clone this repository.
3. Import the `.apkg` files in the `decks` folder in Anki.
4. Done! You should now have all the cards in your Anki decks.

NOTE: for now, apkg files are not updated automatically. See last commit date. If you want to update them, you have to do it manually (see below).

## How to use (for Obsidian and Anki users)
1. Download the [Anki desktop app](https://apps.ankiweb.net/).
2. Download the [AnkiConnect](https://ankiweb.net/shared/info/2055492159) plugin.
3. Clone this repository.
4. Download [Obsidian](https://obsidian.md/) and open the Obsidian vault in this repository.
5. Download the [Obsidian_to_Anki](https://github.com/Pseudonium/Obsidian_to_Anki/) plugin and the follow the instructions.
6. Create decks in Anki for each of the `.md` files in this repository. Each deck should have the same name as the `.md` file (TBH, see each markdown file for the name of the deck).
7. Click on the button in the left sidebar with the "Anki" icon and follow the instructions.
8. Done! You should now have all the cards in your Anki decks.

## How to contribute
1. Fork this repository.
2. Edit or add cards in the `.md` files.
3. Create a pull request.
4. Done! I'll review your changes and merge them if they're good.

Do not commit markdown files with `<!-- -->` comments. They're used by the Obsidian_to_Anki plugin to generate the `.apkg` files. Not removing them will result in the cards not being updated.

If you need it, use this regex to remove them: `<!--[\s\S]*?-->` and after you're done, undo the changes to the `.md` files so you won't lose the progress you made on Anki.

## Credits
- The awesome people who wrote the original documents from which I took the cards. Thank you! :heart:
- My personal notes
- [Obsidian](https://obsidian.md/) and [Anki](https://apps.ankiweb.net/) for being awesome
- [Pseudonium](https://github.com/Pseudonium) for the Obsidian_to_Anki plugin 

