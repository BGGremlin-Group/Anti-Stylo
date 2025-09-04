### ***🛸The BG GREMLIN GROUP ANTI-STYLOMETRY TOOL🛸***

> Offline, browser-based text obfuscation for privacy, and anonymity.


---

# Why this exists

**What is stylometry?**

*Stylometry* is the statistical study of *linguistic style—patterns* such as character and word n-grams, punctuation habits, function-word usage, syntactic preferences, and rhythm. Taken together, these features can serve as an “authorship fingerprint,” enabling systems to link pseudonymous texts back to the same writer or even to a known identity. Modern pipelines range from classic Writeprints-style feature bags to deep neural encoders that learn author embeddings from raw text. The point isn’t *“what you said,”* but *how you tend to say it.*

# How stylometry affects people today

Anonymity erosion. Writers who operate under pseudonyms (activists, whistleblowers, survivors, employees discussing sensitive topics, etc.) can be clustered or deanonymized based on style—even across platforms.

Chilling effects. Knowing one’s style can be traced discourages participation in forums, reporting, and research—especially for vulnerable groups.

Sockpuppet & bot hunting (with collateral damage). Authorship-linking tools help platforms find bad actors, but they also create false positives when multiple people share dialects or when large language models flatten style, causing misattribution.

Cross-context tracking. Even if you never reuse a username or email, your writing style can connect work, school, and personal accounts.


# Why programs are needed to combat stylometry

Telling people to *“just write differently”* **doesn’t work**. Stylometric features are subtle, numerous, and correlated. Manual edits are inconsistent and cognitively heavy; automated rewriters often change meaning, leak to servers, or impose a telltale “LLM voice.” A practical defense needs to be:

- Local/offline. Text never leaves your machine.

- Configurable. Different threat models require different transformations.

- Layered & stochastic. Multiple, randomized edits reduce consistent signatures.

- Reversible enough for you. You should be able to roughly get back to readable form.


*That is precisely why this tool exists.*


---

# What this project is

The *BG Gremlin Group* **Anti-Stylometry Tool** is a single-file, offline-capable web app you open in any modern browser. It lets you paste text, apply layered, randomized obfuscations, and analyze overused tokens—without sending data anywhere. The app title appears prominently in the UI (***“THE BG GREMLIN GROUP ANTI-STYLOMETRY TOOL”***).

# Key features (at a glance)

Obfuscation intensity slider (1–100%) to tune how aggressively transformations are applied.

*Layered transformations you can toggle on/off:*

- Quote nouns/pronouns

- Punctuation noise

- Pronoun capitalization

- Word substitution

- Emoji injection

- Fake metadata

Syntax shuffle
(All layers are surfaced as checkboxes in the UI.)


Theme-based style shifts (East Coast, West Coast, Tech, Goth, Conspiracy, Esoteric, Intellectual) to nudge vocabulary toward a chosen register.

Word frequency analysis with a simple “heat” visualization (red/yellow/green) and tally, plus click-to-suggest alternatives.

Decode & Clear actions to heuristically reverse common obfuscations and reset the workspace.

Fully client-side UI with optional visual flair (a starfield/earth background rendered via Three.js).


> Note on offline assets. The default HTML references a CDN for Three.js and a remote Earth texture; to run with no network, vendor these locally and update the paths. See Offline setup below.




---

# How the defense works (conceptual)

This tool focuses on surface-level and shallow syntactic features that classical and modern stylometry often learn—without rewriting your meaning. It applies many small, randomized edits so any single model sees less consistent signal:

1. Token framing & punctuation variability. Adding quotes around detected nouns/pronouns changes boundary patterns; punctuation variation perturbs sentence-final and intra-sentence markers.


2. Case and pronoun emphasis. Random capitalization disrupts casing distributions frequently used as features.


3. Theme-targeted vocabulary swaps. Opt-in registers (e.g., Tech or Goth) replace common lexical items with plausible alternatives, creating localized dialect drift.


4. Common-word and synonym substitutions. Randomized, capitalization-aware replacements alter your most predictable lexical frequencies.


5. Syntax shuffle (light). Limited clause re-ordering and sentence tinkering inject additional variance without heavy paraphrasing.


6. Decorative noise. Emoji and fake metadata (hashtags/sign-offs) add unpredictable tokens at boundaries—use sparingly if your threat model penalizes non-semantic tokens.


