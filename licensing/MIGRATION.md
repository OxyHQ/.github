# Licensing migration analysis

Investigation date: 2026-08-06. Method: `gh api` against `OxyHQ/*`, `npm view`
against every published `@oxyhq/*`, `@syra.fm/*`, and `@alia.onl/*` package, and
a scan of local clones under `~/Oxy` for `package.json` `license` fields,
`LICENSE` files, and installed dependency licenses.

> Not legal advice. A lawyer should review the conclusions before anything is
> relicensed, in particular the copyright ownership findings in Section 3.

## 1. The headline

**The plan is viable. Two things need saying up front, and they point in
opposite directions.**

**First, the current state is already inconsistent and needs fixing regardless.**
Nine `@oxyhq/*` packages are published to npm as **AGPL-3.0-only**. Every Oxy
application already depends on them. Those applications declare themselves
**MIT**. An MIT application that links AGPL libraries and is served over a
network is not an MIT work in any meaningful sense: the combination carries AGPL
obligations. The MIT `LICENSE` files in `Mention`, `CrowdSource`, `Homiio`,
`Allo`, `Syra`, and `tnp` are therefore already inaccurate today.

**Second, Breathe is stricter than what those repositories notionally carry, and
stricter than the AGPL.** The AGPL requires publication of modifications but
lets anyone use the software commercially for free. Breathe requires the same
publication **and** charges for commercial use. So moving the applications to
Breathe is a genuine narrowing for commercial users, not merely a correction of
paperwork. Both things are true at once, and Section 6 works through what it
costs.

**The load bearing step is the opposite move:** the SDK layer has to come back
from AGPL to **Apache-2.0**. Without it nothing can link the SDKs into a Breathe
application, or into anyone else's product, because Breathe and the AGPL are
mutually incompatible.

## 2. Current state, per repository

`gh repo list` reports `licenseInfo: NONE` for every OxyHQ repository, which is
an artefact of that API field. The `/license` endpoint and the files on disk
give the real picture.

### Repositories with a detected LICENSE

| Repository | LICENSE file | `package.json` | Target layer | Move required |
| --- | --- | --- | --- | --- |
| `oxy` (OxyHQServices) | AGPL-3.0 | mixed, see below | **split** | Yes, per package |
| `Bloom` | AGPL-3.0 | `AGPL-3.0-only` | Apache | **AGPL to Apache-2.0** |
| `website` | AGPL-3.0 | `AGPL-3.0-only` | Breathe | AGPL to Breathe |
| `Mention` | MIT | `MIT` | Breathe | MIT to Breathe |
| `CrowdSource` | MIT | `MIT` | Breathe | MIT to Breathe |
| `Allo` | MIT | none / `ISC` / `UNLICENSED` | Breathe | MIT to Breathe |
| `Homiio` | MIT | none / `ISC` / `UNLICENSED` | Breathe | MIT to Breathe |
| `Syra` | MIT | none / `ISC` / `UNLICENSED` / `MIT` | Breathe | MIT to Breathe |
| `tnp` | MIT | none throughout | not assigned | decide |

The three AGPL `LICENSE` files in `oxy`, `Bloom`, and `website` are byte
identical to the canonical FSF text (md5 `eb1e647870add0502f8f010b19de32af`).
They carry **no Oxy copyright line at all**. The AGPL text alone does not say
who owns the work. Fix this when relicensing.

### Repositories with no LICENSE file at all

`Alia`, `Mercaria`, `OxyPay`, `Clarity`, `Space`, `Schedio`, `Moovo`,
`examples`, `engineering`, `Astro`, `OxyOS` and the `OxyOS-*` family, and
`.github` itself.

No license means **all rights reserved**. Nobody may legally use, copy, or
modify them. For public repositories this is a bug. `examples` is the worst
case: public sample code with no license, which means the samples cannot
lawfully be copied, which defeats their purpose. It is on the Apache list for
exactly that reason.

### `oxy` (OxyHQServices) needs splitting, not relicensing

