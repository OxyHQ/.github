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
depends on whether the code is something **you build with** or something **Oxy
runs**.

| | SDK and client layer | Server and application layer |
| --- | --- | --- |
| License | **Apache-2.0** | **The Breathe License 1.0** |
| Open source? | Yes, OSI approved | **No.** Source available |
| Cost | Free, always | Free unless your use earns revenue |
| Must publish source | No | **Yes, always, everyone** |
| Must credit Oxy | No, beyond the Apache notice | **Yes, always, everyone** |

**Why the SDK layer is Apache-2.0 and not Breathe, in one sentence:** if
integrating Oxy login cost money, nobody would integrate it.

**Apache-2.0:** `@oxyhq/core`, `@oxyhq/services`, `@oxyhq/contracts`,
`@oxyhq/protocol`, `@oxyhq/app-preset`, `@oxyhq/expo-splash`, `create-oxy-app`,
`examples`, `Bloom`. Also recommended, pending a decision: `@oxyhq/federation`,
`@oxyhq/ship`, and `@oxyhq/pay`, the OxyPay SDK, which is a client library and
belongs with the SDKs rather than with the OxyPay application.

**Breathe:** `@oxyhq/api`, `@oxyhq/node`, `website`, `Mention`, `CrowdSource`,
`Syra`, `Mercaria`, `Homiio`, `Moovo`, `Space`, `Allo`, `Alia`, `OxyPay`.

**Watch the boundary.** An Apache-2.0 package must never depend on a Breathe
package. The reverse is fine. As of this analysis the boundary is clean: no SDK
layer package depends on `@oxyhq/api` or `@oxyhq/node`. Enforce it in CI before
it breaks.

## What the Breathe License says

Read it: [`../LICENSE-BREATHE.md`](../LICENSE-BREATHE.md). In summary.

**Free, for anything that is not commercial.** Run it, read it, change it, fork
it, share it, teach with it, research with it, build hobby projects on it, and
evaluate it inside a company for ninety days. No fee, ever, and the grant is
perpetual and irrevocable while you comply.

**Two conditions, on everybody, with no exceptions:**

1. **Publish the source.** If you deploy the software or a modified version,
   whether you ship it or serve it over a network, you make the corresponding
   source available. **This obligation is not for sale.** There is no fee that
   buys release from it, and Oxy will not offer one.
2. **Credit Oxy.** One reachable place per work: an About, Credits, or Licenses
   screen. Not the home page, not a splash screen, not advertising.
   **Attribution cannot be waived by agreement or by payment**, and any contract
   term purporting to waive it is void under Section 3.1.

**Commercial use requires a paid license.** The trigger is **revenue**, not the
desire to close the source. If your use is connected to money coming in, you
need the [Commercial Terms](../LICENSE-COMMERCIAL.md). That explicitly includes
**internal use**: if your company earns revenue and uses the software in the
course of earning it, that is commercial use even if the software never touches
a customer.

**What the Commercial Terms buy: the right to use it commercially, and nothing
else.** They do not release you from publishing source. They do not release you
from attribution. They do not let you make the software or your changes
proprietary. There is no proprietary arm, at any price.

**Zero fee for cooperatives, nonprofits, educational institutions, public
bodies, and worker owned businesses.** They are exempt from the **fee** and from
nothing else: they publish source and give credit like everyone else. See
[`EXEMPTIONS.md`](EXEMPTIONS.md).

**Your own separate program is not caught.** Section 3.5: using the software
only through its documented public interfaces does not make your program a
modified version. Calling the API, importing an SDK, writing a plugin against a
documented interface, and deploying alongside your own programs are all outside
the copyleft, and your program stays yours under whatever license you like.

## FAQ

### Is the Breathe License open source?

**No.** It is source available, and it is worth being precise about why, because
the obvious guess is wrong.

It is **not** because of the copyleft. The AGPL is copyleft, including over a
network, and the AGPL is OSI approved. Requiring people to publish their
modifications is entirely compatible with the Open Source Definition.