Decode heuristics undo many of these edits (remove quotes/emojis/sign-offs/metadata; collapse punctuation; reverse known substitutions), producing a more readable, approximate original. This isn’t a lossless codec—it’s a convenience for you, not a promise to reconstruct the exact text.

Word analysis helps you spot overused tokens (which often carry stylistic signal) and try alternatives with a click.


---

# Threat model & limits (read this!)

*This is not a magic cloak*. Advanced authorship models can exploit deeper structure (syntax trees, discourse patterns, semantic preferences). Our layers primarily target surface features; determined adversaries may still cluster texts.

*Randomization is a trade-off*. Higher intensity increases dispersion but risks readability and introduces new artifacts (e.g., unusual punctuation bursts). Use the slider prudently.

*Domain shift matters*. If your writing occurs in a constrained register (e.g., academic abstracts), excessive slang/theme shifts could increase suspicion. Theme toggles are opt-in for that reason.

*Decode is heuristic*. It removes many transformations but may fail to recover all original tokens or order. Keep your original text separately if exact fidelity matters.


---

# Quick start (no build)

1. Download/clone the repo and open the HTML file in a modern browser.


2. Paste text into Enter Text.


3. Set Obfuscation Intensity and choose Obfuscation Styles.


4. Optionally enable Theme Styles (dialects/registers).


5. Click 🔒 Obfuscate to transform, 📊 Analyze Words to inspect token frequencies, 🔓 Decode to attempt reversal, or 🗑️ Clear to reset.


6. Tune UI Transparency and Background Blur to your taste (purely visual).

> Tip: Keep transformations light but diverse. Combining two or three gentle layers often preserves meaning while reducing stylistic consistency.




---

# Offline setup (strict no-network mode)

The app is client-side already. To ensure zero external requests:

Vendor Three.js locally. Replace the CDN script tag with a local file path. The current HTML references cdnjs (three.min.js r128).

Bundle textures. The Earth background uses a remote texture from the Three.js repo; download it and replace the URL with a local path.

Open the HTML file from disk (no server required). All obfuscation and analysis functions run in your browser.



---

# What’s inside (selected implementation details)

Capitalization-aware substitutions. Replacements preserve initial letter case for natural look.

Noun/pronoun detection (lightweight). Uses simple heuristics (proper-case tokens + pronoun list) to add quotes selectively.

Emoji/metadata/signoffs. Randomized insertions at sentence ends and tails; easy to strip during decode.

Clause shuffle. Limited reordering around commas and sentence boundaries to perturb syntax without changing meaning dramatically.

UI enhancements. Word-cloud “heat” classes (red/yellow/green) help you spot potential stylometric anchors at a glance.



---

# Current methods of stylometry circumvention (and where this tool fits)

Manual style-masking. Writers attempt to “act” a different voice. Effective only for short texts; error-prone and exhausting.

Paraphrasing via cloud LLMs. Can wash style but often injects the model’s fingerprint, changes meaning, and requires sending your text to a third party.

Back-translation / round-trip translation. Adds noise and semantic drift; recognizable artifacts.

Automated local perturbation (this project). Layered, randomized, on-device edits that target shallow stylistic cues while keeping semantics in your control.


This tool intentionally avoids heavy semantic rewriting. It’s a defensive obfuscator, not a ghostwriter.


---

# Roadmap

Local POS tagging and sentence-level transformations that are semantics-aware (still offline).

Optional consistency testing: compare pre/post stylometric profiles locally.

Per-domain presets (academic, forum, chat) and strength recommendations.



---

# FAQ

Does this guarantee I can’t be linked?
No. It reduces some signal and introduces variance; it does not defeat dedicated forensics.

Will the decode button recover my exact text?
No. It reverses many common steps (quotes, emojis, casing, substitutions) but is not lossless. Keep your source.

Is the flashy background required?
No. It’s purely cosmetic (Three.js starfield/Earth). Remove or keep; for full offline operation, vendor assets locally.


---

# Contributing & ethics

Contributions that improve local privacy are welcome. Please include threat-model notes with PRs.


---

Built for researchers, privacy-minded writers, and anyone in-between on the world wide web—***because your words shouldn’t be a tracking cookie.***