| Package | Now | Target |
| --- | --- | --- |
| `@oxyhq/core` | AGPL-3.0-only | **Apache-2.0** |
| `@oxyhq/services` | AGPL-3.0-only | **Apache-2.0** |
| `@oxyhq/contracts` | AGPL-3.0-only | **Apache-2.0** |
| `@oxyhq/protocol` | AGPL-3.0-only | **Apache-2.0** |
| `@oxyhq/app-preset` | AGPL-3.0-only | **Apache-2.0** |
| `@oxyhq/expo-splash` | AGPL-3.0-only | **Apache-2.0** |
| `create-oxy-app` | AGPL-3.0-only | **Apache-2.0** |
| `@oxyhq/federation` | AGPL-3.0-only | **Apache-2.0**, unassigned, see below |
| `@oxyhq/ship` | AGPL-3.0-only | **Apache-2.0**, unassigned, see below |
| `@oxyhq/api` | AGPL-3.0-only | **Breathe** |
| `@oxyhq/node` | AGPL-3.0-only, `private` | **Breathe** |
| `auth`, `accounts`, `console`, `inbox`, `commons` | no `license` field, `private` | **Breathe**, set the field |
| `test-app-expo`, `test-app-vite`, `email-inbound` | no `license` field, `private` | set `UNLICENSED` |

**`@oxyhq/federation` and `@oxyhq/ship` were not in the founder's list.** Both
are published, non private, AGPL-3.0-only, and consumed as libraries;
`Mention`'s backend imports `@oxyhq/federation` directly. Both should be
Apache-2.0 on the same reasoning as the rest of the SDK layer. **Needs an
explicit decision.**

A repository level `LICENSE` cannot express a split monorepo. `oxy` needs a per
package `LICENSE` in each `packages/*` directory and a root `LICENSE` that
states the split and points at the per package files.

## 3. Can these repositories actually be relicensed?

Relicensing requires owning all the copyright.

| Repository | Human contributors other than Nate Isern | Machine contributors |
| --- | --- | --- |
| `oxy` | none | `cursoragent` (228), `claude` (50), `Copilot` (32), `dependabot` (12), `cursor[bot]` (11), `google-labs-jules[bot]` (3) |
| `Bloom` | **none at all** | none |
| `website` | none | `cursoragent` (4), `cursor[bot]` (4) |
| `Mention` | **`alexlab84` (2)** | `Copilot` (27), `dependabot` (22), `claude` (9) |
| `CrowdSource` | **`alexlab84` (2)** | `Copilot` (27), `dependabot` (16), `claude` (9) |
| all others in scope | none | assorted bots |

Nate Isern commits under five identities: `nate@oxy.so`,
`nate.isern.alvarez@gmail.com`, `lady@oxy.so`, `oxy@oxy.so`, and the GitHub
account `NateIsern`. Confirm in writing that all five are him, particularly
`lady@oxy.so`, which accounts for roughly a third of recent `oxy` commits and is
not linked to a GitHub account.

### The only outside human contributor

**`alexlab84`**, two commits, both titled "I add changes in package.json", the
same two SHAs appearing in both `Mention` and `CrowdSource` because the
repositories share history. Dated 2025-02-26.

Almost certainly not copyrightable: dependency version bumps in a manifest are
facts and formatting, below the threshold of originality in both US and EU law.
But "almost certainly" is not how you want to start a commercial licensing
programme. Cheapest fixes, in order:

1. Email them and ask for a one line license grant. Two commits, one email.
2. If no reply, inspect the two diffs and rewrite those specific lines
   independently, then record that you did.
3. Only if both fail, treat it as a real blocker.

### The machine contributors

`cursoragent`, `claude`, `Copilot`, `dependabot[bot]`, `cursor[bot]`, and
`google-labs-jules[bot]` are AI agents and automation run by Nate, under his
direction, against his repositories. Two independent reasons this is not a
blocker: purely machine generated output is generally not copyrightable at all,
and to the extent any of it is, it belongs to the person who directed and
selected it, not to the vendor whose tool produced it. Cursor, GitHub, Google,
and Anthropic do not claim copyright in their tools' output. `dependabot`
commits are generated lockfile updates.

**Flag it for the lawyer anyway**, and note the volume: `cursoragent` has 228
contributions to `oxy`. Diligence processes ask about this, and the answer
should be written down once rather than reconstructed later.

### Conclusion on ownership

**Nothing is hard blocked.** `Bloom` is cleanest, with a single human
contributor and no bots. `oxy` and `website` are clean of outside humans.
`Mention` and `CrowdSource` need the `alexlab84` question closed, which is one
email.

