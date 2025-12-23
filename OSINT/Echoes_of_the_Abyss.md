---

# 🕯️ Echoes of the Abyss — OSINT Write-Up

**Challenge Name:** Echoes of the Abyss
**Category:** OSINT
**Points:** 750

> *“A nameless knight, long forgotten by the flame, has scattered fragments of their soul across the digital abyss.

They say the last Cinder still burns somewhere... waiting for an Unkindled to piece together what remains.

To link the fire, one must first seek the fallen knight.”*

---

## 🧠 Challenge Overview

The challenge revolves around a **Dark Souls–themed OSINT trail**.
A forgotten knight has scattered digital traces across multiple platforms.
Each clue leads to another service, requiring **metadata analysis, decoding, social media investigation, repository history analysis, and geolocation OSINT**.

The final objective was to **piece together all clues and locate the final flag**.

---

## 🔍 Step-by-Step Investigation

---

## 1️⃣ Image Analysis (bonfire.jpg)

The challenge provides an image named **bonfire.jpg**.
Given the OSINT context, the first logical step was to inspect the **image metadata**.

### Tool Used:

* `exif.tools`

### Key Finding (EXIF Metadata):

> *“In the final primes of 100, there lies the last flame that turns the log to ash.
> Its echo lingers where the blue bird once sang.”*

### Interpretation:

* **Final prime below 100** → `97`
* **Blue bird** → Twitter (now X)
* **Last flame / cinder** → likely a username

### Conclusion:

The metadata strongly suggests a Twitter/X username:

```
LastCinder97
```

---

## 2️⃣ Twitter / X Investigation

### Profile Found:

🔗 [https://x.com/LastCinder97](https://x.com/LastCinder97)

The account contained **8 posts**, out of which **4 were relevant**.

### Important Tweets:

1. A post mentioning a **YouTuber friend**
2. A short code:

   ```
   CgG4FyPC
   ```
3. A long **hexadecimal string**:

   ```
   55 43 7a 2d 6b 52 57 67 75 61 78 7a 49 71 74 62 45 31 79 49 39 5a 62 41
   ```
4. The phrase:

   ```
   Pickle pee, Pump-a-rum
   ```

### Clue Summary:

* YouTube reference
* Encoded values
* Pastebin-style code
* Dark Souls reference text

---

## 3️⃣ Hex Decoding

### Tool Used:

* CyberChef

### Input:

```
55 43 7a 2d 6b 52 57 67 75 61 78 7a 49 71 74 62 45 31 79 49 39 5a 62 41
```

### Output:

```
UCz-kRWguaxzIqtbE1yI9ZbA
```

### Interpretation:

This format matches a **YouTube Channel ID**.

---

## 4️⃣ YouTube Channel Investigation

### Channel URL:

🔗 [https://www.youtube.com/channel/UCz-kRWguaxzIqtbE1yI9ZbA](https://www.youtube.com/channel/UCz-kRWguaxzIqtbE1yI9ZbA)

### Channel Name:

**The Ashen One**

The channel had **no obvious videos**, but the **channel banner contained a link** to an **unlisted video**.

---

## 5️⃣ Unlisted Video Analysis

The unlisted video itself contained **no visual clues**.
However, checking **advanced details** revealed a clue.

### Location of Clue:

* **Video transcript**

### Encoded Text Found:

```
OUXUC43IMVXE63TF
```

---

## 6️⃣ Decoding the Transcript

### Tool Used:

* CyberChef (Magic / Base decoding)

### Decoded Output:

```
u/AshenOne
```

### Interpretation:

This is a **Reddit username**.

---

## 7️⃣ Reddit OSINT

### Profile Found:

* `u/AshenOne67`

On reviewing the profile, the key discovery was found under:

* **Moderator of these communities**

### Relevant Subreddit:

```
r/FireIinkShrine
```

This subreddit contained references pointing toward **GitHub**.

---

## 8️⃣ GitHub Investigation

### Referenced Repository:

```
https://github.com/AshenOne67/SoulsTracker
```

The repository was **private / removed (404)**.

### OSINT Technique Used:

* Checking **related users**
* Examining **stars & forks**

### Breakthrough:

A related user was found:
🔗 [https://github.com/shah2006suhail](https://github.com/shah2006suhail)

This account contained a **public repository** named:

```
SoulsTracker
```

---

## 9️⃣ Commit History Analysis

The repository contained **9 commits**.

### Important Commits:

* `Initial README + hints`
* `Add secret (contains pastebin link)`

The latter commit mentioned:

> *“This file contains the pastebin link for the next step of the challenge.
> It will be removed from the tip of the branch — check previous commits to retrieve it.”*

### Key Discovery:

A **tag name** containing the Pastebin ID:

```
Jeja3z8T
```

---

## 🔟 Pastebin Clue

### URL:

🔗 [https://pastebin.com/Jeja3z8T](https://pastebin.com/Jeja3z8T)

### Paste Content:

> *“Ashen One, you're just one step away from rekindling the flame.
> Seek the place that Lord Gwyn ruled over, the city of the mighty,
> which housed the children of Gwyn, the capital city of the once glorious kingdom, now in ruins.”*

### Interpretation:

This description clearly refers to:

```
Anor Londo
```

(from the Dark Souls universe)

---

## 1️⃣1️⃣ Geolocation OSINT (Google Maps)

Searching **“Anor Londo”** on Google Maps produced multiple results.

Each location was inspected carefully.

### Final Discovery:

On the **correct map listing**, a **Google review** posted by:

```
Praneesh R V
```

contained the flag.

---

## 🏁 Final Flag

```
L3m0nCTF{Link_the_fire_or_walk_the_path_of_dark}
```

---

## 🛠️ Tools & Platforms Used

| Platform / Tool | Purpose                        |
| --------------- | ------------------------------ |
| EXIF.tools      | Image metadata extraction      |
| Twitter (X)     | Username OSINT                 |
| CyberChef       | Hex & string decoding          |
| YouTube         | Channel & transcript analysis  |
| Reddit          | User & subreddit investigation |
| GitHub          | Commit history OSINT           |
| Pastebin        | Hidden clue retrieval          |
| Google Maps     | Geolocation & review analysis  |

---

## ⏱️ Effort & Scope

* **Total platforms investigated:** 8
* **Commits analyzed:** 9
* **Encodings decoded:** Multiple (hex, base, magic)
* **OSINT techniques used:** Metadata analysis, username pivoting, commit forensics, transcript extraction, geolocation OSINT
* **Estimated time investment:** Several hours of careful investigation and correlation

---

##📝 Final Notes

You followed the author’s breadcrumb trail perfectly — from EXIF poem → prime number → blue bird → X → hex → YouTube → transcript → Reddit → GitHub → Pastebin → Anor Londo → Google Review.
That’s the OSINT holy trinity of “look everywhere, decode everything, and don’t trust obvious Rickrolls.”

Also — Rick Astley is an emotional landmine.
You handled it like a pro. 🕵️‍♂️🔥

## 📝 Conclusion

This challenge was a **well-designed OSINT puzzle** that rewarded persistence and attention to detail.
Each clue logically chained into the next, requiring **cross-platform thinking** rather than brute force.

From a single image to a hidden Google Maps review — the journey truly reflected the theme:

> *Link the fire… or walk the path of dark.*

🔥 **Well played, Unkindled.**
