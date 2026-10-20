<div align="center">

# 💍 Sajan Sajan Teri Dulhan Tujhko Pukare Aaja
### Alka Yagnik's *Aarzoo* classic, on a 0.96" OLED the size of a postage stamp.

<img src="https://www.oledanimationmaker.com/github-readmes/SajanSajan-preview.gif" alt="Sajan Sajan Teri Dulhan Tujhko Pukare Aaja pixel-art animation playing on a 128x64 SSD1306 OLED" width="512" />

**338 hand-converted frames. One ESP32. Zero audio. Maximum feelings.**

![Arduino](https://img.shields.io/badge/Arduino-IDE-00979D?logo=arduino&logoColor=white)
![ESP32](https://img.shields.io/badge/Board-ESP32%20%2F%20ESP8266-000000?logo=espressif&logoColor=white)
![OLED](https://img.shields.io/badge/Display-SSD1306%20128x64-111827)
![Frames](https://img.shields.io/badge/Frames-338-E11D48)
![Loop](https://img.shields.io/badge/Loop-22.6s-8B5CF6)
![Library](https://img.shields.io/badge/Library-Adafruit%20SSD1306-orange)
![License](https://img.shields.io/badge/code-free%20to%20use-brightgreen)

[**⬇ Get the code**](#-60-second-start) · [**📖 Full tutorial**](https://www.oledanimationmaker.com/blog/sajan-sajan-teri-dulhan-tujhko-pukare-aaja-oled-animation-arduino-ssd1306.html) · [**🛠 Make your own**](https://www.oledanimationmaker.com/) · [**📸 Instagram**](https://www.instagram.com/oled_animator)

</div>

---

## Why this exists

**Sajan Sajan Teri Dulhan Tujhko Pukare Aaja** (साजन साजन तेरी दुल्हन तुझको पुकारे आजा) is the 1999 *Aarzoo* hit sung by **Alka Yagnik**. You know the song. Now watch it play on a screen you can hide in your fist.

A moonlit figure under a tree. A music-note flash. A couple on a balcony as blossoms fall. A mehendi close-up. All of it pixel by pixel, all of it in 1-bit, all of it looping on a **0.96" SSD1306** (128×64).

Put it on a desk. Gift it to someone in wedding season. Film it for a reel. People get it in half a second, which is the best kind of project.

> 🔇 Pictures only. The sketch has no speaker. Play the song from your phone and let the OLED do the visuals.

---

## 🎵 About the song

| Credit | Name |
|---|---|
| **Song** | Sajan Sajan Teri Dulhan Tujhko Pukare Aaja |
| **Singer** | Alka Yagnik |
| **Music** | Anu Malik |
| **Lyrics** | Anand Bakshi |
| **Film** | *Aarzoo* (1999) |
| **Starring** | Madhuri Dixit, Akshay Kumar, Saif Ali Khan |

---

## What you get

| | |
|---|---|
| 🎞 **Frames** | 338 × 128×64 mono bitmaps in `PROGMEM` (`frame0` … `frame337`) |
| ⏱ **Speed** | 67 ms per frame (~15 fps), a single number to change |
| 🔁 **Loop** | ≈ **22.6 seconds** per pass, then it starts over forever |
| 📚 **Libraries** | Adafruit SSD1306 + Adafruit GFX |
| 🔌 **I2C** | Address `0x3C` |
| 🧮 **Index** | `uint16_t`, because 338 doesn't fit in 8 bits |

---

## ⚡ 60-second start

```bash
git clone https://github.com/itzmeAshish/SajanSajan.git
```

1. Rename the folder to **`main`** (the file is `main.ino`, and Arduino IDE needs the names to match)
2. Install **Adafruit SSD1306** and **Adafruit GFX** from Library Manager
3. Select **ESP32** or a **4MB ESP8266**
4. Upload
5. Watch it play

Serial baud is **115200**. If you see `SSD1306 allocation failed`, check power, SDA/SCL, or try address `0x3D`.

---

## Requirements

| Item | Notes |
|------|--------|
| Board | **ESP32 or 4MB ESP8266** |
| OLED | 0.96" SSD1306 I2C 128×64 @ `0x3C` |
| IDE | Arduino IDE 1.8+ or 2.x |
| Wires | 4 Dupont jumpers |

> **Will it run on an Uno?** No. 338 frames × 1024 bytes = **346,112 bytes (338 KB)** of pictures alone.
> Uno has 32 KB of flash and Mega 2560 has 256 KB, so neither can hold it.
> The comment at the top of `main.ino` mentions Uno pins because that's the generator's header. Wire an ESP board.

---

## 🔌 Wiring

### ESP32 (recommended)

| OLED | Board |
|------|--------|
| VCC | **3.3V** |
| GND | GND |
| SDA | **GPIO21** |
| SCL | **GPIO22** |

```cpp
Wire.begin(21, 22);
```

### ESP8266 NodeMCU / Wemos D1 Mini

| OLED | Board | GPIO |
|------|--------|------|
| VCC | **3.3V** | — |
| GND | GND | — |
| SDA | **D2** | GPIO4 |
| SCL | **D1** | GPIO5 |

```cpp
Wire.begin(4, 5);  // only if the panel stays dark
```

Set **Tools → Flash Size** to a **4MB** scheme. A 512 KB or 1 MB profile rejects this sketch even when the chip is bigger.

---

## 🎚 Change the speed

In `loop()`:

```cpp
if (millis() - lastMs >= 67) {  // lower = faster
```

| Delay | Approx FPS | Full 338-frame pass |
|------:|-----------:|--------------------:|
| 134 ms | ~7.5 | ~45 s |
| 100 ms | 10 | 33.8 s |
| **67 ms (stock)** | **~15** | **~22.6 s** |
| 50 ms | 20 | ~16.9 s |

If a stopwatch says ~30 seconds at the stock 67 ms, the I2C bus is the real clock. After the bus starts:

```cpp
Wire.setClock(400000);
```

Leave `numFrames` at **338**, and don't change `frameIdx` to `uint8_t`. It wraps at 255 and cuts the loop short.

---

## 🛠 Make your own in 5 steps

This was built with the free [OLED Animation Maker](https://www.oledanimationmaker.com/). No install, no signup.

1. Open [oledanimationmaker.com](https://www.oledanimationmaker.com/)
2. Import a short clip you have the right to convert
3. Keep 128×64 and a frame count your board can store
4. Click **Get the Code** → Adafruit SSD1306
5. Paste into the IDE and upload

Long version, with wiring, flash math and filming tips:
https://www.oledanimationmaker.com/blog/sajan-sajan-teri-dulhan-tujhko-pukare-aaja-oled-animation-arduino-ssd1306.html

---

## 🧯 Troubleshooting

| Problem | Fix |
|---------|-----|
| IDE says the sketch name doesn't match | Rename the folder to `main` |
| Sketch too big | ESP32 or 4MB ESP8266. Uno and Mega won't link |
| Blank screen | 3.3V, reseat SDA/SCL, try `0x3D` |
| Loop jumps back early | `frameIdx` must stay `uint16_t` |
| Slower than 15 fps | `Wire.setClock(400000)` |
| Compile errors | Install both Adafruit libraries |

Blank-screen checklist: [oledanimationmaker.com/blog/arduino-oled-blank-screen-fix-ssd1306.html](https://www.oledanimationmaker.com/blog/arduino-oled-blank-screen-fix-ssd1306.html)

---

## 🎬 Film it so the reel works

- Fill the frame with the **glass**, not the whole desk
- Kill the light behind the phone or the cover glass mirrors the room
- Record **at least 30 seconds** so one full pass completes
- Play the song from your phone and film both. The OLED stays silent

---

## 🔥 More OLED loops

| Project | Frames | Guide |
|---------|-------:|-------|
| [🦇 Batman x Sajan Sajan](https://github.com/itzmeAshish/SajanSajanBatmanVersion) | 768 | [Blog](https://www.oledanimationmaker.com/blog/sajan-sajan-batman-edit-oled-animation-esp8266-ssd1306.html) |
| [Navratri Garba & Dandiya](https://github.com/itzmeAshish/NavratriGarba) | 390 | [Blog](https://www.oledanimationmaker.com/blog/navratri-garba-dandiya-oled-animation-arduino-ssd1306.html) |
| [Bad Apple](https://github.com/itzmeAshish/BadApple) | 385 | [Blog](https://www.oledanimationmaker.com/blog/bad-apple-oled-animation-arduino-ssd1306.html) |
| [Kalayani](https://github.com/itzmeAshish/kalayanionoled) | 148 | [Blog](https://www.oledanimationmaker.com/blog/kalayani-song-oled-animation-arduino-ssd1306.html) |
| [Khayalon Ki Duniya](https://github.com/itzmeAshish/khayalokiduniya) | 124 | [Blog](https://www.oledanimationmaker.com/blog/khayalon-ki-duniya-oled-animation-arduino-ssd1306.html) |
| [Ganesha Day 7](https://github.com/itzmeAshish/GaneshaDay7) | 150 | [Blog](https://www.oledanimationmaker.com/blog/ganesha-day-7-oled-animation-arduino-ssd1306.html) |

---

## ⭐ Liked it?

- **Star the repo.** It's how the next maker finds it
- **Tag [@oled_animator](https://www.instagram.com/oled_animator)** when you build yours, so the next maker can see it
- **Send it to the friend** who'd lose their mind seeing this on a tiny screen

---

## 🔗 Links

- **Code:** https://github.com/itzmeAshish/SajanSajan
- **Tutorial:** https://www.oledanimationmaker.com/blog/sajan-sajan-teri-dulhan-tujhko-pukare-aaja-oled-animation-arduino-ssd1306.html
- **Tool:** https://www.oledanimationmaker.com/
- **Author:** [itzmeAshish](https://github.com/itzmeAshish)
- **Instagram:** [oled_animator](https://www.instagram.com/oled_animator)
- **YouTube:** [@oled_animator](https://www.youtube.com/@oled_animator)

---

## 🔎 Keywords

`sajan sajan teri dulhan oled` · `alka yagnik oled animation` · `aarzoo song arduino` · `anu malik song oled` · `hindi song oled` · `bollywood oled animation` · `esp32 oled animation` · `esp8266 ssd1306` · `progmem bitmap` · `338 frames` · `0.96 oled` · `adafruit ssd1306`

---

## License

Free to use for learning, demos, gifts and personal projects.
Credit: link this repo and [oledanimationmaker.com](https://www.oledanimationmaker.com/).

This is a visual fan tribute. The song belongs to its original artists (Alka Yagnik, Anu Malik, Anand Bakshi) and the film's music label. Nothing in this repo contains the song's audio or lyrics as text.

<div align="center">

**May your I2C address be 0x3C. 💍**

</div>

<!--
GitHub repo settings to paste:
Description: 💍 Sajan Sajan Teri Dulhan Tujhko Pukare Aaja (Alka Yagnik, Aarzoo) as a 338-frame pixel-art loop on a 0.96" SSD1306 OLED. ESP32 / ESP8266. Free code.
Topics: arduino, esp32, esp8266, oled, ssd1306, oled-animation, pixel-art, progmem, adafruit-gfx, hindi-song, bollywood, alka-yagnik, aarzoo, maker, diy, arduino-project
-->