## 4. Third party copyleft inside the repositories

No vendored GPL or AGPL source was found anywhere outside `node_modules`. The
only copyleft `LICENSE` files present are Oxy's own AGPL files.

| Component | License | Where | Assessment |
| --- | --- | --- | --- |
| `ffmpeg-static` | **GPL-3.0-or-later** | direct dep of `@oxyhq/api` (Breathe layer) | **The one to watch.** Ships a prebuilt ffmpeg binary invoked as a separate process. Separate executables at arm's length are aggregation, not a derivative work, so `@oxyhq/api` is not a GPL derivative. But the binary stays GPL and Oxy must offer its source when distributing it. **Must appear in `NOTICE`.** If anyone ever links `libav*` in process, this becomes a hard blocker on Breathe for `@oxyhq/api`. |
| `@img/sharp-libvips-*` | LGPL-3.0-or-later | `@oxyhq/api`, `commons`, optional peer of `@oxyhq/app-preset` | Native addon loaded as a separate shared library. LGPL permits this in a non LGPL work provided users can relink. Fine under both Apache and Breathe. **`NOTICE` entry with a relinking statement.** |
| `jszip` | MIT **or** GPL-3.0-or-later | `inbox`, `accounts` (private, Breathe layer) | Elect **MIT**. Record the election in `NOTICE`. |
| `node-forge` | BSD-3-Clause **or** GPL-2.0 | transitive, all three repos | Elect **BSD-3-Clause**. Record it. |
| `@zone-eu/mailsplit` | MIT **or** EUPL-1.1+ | transitive in `oxy` | Elect **MIT**. Record it. |
| `@oxyhq/*` at AGPL | AGPL-3.0-only | deps of `oxy` and `website` | Oxy's own code. Disappears when the SDK layer moves to Apache-2.0. |

**No hard blocker found.** Every copyleft component is either dual licensed with
a permissive option, loaded across a process or library boundary, or Oxy's own.

**A standing rule follows:** a Breathe repository may never take a GPL or AGPL
dependency linked in process. Add a CI license check.

## 5. npm consequences

### Nine packages are AGPL on npm right now

Every one started life MIT and was switched:

| Package | Last permissive version | First AGPL version | Latest | Weekly downloads |
| --- | --- | --- | --- | --- |
| `@oxyhq/core` | `12.5.2` (MIT) | `12.5.4` | `19.1.2` | 8,988 |
| `@oxyhq/services` | `22.4.2` (MIT) | `22.5.0` | `27.1.3` | 9,515 |
| `@oxyhq/bloom` | `0.35.5` (MIT) | `0.35.6` | `0.86.0` | 16,678 |
| `@oxyhq/contracts` | `0.17.0` (MIT) | `0.18.0` | `0.24.0` | 14,314 |

Plus `@oxyhq/api`, `@oxyhq/node`, `@oxyhq/protocol`, `@oxyhq/federation`,
`@oxyhq/app-preset`, `@oxyhq/expo-splash`, `create-oxy-app`, and `@oxyhq/ship`.

The switch to AGPL happened inside a **minor** version every time (`12.5.2` to
`12.5.4`, `0.35.5` to `0.35.6`). Anyone with `^12.0.0` in their manifest was
moved from MIT to AGPL by a routine install, with no signal. **Every license
change from here goes out as a major version, with the change in the
changelog.**

### What "already published" means

**A published version's license is permanent and irrevocable.** Anyone who took
`@oxyhq/core@12.5.2` has MIT to that version forever. Anyone who took `19.1.2`
has AGPL to that version forever. Relicensing changes only what future versions
offer.

This cuts both ways, and it is worth being blunt about the second direction:

- **AGPL to Apache-2.0** for the SDK layer is a **strict widening**. Every
  existing user gains rights and loses none. Nobody has to do anything.
- **MIT or AGPL to Breathe** for the applications is a **narrowing, and the
  narrowing is not retroactive.** Every version of `Mention`, `CrowdSource`,
  `Homiio`, `Allo`, `Syra`, and `tnp` published under MIT stays MIT forever, and
  anyone who has a copy may keep using it commercially, for free, indefinitely,
  and may fork it. The same is true of every AGPL version of `website` and the
  SDKs: AGPL permits commercial use at no charge, so an AGPL fork of any of it
  can be run commercially for free forever, provided the forker publishes their
  source. **Breathe binds future versions only.** Its commercial protection is
  worth exactly as much as future versions are worth, which is a real argument
  for doing this now rather than later, and an argument against expecting it to
  protect anything already shipped.

