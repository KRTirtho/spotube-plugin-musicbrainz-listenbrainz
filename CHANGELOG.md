# [1.0.1](https://github.com/KRTirtho/spotube-plugin-musicbrainz-listenbrainz/compare/0.1.1...1.0.1) (2026-10-30)

### Features

- feat: add comprehensive resilience pipeline for MusicBrainz/ListenBrainz API calls
  - Token bucket rate limiter (8 req/s sustained, burst 16) shared across all endpoints
  - Circuit breaker pattern (5 failures threshold, 30s recovery, 3 half-open probes)
  - Exponential backoff retry with jitter (3 attempts, 400ms initial, 2x multiplier, 10s max)
  - Error classifier for intelligent fallback decisions (OFFLINE vs SERVICE_UNAVAILABLE)
- feat: scrobbling now uses resilient ListenBrainz calls with automatic retry

### Bug Fixes

- fix: prevent HTTP 503 errors from concurrent metadata requests
- fix: gracefully handle MusicBrainz/ListenBrainz service outages

### Technical Details

- Added `src/resilience/` module with `rate_limiter.ht`, `circuit_breaker.ht`, `error_classifier.ht`, `retry.ht`
- Updated `CorePlugin` to use resilient calls for scrobbling
- Updated `BrainzMetadataProviderPlugin` with `mbResilient` and `lbResilient` wrappers

---

# [0.1.1](https://github.com/KRTirtho/spotube-plugin-musicbrainz-listenbrainz/compare/0.1.0...0.1.1) (2025-09-15)

### Bug Fixes

- fix: sort playlist by latest date and add support text
- fix: no artists in user stats causing nullObject exception in recommendations.ht (#7)