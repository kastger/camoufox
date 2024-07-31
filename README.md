<img src="https://i.imgur.com/8nXwzrW.png" align="center">

<h1 align="center">Camoufox</h1>

<h4 align="center">A stealthy, minimalistic, custom build of Firefox for web scraping 🦊</h4>

<p align="center">                                      
Camoufox aims to be a minimalistic browser for robust fingerprint injection & anti-bot evasion.
    
</p>

---

> [!WARNING]
> Camoufox is still under active development! Built releases aren't yet avaliable for production.

## Features

- Fingerprint injection (override properties of `navigator`, `window`, `screen`, etc) ✅
- Patches to avoid webdriver detection ✅
- Font spoofing ✅
- Full integration of Playwright's Juggler ✅
- Patches from LibreWolf & Ghostery to remove Mozilla services ✅
- Optimized for memory and speed ✅
- Stays up to date with the latest Firefox version ⌚

#### What's planned?

- Built in TLS fingerprinting protection using [Hazetunnel](https://github.com/daijro/hazetunnel)
- Automatic font renderer rotation on Linux (fontconfig) and Windows (DirectWrite/GDI)
- Create integration tests
- Chromium port (long-term)

<hr width=50>

## Fingerprint Injection

Camoufox overrides Javascript properties on the lowest level possible, allowing values to be spoofed across all scopes.

To spoof fingerprint properties, pass a JSON containing properties to spoof to the `CAMOU_CONFIG` environment variable:

```bash
$ ./launch --config '{"property": "value"}' [...other Firefox arguments]
```

The following attributes can be spoofed:

<details>
<summary>
Navigator 
</summary>

Navigator (the most important attributes) can be fully spoof other Firefox fingerprints, and it is **completely safe**! However, there are some issues when spoofing Chrome (leaks noted).

| Property                       | Notes |
| ------------------------------ | ----- |
| navigator.userAgent            | ✅    |
| navigator.userAgentData        | ✅    |
| navigator.doNotTrack           | ✅    |
| navigator.appCodeName          | ✅    |
| navigator.appName              | ✅    |
| navigator.appVersion           | ✅    |
| navigator.oscpu                | ✅    |
| navigator.language             | ✅    |
| navigator.languages            | ✅    |
| navigator.platform             | ✅    |
| navigator.deviceMemory         | ✅    |
| navigator.hardwareConcurrency  | ✅    |
| navigator.product              | ✅    |
| navigator.productSub           | ✅    |
| navigator.maxTouchPoints       | ✅    |
| navigator.cookieEnabled        | ✅    |
| navigator.globalPrivacyControl | ✅    |
| navigator.appVersion           | ✅    |
| navigator.buildID              | ✅    |
| navigator.doNotTrack           | ✅    |

**Notes**:

- **navigator.webdriver** is set to false at all times.
- When spoofing Chrome fingerprints, the following may leak:
  - navigator.userAgentData missing.
  - navigator.deviceMemory missing.

</details>

<details>
<summary>
Fonts
</summary>

Fonts can be passed to be used in Camoufox through the `fonts` config property.

By default, Camoufox is bundled with the default Windows 11 22H2 fonts, macOS Sonma fonts, and Linux fonts used in the TOR bundle. Camoufox will automatically pass in the default fonts associated your spoofed User-Agent:

**Mac OS** fonts (from macOS Sonma):

```
[".Al Bayan PUA", ".Al Nile PUA", ".Al Tarikh PUA", ".Apple Color Emoji UI", ".Apple SD Gothic NeoI", ".Aqua Kana", ".Aqua Kana Bold", ".Aqua \u304b\u306a", ".Aqua \u304b\u306a \u30dc\u30fc\u30eb\u30c9", ".Arial Hebrew Desk Interface", ".Baghdad PUA", ".Beirut PUA", ".Damascus PUA", ".DecoType Naskh PUA", ".Diwan Kufi PUA", ".Farah PUA", ".Geeza Pro Interface", ".Geeza Pro PUA", ".Helvetica LT MM", ".Hiragino Kaku Gothic Interface", ".Hiragino Sans GB Interface", ".Keyboard", ".KufiStandardGK PUA", ".LastResort", ".Lucida Grande UI", ".Muna PUA", ".Nadeem PUA", ".New York", ".Noto Nastaliq Urdu UI", ".PingFang HK", ".PingFang SC", ".PingFang TC", ".SF Arabic", ".SF Arabic Rounded", ".SF Compact", ".SF Compact Rounded", ".SF NS", ".SF NS Mono", ".SF NS Rounded", ".Sana PUA", ".Savoye LET CC.", ".ThonburiUI", ".ThonburiUIWatch", ".\u82f9\u65b9-\u6e2f", ".\u82f9\u65b9-\u7b80", ".\u82f9\u65b9-\u7e41", ".\u860b\u65b9-\u6e2f", ".\u860b\u65b9-\u7c21", ".\u860b\u65b9-\u7e41", "Academy Engraved LET", "Al Bayan", "Al Nile", "Al Tarikh", "American Typewriter", "Andale Mono", "Apple Braille", "Apple Chancery", "Apple Color Emoji", "Apple SD Gothic Neo", "Apple SD \uc0b0\ub3cc\uace0\ub515 Neo", "Apple Symbols", "AppleGothic", "AppleMyungjo", "Arial", "Arial Black", "Arial Hebrew", "Arial Hebrew Scholar", "Arial Narrow", "Arial Rounded MT Bold", "Arial Unicode MS", "Athelas", "Avenir", "Avenir Black", "Avenir Black Oblique", "Avenir Book", "Avenir Heavy", "Avenir Light", "Avenir Medium", "Avenir Next", "Avenir Next Condensed", "Avenir Next Condensed Demi Bold", "Avenir Next Condensed Heavy", "Avenir Next Condensed Medium", "Avenir Next Condensed Ultra Light", "Avenir Next Demi Bold", "Avenir Next Heavy", "Avenir Next Medium", "Avenir Next Ultra Light", "Ayuthaya", "Baghdad", "Bangla MN", "Bangla Sangam MN", "Baskerville", "Beirut", "Big Caslon", "Bodoni 72", "Bodoni 72 Oldstyle", "Bodoni 72 Smallcaps", "Bodoni Ornaments", "Bradley Hand", "Brush Script MT", "Chalkboard", "Chalkboard SE", "Chalkduster", "Charter", "Charter Black", "Cochin", "Comic Sans MS", "Copperplate", "Corsiva Hebrew", "Courier", "Courier New", "Czcionka systemowa", "DIN Alternate", "DIN Condensed", "Damascus", "DecoType Naskh", "Devanagari MT", "Devanagari Sangam MN", "Didot", "Diwan Kufi", "Diwan Thuluth", "Euphemia UCAS", "Farah", "Farisi", "Font Sistem", "Font de sistem", "Font di sistema", "Font sustava", "Fonte do Sistema", "Futura", "GB18030 Bitmap", "Galvji", "Geeza Pro", "Geneva", "Georgia", "Gill Sans", "Grantha Sangam MN", "Gujarati MT", "Gujarati Sangam MN", "Gurmukhi MN", "Gurmukhi MT", "Gurmukhi Sangam MN", "Heiti SC", "Heiti TC", "Heiti-\uac04\uccb4", "Heiti-\ubc88\uccb4", "Helvetica", "Helvetica Neue", "Herculanum", "Hiragino Kaku Gothic Pro", "Hiragino Kaku Gothic Pro W3", "Hiragino Kaku Gothic Pro W6", "Hiragino Kaku Gothic ProN", "Hiragino Kaku Gothic ProN W3", "Hiragino Kaku Gothic ProN W6", "Hiragino Kaku Gothic Std", "Hiragino Kaku Gothic Std W8", "Hiragino Kaku Gothic StdN", "Hiragino Kaku Gothic StdN W8", "Hiragino Maru Gothic Pro", "Hiragino Maru Gothic Pro W4", "Hiragino Maru Gothic ProN", "Hiragino Maru Gothic ProN W4", "Hiragino Mincho Pro", "Hiragino Mincho Pro W3", "Hiragino Mincho Pro W6", "Hiragino Mincho ProN", "Hiragino Mincho ProN W3", "Hiragino Mincho ProN W6", "Hiragino Sans", "Hiragino Sans GB", "Hiragino Sans GB W3", "Hiragino Sans GB W6", "Hiragino Sans W0", "Hiragino Sans W1", "Hiragino Sans W2", "Hiragino Sans W3", "Hiragino Sans W4", "Hiragino Sans W5", "Hiragino Sans W6", "Hiragino Sans W7", "Hiragino Sans W8", "Hiragino Sans W9", "Hoefler Text", "Hoefler Text Ornaments", "ITF Devanagari", "ITF Devanagari Marathi", "Impact", "InaiMathi", "Iowan Old Style", "Iowan Old Style Black", "J\u00e4rjestelm\u00e4fontti", "Kailasa", "Kannada MN", "Kannada Sangam MN", "Kefa", "Khmer MN", "Khmer Sangam MN", "Kohinoor Bangla", "Kohinoor Devanagari", "Kohinoor Gujarati", "Kohinoor Telugu", "Kokonor", "Krungthep", "KufiStandardGK", "Lao MN", "Lao Sangam MN", "Lucida Grande", "Luminari", "Malayalam MN", "Malayalam Sangam MN", "Marion", "Marker Felt", "Menlo", "Microsoft Sans Serif", "Mishafi", "Mishafi Gold", "Monaco", "Mshtakan", "Mukta Mahee", "MuktaMahee Bold", "MuktaMahee ExtraBold", "MuktaMahee ExtraLight", "MuktaMahee Light", "MuktaMahee Medium", "MuktaMahee Regular", "MuktaMahee SemiBold", "Muna", "Myanmar MN", "Myanmar Sangam MN", "Nadeem", "New Peninim MT", "Noteworthy", "Noto Nastaliq Urdu", "Noto Sans Adlam", "Noto Sans Armenian", "Noto Sans Armenian Blk", "Noto Sans Armenian ExtBd", "Noto Sans Armenian ExtLt", "Noto Sans Armenian Light", "Noto Sans Armenian Med", "Noto Sans Armenian SemBd", "Noto Sans Armenian Thin", "Noto Sans Avestan", "Noto Sans Bamum", "Noto Sans Bassa Vah", "Noto Sans Batak", "Noto Sans Bhaiksuki", "Noto Sans Brahmi", "Noto Sans Buginese", "Noto Sans Buhid", "Noto Sans CanAborig", "Noto Sans Canadian Aboriginal", "Noto Sans Carian", "Noto Sans CaucAlban", "Noto Sans Caucasian Albanian", "Noto Sans Chakma", "Noto Sans Cham", "Noto Sans Coptic", "Noto Sans Cuneiform", "Noto Sans Cypriot", "Noto Sans Duployan", "Noto Sans EgyptHiero", "Noto Sans Egyptian Hieroglyphs", "Noto Sans Elbasan", "Noto Sans Glagolitic", "Noto Sans Gothic", "Noto Sans Gunjala Gondi", "Noto Sans Hanifi Rohingya", "Noto Sans HanifiRohg", "Noto Sans Hanunoo", "Noto Sans Hatran", "Noto Sans ImpAramaic", "Noto Sans Imperial Aramaic", "Noto Sans InsPahlavi", "Noto Sans InsParthi", "Noto Sans Inscriptional Pahlavi", "Noto Sans Inscriptional Parthian", "Noto Sans Javanese", "Noto Sans Kaithi", "Noto Sans Kannada", "Noto Sans Kannada Black", "Noto Sans Kannada ExtraBold", "Noto Sans Kannada ExtraLight", "Noto Sans Kannada Light", "Noto Sans Kannada Medium", "Noto Sans Kannada SemiBold", "Noto Sans Kannada Thin", "Noto Sans Kayah Li", "Noto Sans Kharoshthi", "Noto Sans Khojki", "Noto Sans Khudawadi", "Noto Sans Lepcha", "Noto Sans Limbu", "Noto Sans Linear A", "Noto Sans Linear B", "Noto Sans Lisu", "Noto Sans Lycian", "Noto Sans Lydian", "Noto Sans Mahajani", "Noto Sans Mandaic", "Noto Sans Manichaean", "Noto Sans Marchen", "Noto Sans Masaram Gondi", "Noto Sans Meetei Mayek", "Noto Sans Mende Kikakui", "Noto Sans Meroitic", "Noto Sans Miao", "Noto Sans Modi", "Noto Sans Mongolian", "Noto Sans Mro", "Noto Sans Multani", "Noto Sans Myanmar", "Noto Sans Myanmar Blk", "Noto Sans Myanmar ExtBd", "Noto Sans Myanmar ExtLt", "Noto Sans Myanmar Light", "Noto Sans Myanmar Med", "Noto Sans Myanmar SemBd", "Noto Sans Myanmar Thin", "Noto Sans NKo", "Noto Sans Nabataean", "Noto Sans New Tai Lue", "Noto Sans Newa", "Noto Sans Ol Chiki", "Noto Sans Old Hungarian", "Noto Sans Old Italic", "Noto Sans Old North Arabian", "Noto Sans Old Permic", "Noto Sans Old Persian", "Noto Sans Old South Arabian", "Noto Sans Old Turkic", "Noto Sans OldHung", "Noto Sans OldNorArab", "Noto Sans OldSouArab", "Noto Sans Oriya", "Noto Sans Osage", "Noto Sans Osmanya", "Noto Sans Pahawh Hmong", "Noto Sans Palmyrene", "Noto Sans Pau Cin Hau", "Noto Sans PhagsPa", "Noto Sans Phoenician", "Noto Sans PsaPahlavi", "Noto Sans Psalter Pahlavi", "Noto Sans Rejang", "Noto Sans Samaritan", "Noto Sans Saurashtra", "Noto Sans Sharada", "Noto Sans Siddham", "Noto Sans Sora Sompeng", "Noto Sans SoraSomp", "Noto Sans Sundanese", "Noto Sans Syloti Nagri", "Noto Sans Syriac", "Noto Sans Tagalog", "Noto Sans Tagbanwa", "Noto Sans Tai Le", "Noto Sans Tai Tham", "Noto Sans Tai Viet", "Noto Sans Takri", "Noto Sans Thaana", "Noto Sans Tifinagh", "Noto Sans Tirhuta", "Noto Sans Ugaritic", "Noto Sans Vai", "Noto Sans Wancho", "Noto Sans Warang Citi", "Noto Sans Yi", "Noto Sans Zawgyi", "Noto Sans Zawgyi Blk", "Noto Sans Zawgyi ExtBd", "Noto Sans Zawgyi ExtLt", "Noto Sans Zawgyi Light", "Noto Sans Zawgyi Med", "Noto Sans Zawgyi SemBd", "Noto Sans Zawgyi Thin", "Noto Serif Ahom", "Noto Serif Balinese", "Noto Serif Hmong Nyiakeng", "Noto Serif Myanmar", "Noto Serif Myanmar Blk", "Noto Serif Myanmar ExtBd", "Noto Serif Myanmar ExtLt", "Noto Serif Myanmar Light", "Noto Serif Myanmar Med", "Noto Serif Myanmar SemBd", "Noto Serif Myanmar Thin", "Noto Serif Yezidi", "Optima", "Oriya MN", "Oriya Sangam MN", "PT Mono", "PT Sans", "PT Sans Caption", "PT Sans Narrow", "PT Serif", "PT Serif Caption", "Palatino", "Papyrus", "Party LET", "Phosphate", "Ph\u00f4ng ch\u1eef H\u1ec7 th\u1ed1ng", "PingFang HK", "PingFang SC", "PingFang TC", "Plantagenet Cherokee", "Police syst\u00e8me", "Raanana", "Rendszerbet\u0171t\u00edpus", "Rockwell", "STIX Two Math", "STIX Two Text", "STIXGeneral", "STIXIntegralsD", "STIXIntegralsSm", "STIXIntegralsUp", "STIXIntegralsUpD", "STIXIntegralsUpSm", "STIXNonUnicode", "STIXSizeFiveSym", "STIXSizeFourSym", "STIXSizeOneSym", "STIXSizeThreeSym", "STIXSizeTwoSym", "STIXVariants", "STSong", "Sana", "Sathu", "Savoye LET", "Seravek", "Seravek ExtraLight", "Seravek Light", "Seravek Medium", "Shree Devanagari 714", "SignPainter", "SignPainter-HouseScript", "Silom", "Sinhala MN", "Sinhala Sangam MN", "Sistem Fontu", "Skia", "Snell Roundhand", "Songti SC", "Songti TC", "Sukhumvit Set", "Superclarendon", "Symbol", "Systeemlettertype", "System Font", "Systemschrift", "Systemskrift", "Systemtypsnitt", "Syst\u00e9mov\u00e9 p\u00edsmo", "Tahoma", "Tamil MN", "Tamil Sangam MN", "Telugu MN", "Telugu Sangam MN", "Thonburi", "Times", "Times New Roman", "Tipo de letra del sistema", "Tipo de letra do sistema", "Tipus de lletra del sistema", "Trattatello", "Trebuchet MS", "Verdana", "Waseem", "Webdings", "Wingdings", "Wingdings 2", "Wingdings 3", "Zapf Dingbats", "Zapfino", "\u0393\u03c1\u03b1\u03bc\u03bc\u03b1\u03c4\u03bf\u03c3\u03b5\u03b9\u03c1\u03ac \u03c3\u03c5\u03c3\u03c4\u03ae\u03bc\u03b1\u03c4\u03bf\u03c2", "\u0421\u0438\u0441\u0442\u0435\u043c\u043d\u0438\u0439 \u0448\u0440\u0438\u0444\u0442", "\u0421\u0438\u0441\u0442\u0435\u043c\u043d\u044b\u0439 \u0448\u0440\u0438\u0444\u0442", "\u05d2\u05d5\u05e4\u05df \u05de\u05e2\u05e8\u05db\u05ea", "\u0627\u0644\u0628\u064a\u0627\u0646", "\u0627\u0644\u062a\u0627\u0631\u064a\u062e", "\u0627\u0644\u0646\u064a\u0644", "\u0628\u063a\u062f\u0627\u062f", "\u0628\u064a\u0631\u0648\u062a", "\u062c\u064a\u0632\u0629", "\u062e\u0637 \u0627\u0644\u0646\u0638\u0627\u0645", "\u062f\u0645\u0634\u0642", "\u062f\u064a\u0648\u0627\u0646 \u062b\u0644\u062b", "\u062f\u064a\u0648\u0627\u0646 \u0643\u0648\u0641\u064a", "\u0635\u0646\u0639\u0627\u0621", "\u0641\u0627\u0631\u0633\u064a", "\u0641\u0631\u062d", "\u0643\u0648\u0641\u064a", "\u0645\u0646\u0649", "\u0645\u0650\u0635\u062d\u0641\u064a", "\u0645\u0650\u0635\u062d\u0641\u064a \u0630\u0647\u0628\u064a", "\u0646\u062f\u064a\u0645", "\u0646\u0633\u062e", "\u0648\u0633\u064a\u0645", "\u0906\u0908\u0970\u091f\u0940\u0970\u090f\u092b\u093c\u0970 \u0926\u0947\u0935\u0928\u093e\u0917\u0930\u0940", "\u0906\u0908\u0970\u091f\u0940\u0970\u090f\u092b\u093c\u0970 \u0926\u0947\u0935\u0928\u093e\u0917\u0930\u0940 \u092e\u0930\u093e\u0920\u0940", "\u0915\u094b\u0939\u093f\u0928\u0942\u0930 \u0926\u0947\u0935\u0928\u093e\u0917\u0930\u0940", "\u0926\u0947\u0935\u0928\u093e\u0917\u0930\u0940 \u090f\u092e\u0970\u091f\u0940\u0970", "\u0926\u0947\u0935\u0928\u093e\u0917\u0930\u0940 \u0938\u0902\u0917\u092e \u090f\u092e\u0970\u090f\u0928\u0970", "\u0936\u094d\u0930\u0940 \u0926\u0947\u0935\u0928\u093e\u0917\u0930\u0940 \u096d\u0967\u096a", "\u0e41\u0e1a\u0e1a\u0e2d\u0e31\u0e01\u0e29\u0e23\u0e23\u0e30\u0e1a\u0e1a", "\u2e41\u7175\u6120\u82a9\u82c8", "\u30b7\u30b9\u30c6\u30e0\u30d5\u30a9\u30f3\u30c8", "\u30d2\u30e9\u30ae\u30ce\u4e38\u30b4 Pro", "\u30d2\u30e9\u30ae\u30ce\u4e38\u30b4 Pro W4", "\u30d2\u30e9\u30ae\u30ce\u4e38\u30b4 ProN", "\u30d2\u30e9\u30ae\u30ce\u4e38\u30b4 ProN W4", "\u30d2\u30e9\u30ae\u30ce\u660e\u671d Pro", "\u30d2\u30e9\u30ae\u30ce\u660e\u671d Pro W3", "\u30d2\u30e9\u30ae\u30ce\u660e\u671d Pro W6", "\u30d2\u30e9\u30ae\u30ce\u660e\u671d ProN", "\u30d2\u30e9\u30ae\u30ce\u660e\u671d ProN W3", "\u30d2\u30e9\u30ae\u30ce\u660e\u671d ProN W6", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4 Pro", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4 Pro W3", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4 Pro W6", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4 ProN", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4 ProN W3", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4 ProN W6", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4 Std", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4 Std W8", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4 StdN", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4 StdN W8", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4 \u7c21\u4f53\u4e2d\u6587", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4 \u7c21\u4f53\u4e2d\u6587 W3", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4 \u7c21\u4f53\u4e2d\u6587 W6", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4\u30b7\u30c3\u30af", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4\u30b7\u30c3\u30af W0", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4\u30b7\u30c3\u30af W1", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4\u30b7\u30c3\u30af W2", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4\u30b7\u30c3\u30af W3", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4\u30b7\u30c3\u30af W4", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4\u30b7\u30c3\u30af W5", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4\u30b7\u30c3\u30af W6", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4\u30b7\u30c3\u30af W7", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4\u30b7\u30c3\u30af W8", "\u30d2\u30e9\u30ae\u30ce\u89d2\u30b4\u30b7\u30c3\u30af W9", "\u51ac\u9752\u9ed1\u4f53\u7b80\u4f53\u4e2d\u6587", "\u51ac\u9752\u9ed1\u4f53\u7b80\u4f53\u4e2d\u6587 W3", "\u51ac\u9752\u9ed1\u4f53\u7b80\u4f53\u4e2d\u6587 W6", "\u51ac\u9752\u9ed1\u9ad4\u7c21\u9ad4\u4e2d\u6587", "\u51ac\u9752\u9ed1\u9ad4\u7c21\u9ad4\u4e2d\u6587 W3", "\u51ac\u9752\u9ed1\u9ad4\u7c21\u9ad4\u4e2d\u6587 W6", "\u5b8b\u4f53-\u7b80", "\u5b8b\u4f53-\u7e41", "\u5b8b\u9ad4-\u7c21", "\u5b8b\u9ad4-\u7e41", "\u7cfb\u7d71\u5b57\u9ad4", "\u7cfb\u7edf\u5b57\u4f53", "\u82f9\u65b9-\u6e2f", "\u82f9\u65b9-\u7b80", "\u82f9\u65b9-\u7e41", "\u8371\u8389\u834d\u836d\u8a70\u8353\u2050\u726f", "\u8371\u8389\u834d\u836d\u8a70\u8353\u2053\u7464", "\u8371\u8389\u834d\u836d\u8a70\u8353\u8356\u8362\u834e", "\u8371\u8389\u834d\u836d\u8adb\u8353\u2050\u726f", "\u8371\u8389\u834d\u836d\u96be\u92a9\u2050\u726f", "\u860b\u65b9-\u6e2f", "\u860b\u65b9-\u7c21", "\u860b\u65b9-\u7e41", "\u9ed1\u4f53-\u7b80", "\u9ed1\u4f53-\u7e41", "\u9ed1\u9ad4-\u7c21", "\u9ed1\u9ad4-\u7e41", "\u9ed2\u4f53-\u7c21", "\u9ed2\u4f53-\u7e41", "\uc2dc\uc2a4\ud15c \uc11c\uccb4"]
```

**Windows** fonts (from Windows 11 22H2):

```
["Arial", "Arial Black", "Bahnschrift", "Calibri", "Calibri Light", "Cambria", "Cambria Math", "Candara", "Candara Light", "Comic Sans MS", "Consolas", "Constantia", "Corbel", "Corbel Light", "Courier New", "Ebrima", "Franklin Gothic Medium", "Gabriola", "Gadugi", "Georgia", "HoloLens MDL2 Assets", "Impact", "Ink Free", "Javanese Text", "Leelawadee UI", "Leelawadee UI Semilight", "Lucida Console", "Lucida Sans Unicode", "MS Gothic", "MS PGothic", "MS UI Gothic", "MV Boli", "Malgun Gothic", "Malgun Gothic Semilight", "Marlett", "Microsoft Himalaya", "Microsoft JhengHei", "Microsoft JhengHei Light", "Microsoft JhengHei UI", "Microsoft JhengHei UI Light", "Microsoft New Tai Lue", "Microsoft PhagsPa", "Microsoft Sans Serif", "Microsoft Tai Le", "Microsoft YaHei", "Microsoft YaHei Light", "Microsoft YaHei UI", "Microsoft YaHei UI Light", "Microsoft Yi Baiti", "MingLiU-ExtB", "MingLiU_HKSCS-ExtB", "Mongolian Baiti", "Myanmar Text", "NSimSun", "Nirmala UI", "Nirmala UI Semilight", "PMingLiU-ExtB", "Palatino Linotype", "Segoe Fluent Icons", "Segoe MDL2 Assets", "Segoe Print", "Segoe Script", "Segoe UI", "Segoe UI Black", "Segoe UI Emoji", "Segoe UI Historic", "Segoe UI Light", "Segoe UI Semibold", "Segoe UI Semilight", "Segoe UI Symbol", "Segoe UI Variable", "SimSun", "SimSun-ExtB", "Sitka", "Sitka Text", "Sylfaen", "Symbol", "Tahoma", "Times New Roman", "Trebuchet MS", "Twemoji Mozilla", "Verdana", "Webdings", "Wingdings", "Yu Gothic", "Yu Gothic Light", "Yu Gothic Medium", "Yu Gothic UI", "Yu Gothic UI Light", "Yu Gothic UI Semibold", "Yu Gothic UI Semilight", "\u5b8b\u4f53", "\u5fae\u8edf\u6b63\u9ed1\u9ad4", "\u5fae\u8edf\u6b63\u9ed1\u9ad4 Light", "\u5fae\u8f6f\u96c5\u9ed1", "\u5fae\u8f6f\u96c5\u9ed1 Light", "\u65b0\u5b8b\u4f53", "\u65b0\u7d30\u660e\u9ad4-ExtB", "\u6e38\u30b4\u30b7\u30c3\u30af", "\u6e38\u30b4\u30b7\u30c3\u30af Light", "\u6e38\u30b4\u30b7\u30c3\u30af Medium", "\u7d30\u660e\u9ad4-ExtB", "\u7d30\u660e\u9ad4_HKSCS-ExtB", "\ub9d1\uc740 \uace0\ub515", "\ub9d1\uc740 \uace0\ub515 Semilight", "\uff2d\uff33 \u30b4\u30b7\u30c3\u30af", "\uff2d\uff33 \uff30\u30b4\u30b7\u30c3\u30af"]
```

**Linux** fonts (from TOR bundle):

```
["Arimo", "Cousine", "Noto Naskh Arabic", "Noto Sans Adlam", "Noto Sans Armenian", "Noto Sans Balinese", "Noto Sans Bamum", "Noto Sans Bassa Vah", "Noto Sans Batak", "Noto Sans Bengali", "Noto Sans Buginese", "Noto Sans Buhid", "Noto Sans Canadian Aboriginal", "Noto Sans Chakma", "Noto Sans Cham", "Noto Sans Cherokee", "Noto Sans Coptic", "Noto Sans Deseret", "Noto Sans Devanagari", "Noto Sans Elbasan", "Noto Sans Ethiopic", "Noto Sans Georgian", "Noto Sans Grantha", "Noto Sans Gujarati", "Noto Sans Gunjala Gondi", "Noto Sans Gurmukhi", "Noto Sans Hanifi Rohingya", "Noto Sans Hanunoo", "Noto Sans Hebrew", "Noto Sans JP", "Noto Sans Javanese", "Noto Sans KR", "Noto Sans Kannada", "Noto Sans Kayah Li", "Noto Sans Khmer", "Noto Sans Khojki", "Noto Sans Khudawadi", "Noto Sans Lao", "Noto Sans Lepcha", "Noto Sans Limbu", "Noto Sans Lisu", "Noto Sans Mahajani", "Noto Sans Malayalam", "Noto Sans Mandaic", "Noto Sans Masaram Gondi", "Noto Sans Medefaidrin", "Noto Sans Meetei Mayek", "Noto Sans Mende Kikakui", "Noto Sans Miao", "Noto Sans Modi", "Noto Sans Mongolian", "Noto Sans Mro", "Noto Sans Multani", "Noto Sans Myanmar", "Noto Sans NKo", "Noto Sans New Tai Lue", "Noto Sans Newa", "Noto Sans Ol Chiki", "Noto Sans Oriya", "Noto Sans Osage", "Noto Sans Osmanya", "Noto Sans Pahawh Hmong", "Noto Sans Pau Cin Hau", "Noto Sans Rejang", "Noto Sans Runic", "Noto Sans SC", "Noto Sans Samaritan", "Noto Sans Saurashtra", "Noto Sans Sharada", "Noto Sans Shavian", "Noto Sans Sinhala", "Noto Sans Sora Sompeng", "Noto Sans Soyombo", "Noto Sans Sundanese", "Noto Sans Syloti Nagri", "Noto Sans Symbols", "Noto Sans Symbols 2", "Noto Sans Syriac", "Noto Sans TC", "Noto Sans Tagalog", "Noto Sans Tagbanwa", "Noto Sans Tai Le", "Noto Sans Tai Tham", "Noto Sans Tai Viet", "Noto Sans Takri", "Noto Sans Tamil", "Noto Sans Telugu", "Noto Sans Thaana", "Noto Sans Thai", "Noto Sans Tifinagh", "Noto Sans Tifinagh APT", "Noto Sans Tifinagh Adrar", "Noto Sans Tifinagh Agraw Imazighen", "Noto Sans Tifinagh Ahaggar", "Noto Sans Tifinagh Air", "Noto Sans Tifinagh Azawagh", "Noto Sans Tifinagh Ghat", "Noto Sans Tifinagh Hawad", "Noto Sans Tifinagh Rhissa Ixa", "Noto Sans Tifinagh SIL", "Noto Sans Tifinagh Tawellemmet", "Noto Sans Tirhuta", "Noto Sans Vai", "Noto Sans Wancho", "Noto Sans Warang Citi", "Noto Sans Yi", "Noto Sans Zanabazar Square", "Noto Serif Armenian", "Noto Serif Balinese", "Noto Serif Bengali", "Noto Serif Devanagari", "Noto Serif Dogra", "Noto Serif Ethiopic", "Noto Serif Georgian", "Noto Serif Grantha", "Noto Serif Gujarati", "Noto Serif Gurmukhi", "Noto Serif Hebrew", "Noto Serif Kannada", "Noto Serif Khmer", "Noto Serif Khojki", "Noto Serif Lao", "Noto Serif Malayalam", "Noto Serif Myanmar", "Noto Serif NP Hmong", "Noto Serif Sinhala", "Noto Serif Tamil", "Noto Serif Telugu", "Noto Serif Thai", "Noto Serif Tibetan", "Noto Serif Yezidi", "STIX Two Math", "Tinos", "Twemoji Mozilla"]
```

Note other fonts can be added to this list (and please do add your own fonts) to avoid font fingerprinting.

</details>

<details>
<summary>
Screen
</summary>

| Property           | Status |
| ------------------ | ------ |
| screen.availHeight | ✅     |
| screen.availWidth  | ✅     |
| screen.availTop    | ✅     |
| screen.availLeft   | ✅     |
| screen.colorDepth  | ✅     |
| screen.height      | ✅     |
| screen.width       | ✅     |
| screen.pixelDepth  | ✅     |
| screen.pageXOffset | ✅     |
| screen.pageYOffset | ✅     |

**Notes:**

- For screen properties, using Page.setViewportSize() may be more effective.

</details>

<details>
<summary>
Window
</summary>

| Property                | Status                      |
| ----------------------- | --------------------------- |
| window.scrollMinX       | ✅                          |
| window.scrollMinY       | ✅                          |
| window.scrollMaxX       | ✅                          |
| window.scrollMaxY       | ✅                          |
| window.innerHeight      | ✅                          |
| window.outerHeight      | ✅                          |
| window.outerWidth       | ✅                          |
| window.innerWidth       | ✅                          |
| window.screenX          | ✅                          |
| window.screenY          | ✅                          |
| window.history.length   | ✅                          |
| window.devicePixelRatio | Works, but not recommended! |

</details>

<details>
<summary>
Document
</summary>

Spoofing document.body has been implemented, but it is more advicable to set `window.innerWidth` and `window.innerHeight` instead.

| Property                   | Status |
| -------------------------- | ------ |
| document.body.clientWidth  | ✅     |
| document.body.clientHeight | ✅     |
| document.body.clientTop    | ✅     |
| document.body.clientLeft   | ✅     |

</details>

<details>
<summary>
Miscellaneous (WebGl spoofing, battery status, etc)
</summary>

| Property                | Status | Notes                                                                                                                                          |
| ----------------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| pdfViewer               | ✅     | Sets navigator.pdfViewerEnabled. Please keep this on though, many websites will flag a lack of pdfViewer as a headless browser.                |
| webGl:renderer          | ✅     | Spoofs the name of the unmasked WebGL renderer. Can cause leaks, use at your own caution! Also note, webGl is disabled in Camoufox by default. |
| webGl:vendor            | ✅     | Spoofs the name of the unmasked WebGL vendor. Can cause leaks, use at your own caution! Also note, webGl is disabled in Camoufox by default.   |
| battery:charging        | ✅     | Spoofs the battery charging status.                                                                                                            |
| battery:chargingTime    | ✅     | Spoofs the battery charging time.                                                                                                              |
| battery:dischargingTime | ✅     | Spoofs the battery discharging time.                                                                                                           |
| battery:level           | ✅     | Spoofs the battery level.                                                                                                                      |

**Notes:**

- For screen properties, using Page.setViewportSize() may be more effective.

</details>

<hr width=50>

## Patches

### What other changes were made?

#### Fingerprint injection

- Navigator properties spoofing (device, browser, locale, etc.)
- Support for emulating screen size, resolution, etc.
- Spoof default system fonts of Windows, Mac, and Linux
- WebGL unmasked renderer spoofing (WIP).
- Battery API spoofing
- Support for spoofing both inner and outer window sizes
- Network headers (Accept-Languages and User-Agent) are spoofed to match the navigator properties.
- etc.

#### Playwright support

- Added Playwright's Juggler patches
- Various config patches to evade bot detection

#### Debloat/Optimizations

- Stripped out/disabled _many, many_ Mozilla services. Runs faster than the original Mozilla Firefox, and uses less memory (200mb)
- Includes the debloat config from PeskyFox & LibreWolf, and others
- Speed optimizations from FastFox, and other network optimizations
- Minimalistic theming
- etc.

#### Addons

- Added uBlock Origin with custom privacy filters
- Added B.P.C.
- Addons are not allowed to open tabs
- Addons will automatically run in Private Browsing mode

## Stealth Performance

### Tests

Camoufox performs well against every major WAF I've tested. (Test sites from [Botright](https://github.com/Vinyzu/botright/?tab=readme-ov-file#browser-stealth))

| Test                                                                                               | Status                                            |
| -------------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| **reCaptcha Score**                                                                                | ✔️                                                |
| ‣ [nopecha.com](https://nopecha.com/demo/recaptcha)                                                | ✔️ (v2-Hardest is unstable on Chrome fingerprint) |
| ‣ [recaptcha-demo.appspot.com](https://recaptcha-demo.appspot.com/recaptcha-v3-request-scores.php) | ✔️ 0.9                                            |
| ‣ [berstend.github.io](https://berstend.github.io/static/recaptcha/v3-programmatic.html)           | ✔️ 0.9                                            |
| [**CreepJS**](https://abrahamjuliot.github.io/creepjs/)                                            | ✔️ 68.5% (56% with Chrome fingerprint)            |
| ‣ **DataDome**                                                                                     | ✔️                                                |
| ‣ [antoinevastel.com](https://antoinevastel.com/bots/datadome)                                     | ✔️                                                |
| ‣ [datadome.co](https://datadome.co/bot-tester/)                                                   | ✔️                                                |
| **Imperva**                                                                                        | ✔️                                                |
| ‣ [ticketmaster.es](https://www.ticketmaster.es/)                                                  | ✔️                                                |
| ‣ **Kasada**                                                                                       | ✔️                                                |
| ‣ [canadagoose.com](https://www.canadagoose.com/)                                                  | ✔️                                                |
| ‣ **Cloudflare**                                                                                   | ✔️                                                |
| ‣ [Turnstile](https://nopecha.com/demo/turnstile)                                                  | ✔️                                                |
| ‣ [Interstitial](https://nopecha.com/demo/cloudflare)                                              | ✔️❓ Unstable on Chrome fingerprints              |
| [**SannySoft**](https://bot.sannysoft.com/)                                                        | ✔️                                                |
| [**Incolumitas**](https://bot.incolumitas.com/)                                                    | ✔️ 0.8-1.0                                        |
| [**Fingerprint.com**](https://fingerprint.com/products/bot-detection/)                             | ✔️                                                |
| [**IpHey**](https://iphey.com/)                                                                    | ✔️                                                |
| [**BrowserScan**](https://browserscan.net/)                                                        | ✔️                                                |
| [**Bet365**](https://www.bet365.com/#/AC/B1/C1/D1002/E79147586/G40/)                               | ✔️                                                |

Camoufox does **not** fully support injecting Chromium fingerprints. Some websites (such as Cloudflare [Interstitial](https://nopecha.com/demo/cloudflare)) look for the Gecko webdriver underneath.

---

## Build System

### Overview

Here is a diagram of the build system, and its associated make commands:

```mermaid
graph TD
    FFSRC[Firefox Source] -->|make fetch| REPO

    subgraph REPO[Camoufox Repository]
        MASKING[Camoufox masking module]
        PATCHES[Debloat/optimizations]
        ADDONS[uBlock & B.P.C.]
        SYSTEM_FONTS[Win, Mac, Linux System fonts]
        JUGGLER[Playwright Juggler]
    end

    subgraph Local
    REPO -->|make dir| PATCH[Patched Source]
    PATCH -->|make build| BUILD[Built]
    BUILD -->|make package-linux| LINUX[Linux Portable]
    BUILD -->|make package-windows| WIN[Windows Portable]
    BUILD -->|make package-macos| MAC[macOS Portable]
    end
```

This was originally forked from the LibreWolf build system.

## Build CLI

> [!WARNING]
> Camoufox's build system is designed to be used in Linux. WSL will not work!

First, clone this repository with Git:

```bash
git clone --depth 1 https://gitlab.com/daijro/camoufox
cd camoufox
```

Next, build the Camoufox source code with the following command:

```bash
make dir
```

After that, you have to bootstrap your system to be able to build Camoufox. You only have to do this one time. It is done by running the following command:

```bash
make bootstrap
```

Finally you can build Camoufox and then package it with the following commands:

```bash
make build
# Example package commands:
make package-linux arch=x64
make package-windows arch=x86
make package-macos arch=amd64
```

### Using Docker

Camoufox can be built through Docker on all platforms.

1. Create the Docker image containing Firefox's source code:

```bash
docker build -t camoufox-builder .
```

2. Build Camoufox patches to a target platform and architecture:

```bash
docker run -v "$(pwd)/dist:/app/dist" camoufox-builder --target <os> --arch <arch>
```

<details>
<summary>
CLI Parameters
</summary>

```bash
Options:
  -h, --help            show this help message and exit
  --target {linux,windows,macos}
                        Target platform for the build
  --arch {x86_64,arm64,i686}
                        Target architecture for the build
```

</details>

<details>
<summary>
How can I use my local ~/.mozbuild directory?
</summary>

If you want to use the host's .mozbuild directory, you can use the following command instead to run the docker:

```bash
docker run \
  -v "$HOME/.mozbuild":/root/.mozbuild:rw,z \
  -v "$(pwd)/dist:/app/dist" \
  camoufox-builder \
  --target <os> \
  --arch <arch>
```

</details>

<br>

Build artifacts will now appear written under the `dist/` folder.

---

## Development Notes

### How to make a patch

This repo comes with a developer UI under scripts/developer.py:

```
make edits
```

Patches can be added, removed, and new patches can be added through here.

<img src="https://i.imgur.com/cLEn2Yr.png">

To use, select "Reset workspace", make changes in the camoufox-\*/ folder, then select "Write workspace to patch".

### How to work on an existing patch

1. In the developer UI, reset your workspace.
2. Then, click "Select patches", and select all **but** the one you want to edit.
3. Create a checkpoint. This will commit the current workspace to the local repo:

```bash
make checkpoint
```

4. In the developer UI, click "Select patches", and _apply_ the patch you would like to edit.

   Make your changes. Test builds can be made with `make build` and `make run`.

5. After you're done editing, hit "Write workspace to patch", and overwrite the existing patch.

---
