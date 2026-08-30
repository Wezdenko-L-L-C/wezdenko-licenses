# wezdenko-licenses

**Licence texts for Wezdenko L.L.C. products. Public, versioned, immutable, hash-pinned.**

Consumed at build time by the products that ask people to accept them, so the text shown to a
person and the text recorded in this repo cannot drift apart.

```
licenses/<product>/<kind>/<version>/
    text.md     ⛔ the words people accept. Hashed. NEVER edited after publication.
manifest.json   generated — id, version, sha256, bytes, plus private-record hashes
tools/manifest.mjs
```

⛔ **Accepted text only. Nothing else belongs here.**

## The four rules

**1. ⛔ A published `text.md` is immutable.** Someone has accepted those words and a capture record
names that version. Changing it makes the record a claim about text that no longer exists. To change
a licence, **add a new version directory**. Never edit in place, never move a tag.

**2. ⛔ Only the words people accept.** This repo is public and distributed, so the test is not
*"is it privileged?"* but *"is this shown to the person accepting?"*

Our **rationale** fails that test even though nothing protects it. It records where our own position
is weakest — which clause rests on bundled consent, which age floor is a guess pending advice — and
published, it is a map to the weakest clause, written by us and contemporaneously dated. It lives at
`G:\Shared drives\Wezdenko L.L.C\Legal\<Product>\Rationale\`, beside the reviews and
correspondence it belongs with, together with everything genuinely privileged.

⭐ **Public is the safety property.** If everything here is meant to be public, nothing sensitive can
end up here by accident. A private repo would quietly invite the opposite.

➡️ **When you add a licence version, write its rationale in `Legal\` and record that document's
hash in `private_record`.** The pairing is then provable without publishing a word of it.

**3. ⛔ Pin by commit SHA. Never a version range.** A licence is not a normal dependency: bumping it
invalidates every existing acceptance and forces a re-prompt on real people. A caret range or an
automated dependency PR would silently start a re-consent campaign. Pin the SHA; tags are labels for
humans and can be moved, so they are not the pin.

**4. Regenerate and verify.** `npm run manifest` after adding a version, `npm run verify` in CI.
Verify fails if any `text.md` differs from its recorded hash — which, given rule 1, means someone
edited published text.

## Why the hash matters

A capture record storing `licence_version: "2026-08-29"` asserts which version was current and
trusts the archive to still hold the matching words. A record storing the **sha256** proves *which
bytes were shown* — checkable by anyone, independent of this repo, the archive, or our own
discipline. That is the difference between "we keep good records" and evidence.

➡️ Consumers should store **both** the version and the hash on the acceptance record.

## The private record

`G:\Shared drives\Wezdenko L.L.C\Legal\` holds what this repo must not: reviews, correspondence,
memos, evidence. It is deliberately outside version control and outside the build — **the build
cannot reach `G:`**, which makes leaking privileged material into a package structurally impossible
rather than merely against the rules.

When a document lands there that is worth pinning, add its hash to `private_record.documents` in
`manifest.json`:

```json
{ "path": "Legal/Spotcraft/Reviews/2026-09-xx counsel review.pdf",
  "sha256": "…", "recorded": "2026-09-xx", "note": "what it is, not what it says" }
```

⭐ **Publishing a hash proves a document existed and has not changed, without disclosing it or
waiving privilege.** The `note` must describe the document, never its contents.

⚠️ The shared drive protects against a bad edit, not against losing account access; the backup
routine for the business records covers `Legal\` for that reason.

## Consuming this

```bash
npm install github:Wezdenko-L-L-C/wezdenko-licenses#<commit-sha>
```

Then inline `text.md` at build and record `version` + `sha256` on every acceptance. See
`scripts/inline-license.mjs` in the spotcraft repo for the reference consumer.
