<p align="center">
  <img alt="Oxy" src="https://github.com/OxyHQ/.github/raw/main/profile/assets/header.svg" width="100%">
</p>

<p align="center">
  <a href="https://oxy.so"><img alt="oxy.so" src="https://img.shields.io/badge/oxy.so-440151?style=flat-square"></a>
  <a href="https://mention.earth/@oxy"><img alt="@oxy on Mention" src="https://github.com/OxyHQ/.github/raw/main/profile/assets/badge-mention.svg" height="20"></a>
</p>

<p align="center">
  <b>We build ethical alternatives to systems that exploit people.</b><br>
  It started in 2011, when a twelve year old opened Facebook, hated what he saw,<br>
  and decided to build his own social network instead.
</p>

---

<table>
<tr>
<td valign="top" width="50%">

### 🧭 What we mean by ethical

**The user is not the product.** No selling personal data. No advertising layers. No design tricks that make leaving hard.

**Open by default.** Read the code, fork it, take your identity elsewhere.

**Limits on us, too.** No secret admin panels where one person removes whatever they feel like. Reports go through a process, evidence gets reviewed, people can appeal.

If the word never costs you anything, it probably doesn't mean very much.

</td>
<td valign="top" width="50%">

### 🔐 One identity, every app

Keys live on the person's device. Records are signed client side, so ownership is proven by cryptography rather than granted by us.

Every app here shares one identity layer, one session model and one UI library, which is why signing in once works everywhere without a single tracking cookie.

Start at [**oxy**](https://github.com/OxyHQ/oxy), the platform the rest stands on.

</td>
</tr>
</table>

## The ecosystem

<table>
<tr>
<td valign="top" width="50%">

**Platform**

| | |
|---|---|
| [oxy](https://github.com/OxyHQ/oxy) | Identity, protocol, API, SDK, and the identity apps |
| [Bloom](https://github.com/OxyHQ/Bloom) | Cross-platform UI library every app is built with |
| [OxyPay](https://github.com/OxyHQ/OxyPay) | Payments platform · [SDK](https://github.com/OxyHQ/OxyPaySDK) |
| [examples](https://github.com/OxyHQ/examples) | Runnable starters: Next.js, Vite, Expo |

**People and speech**

| | |
|---|---|
| [Mention](https://github.com/OxyHQ/Mention) | Social network, connected to the Fediverse |
| [CrowdSource](https://github.com/OxyHQ/CrowdSource) | Participatory moderation: juries, evidence, appeals |
| [Allo](https://github.com/OxyHQ/Allo) | Communication |

</td>
<td valign="top" width="50%">

**Life and work**

| | |
|---|---|
| [Syra](https://github.com/OxyHQ/Syra) | Music: artists, albums, live |
| [Mercaria](https://github.com/OxyHQ/Mercaria) | Marketplace: shops and second hand |
| [Homiio](https://github.com/OxyHQ/Homiio) | Housing |
| [Moovo](https://github.com/OxyHQ/Moovo) | Courier and transport |
| [Space](https://github.com/OxyHQ/Space) | Docs, databases, collaboration |
| [Schedio](https://github.com/OxyHQ/Schedio) | Design and prototyping |

**Systems and tools**

| | |
|---|---|
| [Alia](https://github.com/OxyHQ/Alia) | AI assistant platform |
| [OxyOS](https://github.com/OxyHQ/OxyOS) | Desktop operating system |
| [Astro](https://github.com/OxyHQ/Astro) | Browser |
| [Codea Studio](https://github.com/OxyHQ/CodeaStudioCode) | AI code editor |

</td>
</tr>
</table>

## Build on Oxy

```bash
bun add @oxyhq/services   # Expo, React Native and web, through React Native Web
bun add @oxyhq/core       # API client, session engine, types, for any JavaScript runtime
```

```tsx
import { OxyProvider } from "@oxyhq/services";

<OxyProvider clientId={process.env.OXY_CLIENT_ID} baseURL="https://api.oxy.so">
  <App />
</OxyProvider>
```

One provider covers web and native. Cold boot restores the session silently and never redirects anyone to a login page.

## Come build with us

The hard part is no longer the infrastructure. It is the community around it.

We need developers, artists for Syra, sellers for Mercaria, researchers willing to attack the reputation design and tell us where it turns ugly, translators, organisers, moderators, people who know housing and education, and people who know how to build institutions, which is a different skill from building software.

You don't have to agree with us about everything. We specifically need people who will say when something is badly designed, or when an ethical idea creates a different kind of harm.

- [Engineering standards](https://github.com/OxyHQ/engineering) — conventions, tooling, onboarding
- [Contributing](https://github.com/OxyHQ/.github/blob/main/CONTRIBUTING.md) · [Security policy](https://github.com/OxyHQ/.github/blob/main/SECURITY.md) · [Code of conduct](https://github.com/OxyHQ/.github/blob/main/CODE_OF_CONDUCT.md)

<br>

<div align="center">
<sub><em>Oxy didn't appear because somebody spotted a market trend.<br>It started because something felt wrong and building an alternative seemed worth trying.</em></sub>
<br><br>
<sub>Licences are per repository. The platform is AGPL-3.0-only.</sub>
</div>
