# FreeAppStore AI Skills

Point your Claude Code or Codex to this file for platform-aware development.

**Add to your CLAUDE.md or agent config:**
```
See https://raw.githubusercontent.com/freeappstore-online/ops/main/SKILLS.md for platform skills.
```

---

## Platform Context

You are building an app for FreeAppStore (freeappstore.online). Follow these rules exactly.

### Platform Rules
- ONE environment: production only. Push to `main` = deploy. No staging, no rollbacks. Fix forward.
- Static hosting on Cloudflare Pages. No server-side code.
- Backend (if needed): Firebase or Supabase only.
- Free means free forever. No monetization in the free version.
- One app per category. Check freeappstore.online for taken categories.

### Tech Stack (required)
- TypeScript ^5.7
- React ^19.0
- Vite ^6.0
- Tailwind CSS ^4.1
- pnpm (workspace with web/ package)
- Node >=22

### Project Structure
```
app-name/
├── package.json           (root workspace)
├── pnpm-workspace.yaml    (packages: [web])
├── LICENSE                (MIT)
├── .github/workflows/compliance.yml
└── web/
    ├── package.json
    ├── index.html
    ├── vite.config.ts
    ├── tsconfig.json
    ├── public/manifest.json
    └── src/
        ├── main.tsx
        ├── index.css      (Tailwind + brand CSS variables)
        ├── App.tsx
        └── components/
```

### Brand Design (mandatory)
- Fonts: Manrope (body, all weights) + Fraunces (display, 700-800)
- CSS Variables: `--paper`, `--ink`, `--muted`, `--line`, `--panel`, `--glass`, `--dock`, `--accent`, `--success`, `--warning`, `--error`
- Layout: Desktop = sidebar (17rem) + main content. Mobile = header + main + bottom dock.
- Dark mode: via `prefers-color-scheme: dark` or `[data-theme='dark']`
- Border radius: 1.25rem (cards), 0.75rem (buttons)
- Transitions: 160ms ease (buttons), 200ms ease (cards)
- Must include "Part of FreeAppStore — free forever" link somewhere in the app

### Privacy Rules
- ZERO analytics, tracking, cookies
- No Google Analytics, Amplitude, Mixpanel, Segment, Hotjar, PostHog, Sentry
- All user data in localStorage (standalone) or Firebase (connected)
- No third-party scripts except Google Fonts CDN

### App Types

**Standalone** (no backend):
- All data in localStorage
- No account required
- Works fully offline
- Template: github.com/freeappstore-online/template-standalone

**Connected** (shared backend):
- Firebase/Supabase for data
- Free + Pro versions share same backend
- Feature gating via user roles in Firestore rules
- Free version must work for browsing without sign-in
- Template: github.com/freeappstore-online/template-connected

### Compliance Checks (automated)
These run on every push to main:
1. Build passes (`pnpm build`)
2. MIT license exists
3. No tracking dependencies or code
4. Manrope + Fraunces fonts in CSS
5. CSS variables (--paper, --ink, --accent) present
6. PWA manifest.json exists
7. "freeappstore.online" link in source
8. Dark mode support
9. pnpm workspace structure
10. Bundle < 300KB gzipped

### Publishing Workflow
1. Build app using template
2. Submit at github.com/freeappstore-online/submissions
3. Review (48h response)
4. Approved → repo transferred to org → CF Pages project created → live at appname.freeappstore.online

### Commands for Development
```bash
pnpm dev          # Start dev server
pnpm build        # Production build
pnpm preview      # Preview production build
```

### Do NOT
- Add dev/staging environments
- Add rollback mechanisms
- Add analytics or tracking
- Add monetization to free version
- Use npm or yarn (pnpm only)
- Use Next.js, Nuxt, or any SSR framework
- Create server-side APIs (use Firebase/Supabase)
- Add CLAUDE.md to the repo (skills are external)
