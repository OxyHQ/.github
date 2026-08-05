# Oxy licensing

**Free to breathe, paid to bottle.**

> **Status: proposal.** Nothing here changes the license of any Oxy repository.
> The pull request that introduced these documents does not modify any other
> repository's `LICENSE` file. This is a draft for review.
>
> **Not reviewed by a lawyer.** These documents were drafted from established
> templates, which is not the same as legal advice and is no substitute for it.
> Have a qualified lawyer in the relevant jurisdiction review them before
> applying them to any work that matters commercially.

## Two layers, two licenses

Oxy does not use one license for everything. It uses two, and which one applies
depends on whether the code is something **you build with** or something
**Oxy runs**.

| | SDK and client layer | Server and application layer |
| --- | --- | --- |
| License | **Apache-2.0** | **The Breathe License 1.0** |
| Open source? | Yes. OSI approved | No. Source available |
| Why | If wiring Oxy login into your app obliged you to pay or to open your source, nobody would wire it in, and the ecosystem dies at the first integration | These are the products. Copyleft keeps improvements in the commons; the commercial arm funds the work |
| Copyleft | None | Yes, including over a network |
| Paying | Never | Only to keep your changes closed |

This is the split Sentry uses: permissive SDKs, a source available server. It is
the split that lets a third party adopt Oxy without a legal review, while still
giving Oxy something to sell.

### The SDK and client layer: Apache-2.0

Everything a third party has to link into their own product.

| Repository or package | Why it is here |
| --- | --- |
| `@oxyhq/core` | The client SDK every Oxy integration imports |
| `@oxyhq/services` | The React Native and web SDK, imported directly into consumer apps |
| `@oxyhq/contracts` | Shared types, imported by every consumer at compile time |
| `@oxyhq/protocol` | Wire protocol definitions; a protocol nobody may implement freely is not a protocol |
| `@oxyhq/app-preset` | Build configuration consumed by third party apps |
| `@oxyhq/expo-splash` | A drop in Expo component |
| `create-oxy-app` | A scaffolder; its output must be freely licensable by whoever runs it |
| `OxyHQ/examples` | Sample code exists to be copied, so its license must permit copying |
| `OxyHQ/Bloom` (`@oxyhq/bloom`) | The UI component library; components are compiled into the consumer's bundle |

**Two packages the founder's list did not assign, needing a decision.** Both
are published, both are consumed as libraries, and both should go Apache-2.0 on
the same reasoning:

- `@oxyhq/federation`, currently AGPL-3.0-only, already imported directly by
  `Mention`'s backend. It is a library, not a service.
- `@oxyhq/ship`, currently AGPL-3.0-only. Developer tooling that runs inside
  other people's builds.

### The server and application layer: the Breathe License

Everything Oxy operates or ships as a product.

| Repository or package | |
| --- | --- |
| `@oxyhq/api` | The Oxy platform API server |
| `@oxyhq/node` | The self hostable Oxy node |
| `OxyHQ/website` | oxy.so |
| `OxyHQ/Mention` | Social and fediverse app |
| `OxyHQ/CrowdSource` | Crowdsourcing platform |
| `OxyHQ/Syra` | |
| `OxyHQ/Mercaria` | Marketplace |
| `OxyHQ/Homiio` | Real estate |
| `OxyHQ/Moovo` | Delivery and fleet |
| `OxyHQ/Space` | |
| `OxyHQ/Allo` | Encrypted messaging |
| `OxyHQ/Alia` | AI platform |
| `OxyHQ/OxyPay` | Payments |

**Watch the boundary.** An Apache-2.0 package must never depend on a Breathe
package. The reverse is fine. As of this analysis the boundary is clean: no SDK
layer package depends on `@oxyhq/api` or `@oxyhq/node`. Enforce it in CI before
it breaks. See [`MIGRATION.md`](MIGRATION.md).

One exception worth calling out: `@oxyhq/pay`, the OxyPay **SDK**, is MIT today
and is a client library. It belongs in the SDK layer, not with the OxyPay
application. Move it to Apache-2.0, not Breathe.

