# Loki Radar

Daily machine-curated tech radar behind [lucashanson.dk/radar](https://lucashanson.dk/radar).

Sources: RSS and Bluesky feeds, Reddit (via Redlib), GitHub (releases of starred repos, trending, rising new repos), Hacker News, Lobsters, Hugging Face daily papers and verified public Nostr notes. A local Qwen model scores each item against an interest profile and writes a short summary.

- `public.json`: latest output, read by the website

Runs twice a day on a home server.

## Nostr collection

`sources.toml` defines public relays, discovery topic tags and optional curated
author public keys. Reads are anonymous: no signing key, login, AUTH or publishing.
Only signed kind-1 notes within the existing freshness window are accepted.
Tampered events, replies from broad discovery, excluded topic tags, duplicate
events and duplicate linked articles are discarded. Network reads have per-relay
timeouts and caps; other sources continue when a relay is unavailable.

The original note permalink is retained in ranking input. Existing private-topic
and score filters still decide which notes may enter public.json. A signature
proves authorship, not factual accuracy. No arbitrary linked content is fetched.

The legacy signed-in X collector is disabled by default. Nostr requires neither
X API credits nor browser credentials. Existing twice-daily scheduling is unchanged.

Behavior regressions: `uv run --with coincurve --with websockets python -m unittest -v test_nostr_source`.