### Would a paid license on an SDK kill adoption?

**Yes, and the numbers say the SDK layer matters more than the applications.**
`@oxyhq/bloom` at 16,678 weekly downloads and `@oxyhq/contracts` at 14,314 are
the most depended on things Oxy publishes. An SDK is not a product you evaluate;
it is a dependency you either can or cannot add. An engineer who has to open a
legal ticket to add a login SDK adds a different login SDK, and Oxy never finds
out it lost them.

This is why the two layer split is the right call, and it is the same reasoning
behind Sentry's Apache SDKs with a source available server.

**The SDK layer is AGPL today, which is already the bad outcome.** AGPL on a
client library bundled into a consumer's app is more hostile to adoption than
Breathe would be on a server, because AGPL is a license lawyers recognise *and*
refuse. Moving that layer to Apache-2.0 is the single highest value action here,
independent of whether Breathe is ever adopted.

**Downstream MIT packages are now inconsistent.** `@oxyhq/crowdsource` (MIT,
4,153 weekly downloads), `@syra.fm/sdk` (MIT, 3,457), and `@oxyhq/pay` (MIT, 2)
are MIT SDKs whose parent applications are heading to Breathe. Decide
deliberately: they belong in the Apache layer, and `@oxyhq/pay` in particular is
a client library, not part of the OxyPay application.

### Packages with no license field at all

| Package | Weekly downloads | Problem |
| --- | --- | --- |
| **`@alia.onl/sdk`** | **9,821** | Published, public, **no `license` field**. Legally all rights reserved. Nearly ten thousand weekly downloads of a package nobody has permission to use. |
| `@syra/backend`, `@allo/backend`, `@homiio/backend`, `@schedio/backend` | low | Published non private with `ISC`, probably a scaffolding default |
| `@syra/shared-types`, `@allo/shared-types`, `@homiio/shared-types`, `@homiio/listing-providers`, `@schedio/shared-types`, `@oxypay/backend` | low | Published non private as `UNLICENSED` |

**`@alia.onl/sdk` is the most urgent item in this document** and has nothing to
do with the Breathe License. Fix it now: `Apache-2.0` if it is meant to be a
client SDK, or `UNLICENSED` and `"private": true` if it is not meant to be
public.

## 6. The adoption trade off

The founder's stated top priority is building a contributor community. The
honest position, and it got harder with the final design.

**A non OSI license measurably reduces contribution and corporate adoption.**
The mechanism is procedural, not ideological. A company's dependency policy is
usually an allowlist of SPDX identifiers checked automatically in CI. Apache-2.0
and MIT pass silently. An unrecognised identifier fails the check and creates a
ticket for a lawyer who has never heard of Oxy, has no precedent to reuse, and
whose default answer to unquantified risk is no.

**The final design is stricter than the version first drafted, and the cost is
higher.** The earlier draft was conventional dual licensing: copyleft by
default, pay to close your source. Under that model a company could adopt Oxy
software commercially for free by simply complying with the copyleft, which is a
decision an engineer can make alone. Under the final design **any** commercial
use requires a paid license, including purely internal use. That is a decision
that requires procurement, a budget line, and a signature, and it must happen
before the first line of integration code. The set of companies that will do
that for an unproven dependency is much smaller than the set that will comply
with a copyleft.

Three specific consequences worth stating plainly:

1. **It is not open source, and the reason is Section 2, not the copyleft.**
   Charging for commercial use is discrimination against a field of endeavour
   under clause 6 of the Open Source Definition. Copyleft is fine; the AGPL is
   OSI approved. This means Oxy cannot describe these repositories as open
   source, cannot list them in open source directories, and will be corrected in
   public if it tries.
2. **Contributors are harder to attract than under any copyleft license.**
   People contribute to software they can use. A developer who would happily fix
   a bug in an AGPL project may decline when their employer cannot use the
   result without buying a license, and many will decline to sign a CLA that
   lets a company charge for their donated work. There is no clever answer to
   that objection.
