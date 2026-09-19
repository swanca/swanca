## Hi, I'm Swan

I build small tools that do one thing precisely, and I publish the results even when
the result is "this doesn't work".

Most of what's here answers a question I actually had: *is my email set up to reach the
inbox? what does this CSP really allow? is there an edge in this market at retail size?*
The tools are small because the questions are specific.

---

### Web tools

Each one is a single-purpose checker, free, no account. Astro + TypeScript, deployed as a
static site with a thin API. Written with the reasoning in the code: the interesting parts
cite the RFC they implement.

| | What it answers | Tests |
|---|---|---|
| **[MailScope](https://github.com/swanca/mailscope)** | Is this domain's email set up to reach the inbox? Expands every SPF `include` and counts the RFC 7208 lookups the receiver will actually perform — the limit most records quietly exceed. | 76 |
| **[HeaderScope](https://github.com/swanca/headerscope)** | Not "is there a CSP" but "what does this CSP permit". A policy with `'unsafe-inline'` passes every presence check while stopping almost nothing. | 69 |
| **[OGScope](https://github.com/swanca/ogscope)** | What preview card will X, LinkedIn, Slack and the rest actually render for this URL? X shut down its Card Validator; Facebook's needs a developer login. | 86 |
| **[BotCheck](https://github.com/swanca/botcheck)** | Which AI crawlers is your `robots.txt` letting train on your site? | 65 |
| **[Origin](https://github.com/swanca/content-origin)** | Who signed this image and has it changed since? Reads C2PA Content Credentials in the browser — a cryptographic record, not a guess from the pixels. | 35 |
| **[Shade](https://github.com/swanca/shade)** | A daily colour game. One tile is off. Seeded from the date, so everyone gets the same puzzle, and nothing is fetched after load. | 53 |

### Larger projects

**[crypto-backtest-study](https://github.com/swanca/crypto-backtest-study)** — 168 strategy
variants on BTC/EUR and ETH/EUR at 200 EUR of capital, run to a protocol fixed in writing
before the first result was read.

**None was admissible** once retail fees and robustness controls were applied. The
out-of-sample segment was never touched, and no live trading followed. The repository is
the whole study, including the part where it fails: the engine, 17 tests, 576 898 candles
with fingerprints, and the frozen run that produced every number in the reports.

A backtest showing a profit is the easy outcome to produce and the hard one to trust. This
one was built so that failure would be detectable.

**[french-benefits-engine](https://github.com/swanca/french-benefits-engine)** — a deterministic
eligibility engine for French social benefits, extracted from a larger private project.

The design constraint that shapes everything: **a rule is validated data, never executable code.**
The obvious alternative — let an administrator write conditions as code so new benefits need no
deploy — is a remote code execution hole wearing a CMS costume, and it makes rules untestable.
So the vocabulary is small and declarative, and anything it cannot express is a gap forced into
the open rather than hidden in a lambda.

The guarantees are enforced and tested rather than documented: nothing medical is ever inferred,
an unmodelled situation returns "outside scope" rather than a refusal, stale or malformed review
dates stop answering, and an invalid catalogue produces no positive match. 22 tests.

---

### How I work

**Say what the thing doesn't do.** Every one of these repos has a limits section. The benefits
engine orients and never decides. A C2PA signature says who signed a file, not whether it is
true. The backtest found nothing.

**Tests before confidence.** 423 passing across these repos. Where a number appears in a
README, a test holds it up.

**Cite the source in the code.** If a function implements a spec, the comment names the
clause. Six months later that comment is the only thing that explains the magic number.
