# 🪐 Physics Trauma — OSINT Write-Up

**Challenge Name:** Physics Trauma
**Category:** OSINT
**Difficulty:** Medium → Hard (multi‑platform reasoning)
**Final Flag:**

```
L3m0nCTF{backtalk_seeded_restyled}
```

---

## 🧩 Challenge Description Analysis

> *“Someone orbits the digital cosmos, leaving traces of their calculations.
> Find their parameter, follow their journey, and discover where the coordinates meet.”*

The description is intentionally abstract—common for OSINT challenges. Breaking it down:

* **orbits / cosmos** → scientific / physics theme
* **calculations** → technical or analytical content
* **parameter** → likely a username or identifier
* **journey** → cross‑platform trail
* **coordinates meet** → a geographic midpoint

Nothing actionable yet—but the provided hint changes everything.

---

## 🔑 Hint Interpretation

> **There’s someone named `OrbitalParameter` sharing calculations online**

Immediate conclusions:

* We are hunting a **specific username**
* The challenge will involve **account pivoting**
* “Calculations” suggests **code, math, or physics‑related posts**

➡️ Classic OSINT username enumeration begins.

---

## 1️⃣ Username Enumeration — `OrbitalParameter`

### 🔍 Google Search

Results revealed a **GitHub account** named `OrbitalParameter`. However:

* No useful repositories
* No meaningful commits
* No clear breadcrumbs

❌ Dead end—but it confirms the username exists.

➡️ Next step: search other platforms.

---

## 2️⃣ Reddit Discovery (Major Breakthrough)

Searching Reddit uncovered:

```
u/OrbitalParameter
```

The account contained **4 posts**. One post stood out:

> *“yes i do hate coding, ugh can someone remind me why Python sometimes prints 0.30000000004?”*
> *“I know this is floating‑point stuff, but is there a simple explanation for humans?”*
> **jzWAEjDv !!!!!!!!!!**

### Why this mattered

* Floating‑point discussion aligns with **calculations**
* The random string is a deliberate **breadcrumb**

---

## 3️⃣ Pastebin Link Extraction

The string `jzWAEjDv` matched a **Pastebin ID**:

```
https://pastebin.com/jzWAEjDv
```

Inside, a crucial line appeared:

> **“see analysis write‑up: Med. notes 3”**

### Interpretation

* **Med.** → Medium.com
* **notes** → article / write‑up
* **3** → reference index or internal note

➡️ Next pivot: Medium.

---

## 4️⃣ Medium Investigation

Direct searches for `OrbitalParameter` on Medium returned nothing. After indirect searching, the following article surfaced:

```
https://medium.com/@strugglingorbit/trying-to-summarize-the-thermal-drift-lab-notes-probably-wrong-494d1bb6462f
```

### Why this article is relevant

* Physics / lab notes theme
* Fits the challenge narrative
* Author handle `strugglingorbit` matches the **orbit** motif

---

## 5️⃣ Comment Section Clue

In the article’s comments, a suspicious username appeared:

```
u4pruydqqvj
```

Observations:

* Not human‑readable
* Structured, not random
* Likely **encoded**

➡️ Candidate for a **hash, geohash, or burner account**.

---

## 6️⃣ GitHub Pivot — `u4pruydqqvj`

Searching this string led to:

```
https://github.com/u4pruydqqvj
```

The account hosted a single repository:

```
Temperature-analysis
```

---

## 7️⃣ Repository README Analysis

The `README.md` contained a key passage:

```
During the lab debrief, the instructor mentioned something about
“spatial anchors” used in verifying the environmental simulation.

Each validator script uses a textual coordinate token.

Example:
///relive.expresses.ripping
```

### Key deductions

* “Spatial anchors” → geographic reference
* “Textual coordinate token” → words instead of numbers
* Three words separated by dots → **what3words**

---

## 8️⃣ Commit History Examination

The repository contained **5 commits**. One commit, titled:

```
Create work-in-progress
```

Included the following TODO:

```
- confirm whether midpoint == (lat1+lat2)/2 and (lon1+lon2)/2
- check if W3W anchors resolve consistently across devices
- compare with the older notes from the Medium write-up
```

### This reveals the intended solution path

* Two coordinate points exist
* Their **midpoint** must be calculated
* The result will resolve via **what3words**

---

## 9️⃣ Decoding Coordinate #1 — Geohash

The username `u4pruydqqvj` was tested as a **geohash**. Using a decoder, it resolved to:

```
Latitude : 57.64911063015461
Longitude: 10.407439693808556
```

➡️ **First coordinate obtained**

---

## 🔟 Decoding Coordinate #2 — what3words

From the README example:

```
///relive.expresses.ripping
```

Using what3words:

```
Latitude : 48.6695100
Longitude: 68.6144810
```

➡️ **Second coordinate obtained**

---

## 1️⃣1️⃣ Midpoint Calculation

Using the formula specified in the commit:

```
Mid Lat = (lat1 + lat2) / 2
Mid Lon = (lon1 + lon2) / 2
```

### Result

```
Mid Lat ≈ 53.159309
Mid Lon ≈ 39.510951
```

---

## 1️⃣2️⃣ Final what3words Resolution

Resolving the midpoint coordinates via what3words produced:

```
///backtalk.seeded.restyled
```

No further instructions were present in the challenge text.

---

## 1️⃣3️⃣ Author Confirmation

To confirm correctness, a ticket was opened with the challenge author. Response:

> *“That’s the flag. Put underscore instead of dots.”*

---

## 🏁 Final Flag

```
L3m0nCTF{backtalk_seeded_restyled}
```

---

## 🛠️ Tools & Platforms Used

* Google — username pivoting
* Reddit — primary breadcrumb
* Pastebin — hidden reference
* Medium — secondary write‑up
* GitHub — README & commit analysis
* Geohash decoder (dcode.fr)
* what3words
* Basic coordinate arithmetic

**Total platforms involved:** 8+
**Key OSINT skills applied:**

* Username correlation
* Metadata chaining
* Commit analysis
* Encoding recognition
* Geolocation reasoning

---

## 🎯 Final Thoughts

This challenge is an excellent example of **clean, fair OSINT design**:

* Every clue is intentional
* No brute forcing or guesswork
* Each platform naturally leads to the next

It feels difficult while solving—but every step is logical in hindsight.

**Simple later. Tough in the moment. Extremely satisfying.** 🔥
