# Canton Claude

A Claude Code skill for learning Cantonese by absorption. Claude swaps a few words
and short phrases in its English answers for Cantonese written in Jyutping, with
the English gloss in brackets right after:

> `hou2 (good)`, found it. Bug in the auth middleware — token expiry uses `<` not
> `<=`. `zing2 (fix)` is one line. `si3 haa5 (give it a try)` after I push.

You are there to get work done; the Cantonese rides along inside answers you were
going to read anyway. It stays out of code, commands, commit messages, quoted
errors, security warnings and anything else that has to be read exactly right the
first time.

## Install

```bash
git clone https://github.com/WongKongPhooey/Canton-Claude.git
cd Canton-Claude
./install.sh
```

That copies the skill to `~/.claude/skills/canton-claude`, so it is available in
every repo rather than only one. Use `./install.sh --link` to symlink this clone
instead, and `git pull` will then update the installed skill in place.

Start a new Claude Code session and run `/canton-claude`, or just ask for
"Cantonese mode". Adjusting it works in plain language too — more, less, off,
show the characters, drop the brackets.

## Hearing it

`scripts/speak.sh` plays Cantonese through the machine's own speech engine, so you
can hear a word before trying to say it:

```bash
scripts/speak.sh 你好 多謝
```

Pass characters, not Jyutping — speech engines read 好 correctly and read "hou2" as
English nonsense. Each word is printed with its entry on
[words.hk](https://words.hk) (粵典), where the definitions and the recordings of
real speakers are:

```
  你好  https://words.hk/zidin/%E4%BD%A0%E5%A5%BD
  多謝  https://words.hk/zidin/%E5%A4%9A%E8%AC%9D
```

The links print before anything is spoken, so you get them even on a machine with
no Cantonese voice. Nothing is fetched over the network — the URL is the word
itself, percent-encoded.

`scripts/speak.sh --list` reports which voice is installed without speaking; when
none is, it prints that platform's setup steps and exits 3. A Cantonese (zh-HK)
voice is needed:

- **macOS** — System Settings › Accessibility › Spoken Content › System Voice ›
  Manage Voices, then Chinese (Hong Kong) – Sinji.
- **Windows** — Settings › Time & language › Language & region › Add a language ›
  Chinese (Traditional, Hong Kong SAR), and tick Speech.
- **Linux** — `sudo apt install espeak-ng`, which carries a `yue` voice. Robotic,
  approximate tones.

It deliberately refuses to fall back to a Mandarin or English voice, because those
read the same characters as completely different sounds. Synthetic Cantonese is
good enough to check you have the right tone on the right word, not good enough to
copy for rhythm or intonation — for that, follow the words.hk link, or use
Forvo.

## Your vocabulary

The skill keeps a log at `~/.claude/cantonese-vocab.md` — outside any repo, so it
follows you between projects and never lands in a commit. It tracks what you have
seen and how often, which is how the skill knows to repeat words before adding new
ones. Ask "what have I learned?" or "quiz me" to use it.

## Layout

| Path | What it is |
|---|---|
| `SKILL.md` | the skill itself — substitution rules, where Cantonese must not go |
| `references/starter-vocab.md` | verified high-frequency Hong Kong Cantonese, plus the Mandarin traps to avoid |
| `scripts/speak.sh` | cross-platform Cantonese text-to-speech |
| `install.sh` | installs the skill at user level |

## License

GPL-3.0. See [LICENSE](LICENSE).
