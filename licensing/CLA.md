# Contributor License Agreement

> **Status: drafted, not switched on.** The text below is settled on the one
> question that used to block it: the entity contributions are licensed to is
> **The Oxy Collective, Inc.**, which exists today. **No bot is installed and no
> signature has been taken**, and turning one on is a separate decision that
> changes the contribution flow on every pull request. Until it is taken, this
> document binds nobody.
>
> Not legal advice; have a lawyer review this before accepting signatures
> against it.

## Why this exists, in one paragraph

Oxy offers its applications under two licenses: the free
[Breathe License](../LICENSE-BREATHE.md) and the paid
[Commercial Terms](../LICENSE-COMMERCIAL.md). Only the copyright holder can
offer a second license for a work. So the moment a contribution Oxy does not own
is merged into a Breathe repository, Oxy can no longer offer the Commercial
Terms for that repository, because Oxy cannot license out somebody else's
copyright. That is a one way door: until the contributor is tracked down and
asked, the commercial arm for that repository is dead. This agreement prevents
that, by having contributors grant Oxy the rights it needs while **keeping
ownership of their own work**.

## Why a DCO is not enough

A Developer Certificate of Origin certifies that you had the right to submit
your contribution under the project's existing license. It does **not** give the
project the right to license your contribution to someone else on separate,
paid terms. For a single licensed open source project a DCO is the right,
lighter tool. For a dual licensed project it does not do the necessary job. Oxy
needs a CLA.

## What you are and are not agreeing to

**You keep the copyright in your contribution.** This is a license, not an
assignment. You may use, publish, sell, or relicense your own work anywhere else,
without asking Oxy.

**Oxy gets a broad license, including the right to sublicense.** That is the
part that lets Oxy keep offering the Commercial Terms. In practice it means Oxy
can charge a company for the right to use your contribution commercially, and
keep the money.

**What Oxy cannot do with your contribution, and this is worth knowing before
you decide.** Oxy cannot make it proprietary or closed. Under the Breathe
License, source publication and attribution apply to everyone, including to
paying commercial licensees, and Oxy has committed in the license text itself to
never offering any license that removes them. So your contribution stays public,
in every hand it passes through, whatever Oxy charges for it.

**Be clear eyed about the part that remains.** Some people will still not sign
this, on the principled ground that a company should not charge for donated work
at all. That is a reasonable position and Oxy will not argue with anyone who
holds it. If you would rather contribute to a project without a CLA, Oxy's SDK
and UI layer is Apache-2.0 and takes contributions under a DCO only. See
[`README.md`](README.md).

## Which repositories require it

**Required:** every repository in the Breathe layer, because those are the ones
with a commercial arm. `@oxyhq/api`, `@oxyhq/node`, `website`, `Mention`,
`CrowdSource`, `Syra`, `Mercaria`, `Homiio`, `Moovo`, `Space`, `Allo`, `Alia`,
`OxyPay`.

**Not required:** the Apache-2.0 SDK and UI layer. Apache-2.0 already contains
an inbound contribution grant at its Section 5, which is sufficient. A DCO
sign off is enough there, and keeping the barrier low on that layer is the whole
point of it being permissive.

## How to run it, the lightest way

**None of the following has been done.** Step 1 is this file. Steps 2 to 4 are
the switch, and the switch is off on purpose: installing a bot changes what
every contributor sees on every pull request, which is a decision about how the
project receives work, not about what this document says.