## What the Breathe License actually says

Read it: [`../LICENSE-BREATHE.md`](../LICENSE-BREATHE.md). In summary.

**You get, for free, forever, with no fee ever:** the right to run, study, copy,
modify, and redistribute the software, for any purpose, including running a
business on it. Commercial use is free. There is no revenue threshold, no user
cap, and no trial period.

**You owe three things:**

1. **Attribution.** Credit Oxy in one reachable place. An About or Licenses
   screen is enough. Not the home page, not a splash screen, not advertising.
2. **Source on conveyance.** If you ship it to someone, they can get the source
   of what you shipped.
3. **Source on network use.** If you modify it and let others use your modified
   version over a network, publish your changes. This is the network copyleft
   condition, modelled on AGPL-3.0 Section 13 but written in original words.

**Your own separate program is not caught.** Section 3.5 of the license says
that using the software only through its documented public interfaces does not
make your program a modified version. Calling the API, importing an SDK, writing
a plugin against a documented plugin interface, and deploying alongside your own
programs are all explicitly outside the copyleft. This is the clause that makes
the boundary between your code and Oxy's code predictable.

**What costs money:** enclosing it. If you want to build Oxy code into a
proprietary product, ship it in object form only, or run a modified version as a
service without publishing your changes, you take the
[Commercial Terms](../LICENSE-COMMERCIAL.md) instead. Free to breathe, paid to
bottle.

**Who pays nothing for that too:** cooperatives, nonprofit organizations,
educational institutions, public bodies, and worker owned businesses. They get
the Commercial Terms at no charge. See [`EXEMPTIONS.md`](EXEMPTIONS.md).

## FAQ

### Is the Breathe License open source?

**No.** It is source available. The Breathe License is not approved by the Open
Source Initiative and not approved by the Free Software Foundation. It is not on
the SPDX license list. GitHub will show a repository using it as **"Other"** or
**"custom"**, and automated license scanners will report it as unknown, which in
many companies routes it to a legal team rather than to an engineer.

Anyone telling you an Oxy application is open source because you can read the
source is using the wrong word. The correct words are "source available".

The **SDK layer is genuinely open source**, because Apache-2.0 is. That is
deliberate, and it is the answer to the adoption problem the paragraph above
describes: the code third parties must actually depend on carries a license
their lawyers already approved years ago.

### Is it compatible with the GPL or the AGPL?

**No.** Code under the GPL or the AGPL cannot be combined into a work under the
Breathe License, and a Breathe work cannot be combined into a GPL or AGPL work.
The licenses impose conditions each other's terms forbid.

This is a hard constraint with real consequences for Oxy:

- Every package in the SDK layer is published on npm as **AGPL-3.0-only**
  today. Relicensing those to Apache-2.0 is what makes the whole plan possible;
  it is not optional cleanup. An AGPL SDK cannot be linked into a Breathe
  application any more than into anyone else's proprietary one.
- A Breathe repository may not take on a GPL or AGPL dependency, ever. The one
  live case, `ffmpeg-static` in `@oxyhq/api`, survives only because it invokes a
  separate executable rather than linking. Treat that as a line not to cross.

This incompatibility is the price of an original license text. It is the reason
the SDK layer is Apache-2.0 and not Breathe.

### Do I have to pay if I make money with Oxy software?

No. Commercial use is licensed free of charge. You pay only if you want to keep
your modifications closed. The Commercial Terms are an escape from the source
availability conditions, not a toll on revenue.

If the intent is instead that revenue itself should trigger a fee, the license
would need a different Section 2, and the Commercial Terms would become
mandatory above a threshold rather than optional. That is a coherent design too,
and PolyForm Small Business is the template for it, but it is not what is
drafted here. Flagging it explicitly so the choice is a conscious one.

### If I stop paying, do I lose access?