It fails on **clause 6 of the Open Source Definition, discrimination against
fields of endeavour**. Section 2 of the license makes commercial use conditional
on a paid license, and "no discrimination against fields of endeavour" exists
precisely to forbid "free for non-commercial use, pay for business use". This
is the same reason PolyForm Noncommercial and the Anti-Capitalist Software
License are not open source, and it applies regardless of how reasonable the
underlying intent is.

It follows that:

- The Breathe License is not OSI approved and not FSF approved, and will not be.
- It is not on the SPDX license list. GitHub shows it as **"Other"** or
  **"custom"**, and automated scanners report it as unknown, which in many
  companies routes it to a legal team rather than to an engineer.
- **Nobody should call software under this license open source.** The correct
  words are "source available".

For the record, the alternative design that was considered and rejected: a
conventional dual license, where the source obligation itself is what a
commercial licensee buys out of. That version **would** have been ordinary
dual licensing of the kind MySQL and Qt have used for decades. It was rejected
deliberately, because it lets a paying company take the work private, and
keeping the source public in every hand was the higher priority. The
consequence is documented here rather than argued about in the license text.

**The SDK layer is genuinely open source**, because Apache-2.0 is. That is
deliberate, and it is the answer to the adoption problem this whole section
describes.

### Is it compatible with the GPL or the AGPL?

**No.** Code under the GPL or AGPL cannot be combined into a Breathe work, and a
Breathe work cannot be combined into a GPL or AGPL work. Both of those licenses
forbid adding restrictions, and requiring payment for commercial use is a
restriction.

Consequences for Oxy specifically:

- Every SDK layer package is published on npm as **AGPL-3.0-only** today.
  Relicensing them to Apache-2.0 is a **hard precondition**, not cleanup: a
  Breathe application cannot legally depend on an AGPL library.
- A Breathe repository may never take on a GPL or AGPL dependency that links in
  process. The one live case, `ffmpeg-static` in `@oxyhq/api`, survives only
  because it invokes a separate executable.

### Do I have to pay if I make money with Oxy software?

**Yes.** That is the trigger. If your use is connected to revenue, directly or
indirectly, you need the Commercial Terms. Internal business use counts.

### If I pay, can I keep my changes private?

**No.** This is the question the license is built to answer, and the answer does
not change with the size of the cheque. Publishing the corresponding source
applies to paying licensees in full, and Oxy will not offer any arrangement that
removes it.

### If I pay, do I still have to credit Oxy?

**Yes.** Attribution is mandatory for everyone, including paying commercial
licensees, and it cannot be waived by agreement. Section 3.1 of the license and
the Commercial Terms both say so, and the Commercial Terms make any contrary
contract provision void. Paying does not buy anonymity.

### If I stop paying, do I lose access?

You lose the right to use it **commercially**, and you must stop commercial use.
Your license for permitted purposes continues, so you can still read, study,
modify, and run it non commercially.

### Can Oxy revoke it?

Not while you comply. The Section 2 grant is perpetual and irrevocable for as
long as you meet the Section 3 conditions. Oxy can change the license of future
versions, and cannot change it for versions already published.

### Is this stricter than the AGPL?

Yes, deliberately, and in one direction only. The AGPL requires you to publish
your modifications but lets anyone use the software commercially for free.
Breathe requires the same publication **and** charges for commercial use. A
company that is comfortable with the AGPL is not automatically comfortable with
this.

## Third party components: what the clause fixes and what it does not

Both documents carry a **Third Party Components** clause and a **severability**
clause. They say the Oxy terms cover only the parts Oxy owns, that third party
components stay under their own licenses, and that nothing in the Oxy terms
reduces the rights those licenses grant. Each repository lists what it carries
in a `NOTICE` file, per [`NOTICE.template`](NOTICE.template).

**What it fixes.** A repository that *contains* independently licensed files
alongside Oxy's own code: a vendored MIT utility, a BSD font, an Apache-2.0
helper, a CC-BY icon set. Separate works that happen to travel together. The
clause makes explicit that Oxy is not purporting to relicense them, that your
rights under their own licenses are untouched, and, importantly here, that a
permissively licensed component stays usable by you commercially under its own
terms whether or not you hold the Commercial Terms for the Oxy work.

