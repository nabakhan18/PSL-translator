# PSL Translator — AI-Powered Multilingual Text-to-PSL Avatar Translator

A prototype implementation of the system described in *"AI-Powered Multilingual
Text-to-Sign Language Translation Using an Animated Avatar for Deaf and
Non-Speaking Users"* (Naba Zahid Khan, Iqra University, Aug 2026).

Translates English, Urdu, and Arabic text into Pakistani Sign Language (PSL),
shown as an animated 2D signer, triggered from a floating button that appears
when text is selected in any Android app.

## Project layout

```
PSLTranslator/
├── backend/     Node.js/Express + SQLite API (language detection, meaning
│                extraction, gloss generation, dictionary, auth, history)
├── android/     Native Kotlin Android app (floating accessibility button,
│                overlay avatar, manual translate screen, history)
└── docs/        Full documentation set (Word documents)
```

## Quick start

**Backend:**
```bash
cd backend
cp .env.example .env        # then edit JWT_SECRET
npm install
npm run migrate
npm run seed
npm start                   # http://localhost:3000
```

**Android:** open `android/` in Android Studio, let Gradle sync, then set
your backend URL in `app/src/main/java/.../network/ApiClient.kt`. See
`docs/SetupGuide.docx` for full step-by-step instructions including how the
emulator/device reaches your backend.

## Documentation

See the `docs/` folder for:
- **Architecture.docx** — system design, pipeline stages, how the code maps to the research paper
- **APIReference.docx** — every backend endpoint, request/response shapes
- **DatabaseSchema.docx** — table-by-table schema reference
- **SetupGuide.docx** — full local dev setup, running on a real device
- **PlayStorePublishingChecklist.docx** — everything needed to ship to the Play Store

## Important scope notes

- The sign dictionary (98 signs, 3 languages) and all HamNoSys/animation data
  are a **development seed corpus**, not a linguistically validated PSL
  resource. Per the source paper's own guidance (§6.3), a real deployment
  needs review by certified PSL interpreters and Deaf community consultants.
- The avatar is a 2D stick-figure placeholder (as scoped for this build), not
  the full 3D/SiGML avatar described in the paper's long-term design — the
  data model already supports swapping in `animation_type = 'sigml_avatar'`
  later without a schema change.