No. You fall back to the free Breathe Terms, and their conditions apply from
that point forward. You never lose the right to use the software. What you lose
is the right to keep your changes private.

### Can Oxy revoke it?

Not while you comply. The grant in Section 2 is perpetual and irrevocable for as
long as you meet the conditions in Section 3. Oxy can change the license of
future versions, and cannot change it for versions already published.

## Third party components: what the clause fixes and what it does not

Both documents carry a **Third Party Components** clause and a **severability**
clause. They say the Oxy terms cover only the parts Oxy owns, that third party
components stay under their own licenses, and that nothing in the Oxy terms
reduces the rights those licenses grant. Each repository lists what it carries
in a `NOTICE` file, per [`NOTICE.template`](NOTICE.template).

**What it fixes.** The ordinary case: a repository that *contains*
independently licensed files alongside Oxy's own code. A vendored MIT utility, a
BSD font, an Apache-2.0 helper, a CC-BY icon set. Separate works that happen to
travel together. The clause makes explicit that Oxy is not purporting to
relicense them and that your rights under their own licenses are untouched.

**What it does not fix.** It does **not** rescue a work that is a *derivative*
of copyleft code. If GPL or AGPL code is combined into a work such that the
combination is a derivative or covered work, the copyleft governs the **whole
combination**. Copyleft attaches to the combination, not to individual files, so
no third party components clause can carve Oxy's own contributions back out of
it. Where that happens, Oxy cannot license the combination under Breathe at all,
and cannot offer the Commercial Terms for it, because Oxy does not hold the
right to do so.

That distinction is exactly where the migration work lives. `OxyHQ/oxy`,
`OxyHQ/Bloom`, and `OxyHQ/website` are AGPL-3.0 works today, and every other Oxy
application already depends on AGPL versions of `@oxyhq/core`,
`@oxyhq/services`, or `@oxyhq/bloom`. Those are combinations involving AGPL
code right now. They are relicensable only because Oxy owns the copyright in all
of it, not because of the third party components clause. Read
[`MIGRATION.md`](MIGRATION.md) before applying anything.

## Why a CLA is mandatory

**Only the copyright holder can offer a second license.** That is the entire
mechanism behind the Breathe and Commercial pairing. The moment a patch Oxy does
not own lands in a Breathe repository, Oxy can no longer offer the Commercial
Terms for it, because Oxy cannot license out somebody else's copyright. One
merged pull request from an outside contributor, with no agreement in place,
breaks the commercial arm for that repository permanently, or until that person
is found and asked.

It also matters for the Apache layer, though less severely: relicensing the SDKs
from AGPL to Apache-2.0 requires owning them too.

This is a precondition, not a footnote. See [`CLA.md`](CLA.md) for the agreement
and the lightest way to run one.

## Applying a license to a repository

### Breathe layer file layout

```
LICENSE                    <- the Breathe License 1.0, Parameters filled in
LICENSE-COMMERCIAL.md      <- the Commercial Terms, Parameters filled in
NOTICE                     <- third party components, if any
```

### Apache layer file layout

```
LICENSE                    <- verbatim Apache-2.0 text (licensing/Apache-2.0.txt)
NOTICE                     <- third party components, if any
```

Apache-2.0 has its own `NOTICE` semantics: whatever you put in `NOTICE` must be
reproduced by downstream users. Keep it to attribution, not commentary.

### License identifier

| Layer | `package.json` `license` | SPDX / SBOM |
| --- | --- | --- |
| Apache | `"Apache-2.0"` | `Apache-2.0` |
| Breathe, published to npm | `"SEE LICENSE IN LICENSE"` | `LicenseRef-Breathe-1.0` |
| Breathe, private package | `"UNLICENSED"` | `LicenseRef-Breathe-1.0` |

`LicenseRef-Breathe-1.0` is the identifier for SBOMs and scanners. Do not put it
in `package.json`; npm expects either an SPDX expression or `SEE LICENSE IN
<file>`, and a `LicenseRef-` value there makes tooling report the package as
malformed rather than as custom licensed.