3. **The commercial protection is prospective only.** As Section 5 explains,
   every MIT and AGPL version already published stays that way forever and can
   be forked and run commercially for free. Breathe protects future work.

**Against all that:** Oxy has essentially no outside contributors today. One
person, `alexlab84`, with two `package.json` edits, across the entire
organisation. The contributor community is a goal, not a thing currently being
risked. The cost of a non OSI license is paid in a future that has not happened
yet, while the revenue it protects is available immediately. That is a
defensible trade for the **applications**, so long as it is made with open eyes.

**Recommendation, which is what the two layer split delivers:**

- **Keep permissive, and make more permissive than today:** everything a third
  party must depend on. `@oxyhq/core`, `@oxyhq/services`, `@oxyhq/contracts`,
  `@oxyhq/protocol`, `@oxyhq/app-preset`, `@oxyhq/expo-splash`,
  `create-oxy-app`, `@oxyhq/federation`, `@oxyhq/ship`, `@oxyhq/pay`, `Bloom`,
  and `examples`. This is where community forms, and it is worthless as revenue
  protection because its value lies in being adopted.
- **Breathe for the applications and servers:** `@oxyhq/api`, `@oxyhq/node`,
  `website`, `Mention`, `CrowdSource`, `Syra`, `Mercaria`, `Homiio`, `Moovo`,
  `Space`, `Allo`, `Alia`, `OxyPay`. Nobody links an application into their
  product, so the adoption cost is much lower and the revenue protection is
  real.

**If the contributor community goal ever outranks the revenue goal**, the single
change with the largest effect would be dropping the commercial use trigger from
Section 2 and returning to copyleft with a paid escape from the source
obligation. That is the conventional dual license, it is OSI compatible in its
free arm, and it was explicitly rejected. It is recorded here so the decision
stays visible rather than becoming an accident.

## 7. Whether a CLA is needed

**Yes, and before the next outside contribution, not after.**

Dual licensing works only if Oxy owns the copyright in the whole work. A single
merged patch Oxy does not own makes the Commercial Terms unofferable for that
repository. This is a one way door: the contributor may become unreachable, and
until they are found the commercial arm for that repository is dead.

A DCO is not sufficient. It certifies the contributor had the right to submit
under the project's license. It does **not** grant Oxy the right to license the
work commercially on separate terms. Only a CLA with an explicit sublicensing
grant, or an outright assignment, does that.

**Lightest workable mechanism**, in [`CLA.md`](CLA.md):

1. A one page CLA granting Oxy a broad copyright and patent license including
   the right to sublicense. A license grant, not an assignment, so contributors
   keep ownership of their own work.
2. CLA Assistant, a free GitHub app: comments on the first pull request, takes a
   signature by clicking, stores signatures in a repository. Roughly thirty
   minutes to set up organisation wide.
3. A required status check so an unsigned pull request cannot merge.
4. Nate's own contributions do not need it.
5. **The Apache layer does not need a CLA.** Apache-2.0 Section 5 already
   provides an inbound grant, and keeping the barrier low there is the whole
   point of that layer being permissive. A DCO is enough.

Do this **before** announcing the license change, because the announcement is
what draws the first outside pull requests.

## 8. Recommended plan, in order

**Phase 0, this week, independent of everything else.**

1. Fix `@alia.onl/sdk`: no license, 9,821 weekly downloads.
2. Audit every `package.json` with a missing, `ISC`, or `UNLICENSED` value and
   set it deliberately.
3. Add a copyright line naming the owner to each existing `LICENSE`.
4. Confirm the five git identities are all Nate.
5. **Name the copyright holder consistently.** The licensor is **The Oxy
   Foundation, Inc.**, and every document here now says so. The existing MIT
   files still say "OxyHQ" and "Oxy HQ" inconsistently, so they need updating
   to match. Two things remain open before the commercial arm can invoice:
   the jurisdiction of incorporation and the registration number, both still
   placeholders in the Parameters table of each work. Only a real legal person
   can grant a commercial license or take payment for one.

**Phase 1, ownership.** Set up the CLA and CLA Assistant on the Breathe layer.
Close the `alexlab84` question with one email.