**What it does not fix.** It does **not** rescue a work that is a *derivative*
of copyleft code. If GPL or AGPL code is combined into a work such that the
combination is a derivative or covered work, the copyleft governs the **whole
combination**. Copyleft attaches to the combination, not to individual files, so
no third party components clause can carve Oxy's contributions back out of it.
Where that happens, Oxy cannot license the combination under Breathe at all.

That is exactly where the migration work lives. Read
[`MIGRATION.md`](MIGRATION.md) before applying anything.

## Why a CLA is mandatory

**Only the copyright holder can offer a second license.** The moment a patch Oxy
does not own lands in a Breathe repository, Oxy can no longer offer the
Commercial Terms for it, because Oxy cannot license out somebody else's
copyright. One merged pull request from an outside contributor, with no agreement
in place, breaks the commercial arm for that repository permanently, or until
that person is found and asked.

It also matters for the Apache layer, though less severely: relicensing the SDKs
from AGPL to Apache-2.0 requires owning them too.

This is a precondition, not a footnote. See [`CLA.md`](CLA.md).

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

Apache-2.0 has its own `NOTICE` semantics: whatever you put there must be
reproduced by downstream users. Keep it to attribution, not commentary.

### License identifier

| Layer | `package.json` `license` | SPDX / SBOM |
| --- | --- | --- |
| Apache | `"Apache-2.0"` | `Apache-2.0` |
| Breathe, published to npm | `"SEE LICENSE IN LICENSE"` | `LicenseRef-Breathe-1.0` |
| Breathe, private package | `"UNLICENSED"` | `LicenseRef-Breathe-1.0` |

`LicenseRef-Breathe-1.0` is for SBOMs and scanners. Do not put it in
`package.json`; npm expects an SPDX expression or `SEE LICENSE IN <file>`, and a
`LicenseRef-` value there makes tooling report the package as malformed rather
than as custom licensed.

Never leave the `license` field empty. A missing field means all rights reserved
by default, which is almost never intended. Several Oxy packages are in that
state today; see [`MIGRATION.md`](MIGRATION.md).

### Source file headers

```ts
// Copyright (c) <YEARS> <LEGAL ENTITY NAME>
// SPDX-License-Identifier: LicenseRef-Breathe-1.0
// Licensed under the Breathe License 1.0. Commercial use requires a paid
// license. Source publication and attribution are required of everyone.
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

Free to run, read, modify, fork, and share, for any purpose that is not
commercial. Two conditions on everyone: publish the source of what you deploy,
and credit Oxy in one reachable place. Neither can be bought out of.

**Commercial use requires a paid license.** The trigger is revenue, including
internal use inside a business that earns it. See the
[Commercial Terms](./LICENSE-COMMERCIAL.md). Paying buys the right to use it
commercially; it does not let you keep your changes private and it does not
remove attribution.

Cooperatives, nonprofits, educational institutions, and public bodies pay
nothing. They publish source and attribute like everyone else. See the
[Exemption Policy](https://github.com/OxyHQ/.github/blob/main/licensing/EXEMPTIONS.md).

The Breathe License is **source available, not open source**. It is not OSI
approved, because charging for commercial use is discrimination against a field
of endeavour under clause 6 of the Open Source Definition. Oxy's SDKs and client
libraries are Apache-2.0, so building **against** Oxy carries none of this.
```

### Checklist before applying either license

1. Confirm Oxy owns all copyright in the repository, or holds a signed CLA from
   everyone who contributed anything copyrightable.
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
  throughout. PolyForm Noncommercial is also the closest existing analogue to
  the commercial use trigger in Section 2, and PolyForm Small Business is the
  model for expressing that trigger as a condition on the grant rather than as
  a restriction bolted on afterwards.
- **The Permitted Purpose and Commercial Use enumerations:** the Functional
  Source License 1.1, whose enumerated approach is the clearest in the field.
  Sections 2.2 and 2.3 follow its structure of stating the general test and then
  listing what specifically falls on each side of it.
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
- **The exemption categories:** the Cooperative Software License and the Anti
  Capitalist Software License, the two serious attempts to define mission
  aligned organizations in license text. Neither was used as the base document,
  because both make the exemption a **restriction** on who may use the software
  at all. Here the same categories appear as a **fee exemption**, so a
  cooperative is relieved of the fee rather than a corporation being forbidden
  the software.