Never leave the `license` field empty. A missing field means all rights reserved
by default, which is almost never intended. Several Oxy packages are in that
state today; see [`MIGRATION.md`](MIGRATION.md).

### Source file headers

Optional, worth it only on substantial files.

```ts
// Copyright (c) <YEARS> <LEGAL ENTITY NAME>
// SPDX-License-Identifier: LicenseRef-Breathe-1.0
// Licensed under the Breathe License 1.0. Commercial terms are available.
// https://github.com/OxyHQ/.github/blob/main/LICENSE-BREATHE.md
```

```ts
// Copyright (c) <YEARS> <LEGAL ENTITY NAME>
// SPDX-License-Identifier: Apache-2.0
```

### README section for a Breathe repository

```md
## License

[The Breathe License 1.0](./LICENSE). Free to breathe, paid to bottle.

Free forever, for anyone, for any purpose including commercial. Credit us, and
if you modify it and run it as a service, publish your changes.

To build it into a proprietary product without those conditions, take the
[Commercial Terms](./LICENSE-COMMERCIAL.md). Cooperatives, nonprofits,
educational institutions, and public bodies get those free of charge; see the
[Exemption Policy](https://github.com/OxyHQ/.github/blob/main/licensing/EXEMPTIONS.md).

The Breathe License is **source available, not open source**. It is not OSI or
FSF approved, and GitHub shows it as a custom license. Oxy's SDKs and client
libraries are Apache-2.0, so building **against** Oxy carries no such terms.
```

### Checklist before applying either license

1. Confirm Oxy owns all copyright in the repository, or holds a signed CLA from
   everyone who contributed anything copyrightable. If not, stop and read
   [`MIGRATION.md`](MIGRATION.md).
2. For a Breathe repository, confirm no GPL or AGPL code is combined into the
   work. Check dependencies, not just vendored files.
3. Confirm the layer boundary: no Apache package may depend on a Breathe
   package.
4. Add the license files with all `<PLACEHOLDERS>` filled in.
5. Set the `license` field in every `package.json`.
6. Generate `NOTICE` from [`NOTICE.template`](NOTICE.template).
7. Add the README section.
8. Enable CLA checking on the repository.
9. For a package already on npm under a different license, publish the change as
   a new **major** version and say so in the changelog.

## Where the text came from

Neither document was invented from scratch.

- **Clause skeleton and plain language style:** the PolyForm project licenses,
  in particular PolyForm Noncommercial 1.0.0 and PolyForm Small Business 1.0.0.
  Their ordering (Acceptance, Copyright License, Distribution, Changes and New
  Works, Notices, Patent License, No Other Rights, Patent Defense, Violations,
  No Liability, Definitions) and their 32 day cure period are followed
  throughout. PolyForm is drafted by practising licensing lawyers and is the
  best available model for a readable source available license.
- **The network copyleft obligation:** modelled on AGPL-3.0 Sections 6 and 13.
  The obligation is the same in substance; the wording is original, and the
  Breathe License is not the AGPL and is not presented as such.
- **The interface boundary in Section 3.5:** the GCC Runtime Library Exception
  and the GNU Classpath Exception, which solve the same problem of stopping
  copyleft from reaching a separate program that merely uses a documented
  interface.
- **The Parameters block:** the Business Source License 1.1, which pioneered
  putting the variable terms in a table at the top instead of scattering
  placeholders through the text.
- **The competing and commercial use definitions:** the Functional Source
  License 1.1, whose enumerated approach to "Permitted Purpose" is the clearest
  in the field.
- **The exemption categories:** the Cooperative Software License and the Anti
  Capitalist Software License, which are the two serious attempts to define
  mission aligned organizations in license text. Both were rejected as the base
  document, because both make the exemption a **restriction** on who may use
  the software at all, which would have made Oxy software unusable by ordinary
  companies. Here the same categories appear as a **fee exemption** on an
  optional commercial arm, so nobody is excluded from using the software.