**Phase 2, the SDK layer to Apache-2.0.** Highest value, lowest risk, since
widening harms nobody. Major version each, with `NOTICE` files. Do this
**before** Phase 3: a Breathe application cannot legally depend on an AGPL SDK.

**Phase 3, the application layer to Breathe.** Only after Phase 2 lands and the
SDKs have propagated. Major version bumps, changelog entries, and a written
announcement stating plainly that commercial use now requires a license, that
existing versions keep their old license forever, and that source publication
and attribution apply to everyone including paying customers.

**Phase 4, enforcement machinery.** CI checks for the layer boundary and for GPL
and AGPL dependencies in Breathe repositories. Publish the Fee Schedule and the
Exemption Policy. Set up the commercial licensing contact address and a process
for answering "is my use commercial" questions, because there will be many.

**Have a lawyer review before Phase 3.** Phases 0 to 2 are hygiene and widening,
both low risk. Phase 3 creates a commercial licensing programme with a
noncommercial restriction, which is the part that needs more than good drafting
from templates.

## 9. Blockers, in priority order

1. **No confirmed legal entity.** Only a real legal person can offer the
   Commercial Terms or invoice for them. **Blocks the entire commercial arm.**
2. **No CLA.** Blocks accepting any outside contribution to a Breathe repository
   without permanently breaking the commercial arm for it. A DCO is not enough.
3. **The SDK layer is AGPL on npm.** Blocks Phase 3 outright, since Breathe and
   the AGPL are incompatible. Also the current largest drag on adoption, at
   roughly 50,000 combined weekly downloads.
4. **`@alia.onl/sdk` published with no license.** 9,821 weekly downloads nobody
   has permission to use. Independent of this project and the fastest fix here.
5. **`alexlab84`'s two commits** in `Mention` and `CrowdSource`. Probably not
   copyrightable; one email closes it.
6. **`ffmpeg-static` (GPL-3.0-or-later) in `@oxyhq/api`.** Not a blocker today,
   because it runs as a separate process. Hard blocker the moment anyone links
   ffmpeg in process. Needs a `NOTICE` entry and a CI rule.
7. **Undocumented dual license elections:** `jszip`, `node-forge`,
   `@zone-eu/mailsplit`. Audit findings rather than blockers. Fixed by `NOTICE`.
8. **Repositories with no LICENSE at all.** All rights reserved by default.
   `examples` is the worst case: public sample code nobody may lawfully copy.
9. **`@oxyhq/federation`, `@oxyhq/ship`, and `@oxyhq/pay` unassigned.** Published
   libraries not clearly placed in either layer. Recommended Apache-2.0. Needs a
   decision.
10. **The layer boundary is unenforced.** Clean today, verified: no SDK package
    depends on `@oxyhq/api` or `@oxyhq/node`. Nothing stops that changing next
    week except a CI check that does not exist.
11. **No answer yet to "is my use commercial".** A revenue trigger generates
    questions that a copyleft trigger does not, and the first hundred will
    arrive by email. Publishing the Fee Schedule plus a short worked examples
    page will cost less than answering them one at a time.

## Appendix: license naming

The chosen name is **The Breathe License**, identifier
`LicenseRef-Breathe-1.0`, tagline **"free to breathe, paid to bottle"**.

Oxy is named for oxygen, on the reasoning that oxygen is essential and shared.
The name carries that through: breathing, meaning using, studying, changing, and
sharing in the open, is free and always will be, and bottling it to sell is the
part that costs money. The tagline states the whole commercial model in five
words, which is more than most license names manage, and it stayed accurate
through a substantial redesign of the terms.

Two alternatives were considered and rejected:

- **The Element Eight License.** Oxygen's atomic number. Original, memorable,
  unlikely to collide with anything. Rejected because it is opaque: it tells a
  reader nothing about the terms, so every reader must look it up, and opaque
  names add exactly the legal review friction the two layer split exists to
  avoid.
- **The Vital Commons License.** "Vital" for life sustaining, "commons" for a
  shared resource with rules. Reads immediately as a reciprocal sharing license.
  Rejected because "Commons" reads as the Creative Commons family and implies an
  affiliation that does not exist, and because "Commons" is already heavily used
  in license naming, making it the least distinctive of the three.

No existing software license or obvious trademark was found using any of the
three names.
