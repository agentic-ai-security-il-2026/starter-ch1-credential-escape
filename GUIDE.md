# Student guide — Ch2 Credential Escape Room

**Difficulty:** 3 · **Kickoff:** 13 Dec 2026 · **Deadline:** 22 Dec 2026, 23:59 · Tag: `submission-v1`

## 1. Story

Enterprise question: *What’s the blast radius when an agent’s credentials are compromised?*

You get a small multi-service agent stack. **Assume one agent’s credential is stolen.** Measure what it can reach. Then implement **containment** — scoped / short-lived credentials, network boundaries, workload identity patterns (SPIFFE-style) — and measure again.

**In scope:** token scope, TTL, network policy / compose networks, least-privilege service accounts, blast-radius metrics.  
**Out of scope:** need-to-know *payload* envelopes across hops (that’s Ch3); prompt-only “please don’t use the key”; attacking the shared RH demo control plane.

## 2. What we expect

1. Runnable fork of this starter (Apache-2.0) in your `team-<slug>` or this starter’s PR/fork workflow as announced.
2. Filled [SCENARIO.md](SCENARIO.md) (sector + what “compromise” means).
3. `TRACE.md` (create it): how to reproduce **baseline blast radius** and **post-containment** measurements.
4. Public repo + tag `submission-v1` by deadline.
5. ≤5 min demo: before metric → defense → after metric → residual risk.

## 3. Grading

| Criterion | Weight | Good looks like |
|-----------|--------|-----------------|
| Security effectiveness | 50% | Clear before/after reduction; defenses bind without honor-system prompts |
| Code quality & minimalism | 20% | Small, reviewable changes; no secret sprawl |
| Presentation / demo | 20% | Reproducible measurements; scenario makes the risk real |
| Creativity | 10% | Extra containment idea beyond the starter’s TODOs |

**Minimum bar:** automated or scripted blast-radius probe + at least one working containment that measurably shrinks it.

## 4. Setup & install

**Prereqs:** Podman or Docker, Git, ~8–16 GB RAM.

```bash
git clone https://github.com/agentic-ai-security-biu-2026/starter-ch2-credential-escape.git
cd starter-ch2-credential-escape
cp .env.example .env
podman compose up --build
podman compose run --rm probe baseline   # measure blast radius
# implement containment, then:
podman compose run --rm probe contained
```

Optional LLM features use Nebius Token Factory — paste key into `.env` after Form 2 (not required for core blast-radius scoring if the probe is local).

## 5. Related reading

- SPIFFE / SPIRE concepts (workload identity)
- Short-lived credentials / STS patterns
- Network policy / zero-trust for microservices
- Hub: demo platform safety (if you later mirror onto OpenShift)

## 6. Support

Hub issues: `starter-bug`, `challenge-concept`, `infra`, `llm-nebius`.