1. Put [the agreement text](#the-agreement) in each Breathe repository, or once
   in `OxyHQ/.github` and link to it.
2. Install **CLA Assistant**, a free GitHub app. It comments on a first time
   contributor's pull request, takes a signature by clicking a button, and
   stores signatures in a repository you control. No email, no PDFs, no lawyers
   in the loop.
3. Make its status check **required** on protected branches, so an unsigned pull
   request cannot merge.
4. Configure it to skip bots and to skip Oxy's own accounts.

Setup is roughly thirty minutes organisation wide. Alternatives if CLA Assistant
does not fit: the EasyCLA service from the Linux Foundation, which is heavier and
built for corporate contributors, or a GitHub Action that checks signatures
against a file in the repository.

**Do this before announcing any license change.** The announcement is what draws
attention, and attention is what produces the first outside pull requests.

## Corporate contributors

If you are contributing as part of your job, your employer may own your work. In
that case have someone authorised to bind the company sign on its behalf, listing
the accounts covered. The same text works; the signature line differs. Ask
licensing@oxy.so.

---

## The agreement

### Oxy Individual Contributor License Agreement, Version 1.0

Thank you for contributing to Oxy. This agreement sets out the terms on which
you contribute. It is deliberately short.

**1. Definitions.** "Oxy" means **The Oxy Collective, Inc.**, a company
incorporated in `<JURISDICTION OF INCORPORATION>` under registration number
`<REGISTRATION NUMBER>`, and any successor to which this agreement is assigned
under Section 12. "You" means the individual who accepts this agreement.
"Contribution" means any original work of authorship, including any changes or
additions to an existing work, that you intentionally submit to Oxy for
inclusion in any project owned or managed by Oxy. "Submit" means any form of
communication sent to Oxy or its representatives, including on electronic
mailing lists, source code control systems, and issue tracking systems, but
excluding communication you conspicuously mark as "Not a Contribution".

**2. You keep your copyright.** This agreement does not transfer ownership of
your Contribution. You remain free to use, publish, license, and sell your own
Contribution however you wish, without restriction and without notifying Oxy.

**3. Copyright license.** You grant Oxy and to recipients of software
distributed by Oxy a perpetual, worldwide, non exclusive, no charge, royalty
free, irrevocable copyright license to reproduce, prepare derivative works of,
publicly display, publicly perform, sublicense, and distribute your Contribution
and such derivative works.

**4. Right to sublicense on commercial terms.** You expressly agree that the
license in Section 3 includes the right for Oxy to sublicense your Contribution,
and works derived from it, under separate commercial terms, and to charge a fee
for doing so and retain the proceeds. **This is the provision that lets Oxy
offer its commercial license, and it is the reason this agreement exists.**

**4.1 Oxy's commitment in return.** Oxy will not distribute your Contribution,
or any work derived from it, under terms that permit the recipient to withhold
its corresponding source from users, or that waive attribution to the
contributors of the work. This reflects Sections 3.1, 3.2, 3.3, and 4 of the
Breathe License, under which source publication and attribution bind every user
including paying commercial licensees. Oxy may change the license of the project
for future versions, and this Section 4.1 continues to apply to your
Contribution regardless.

**5. Patent license.** You grant Oxy and to recipients of software distributed by
Oxy a perpetual, worldwide, non exclusive, no charge, royalty free, irrevocable
patent license to make, have made, use, offer to sell, sell, import, and
otherwise transfer your Contribution, where such license applies only to those
patent claims licensable by you that are necessarily infringed by your
Contribution alone or by combination of your Contribution with the project to
which it was submitted. If any entity institutes patent litigation alleging that
your Contribution, or the work it was submitted to, constitutes direct or
contributory patent infringement, any patent licenses granted to that entity
under this agreement terminate as of the date such litigation is filed.

**6. You are entitled to grant this.** You represent that each of your
Contributions is your original creation, and that you are legally entitled to
grant the licenses above. If your employer has rights to intellectual property
you create, you represent that you have received permission to make the
Contribution on behalf of that employer, that your employer has waived those
rights, or that your employer has executed a separate corporate agreement with
Oxy.

**7. Third party material.** If you submit work that is not your original
creation, you may submit it separately from any Contribution, identifying its
source and any license or other restriction of which you are personally aware,
and conspicuously marking it as "Submitted on behalf of a third party:
`<name>`".

**8. No obligations, no warranty.** You are not expected to provide support for
your Contribution, and you may choose to do so or not. Except as stated in
Section 6, and as far as the law allows, you provide your Contribution on an "AS
IS" basis, without warranties or conditions of any kind, express or implied.

**9. Oxy is not obliged to use your Contribution.** Oxy may accept, reject, or
remove any Contribution at its discretion. This agreement does not create any
obligation on Oxy to include your Contribution in any product, or to keep it
there.

**10. Notification.** You agree to notify Oxy if any fact or circumstance you
have represented above becomes inaccurate.

**11. Governing law.** This agreement is governed by the law of
`<JURISDICTION>`, without regard to its conflict of law rules.

**12. Successor entity.** Oxy may assign this agreement, together with the
licenses you grant under Sections 3, 4 and 5, to a **single successor entity**
that takes over stewardship of the project, but only where that successor first
assumes in writing, for your benefit and the benefit of every other contributor,
every obligation Oxy owes you under this agreement, **including Section 4.1**.
On such an assignment the successor becomes "Oxy" for the purposes of this
agreement, Oxy's own rights under it end, and Oxy publishes notice of the
assignment in the project's repositories.

This clause is deliberately narrow, and the narrowness is the point. It is
**not** a right to sell, transfer, or sub-contract your Contribution to whoever
is willing to pay for it. An assignment that does not carry Section 4.1 forward
grants the assignee nothing under this agreement. If a successor could take your
work free of the commitment never to make it proprietary or to strip your
attribution, there would be no reason for you to sign this, and that is exactly
the objection this clause exists to answer.

It exists for one foreseeable event. Oxy intends to move this work to a
foundation once that entity is registered. Without this clause, the day that
happens every person who ever signed has to be found and asked to sign again,
and the ones who cannot be found permanently break the commercial arm for the
repositories they contributed to. With it, the deed of assignment carries the
signatures along by itself.

---

Signed by clicking to accept on a pull request, which records your GitHub
username, the commit, and the date.

Name: `<FULL NAME>`
GitHub username: `<USERNAME>`
Date: `<DATE>`
