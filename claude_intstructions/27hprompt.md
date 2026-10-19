Take over TODO 27 (World 4: Tidewhisper). Only stage 27h remains; 27a-27g are
merged. Work on feat/todo-27h-campaign-release. Follow AGENTS.md as written.

IMPORTANT: develop has moved. TODO 29 (caves, 29a-29f) merged on 2026-10-19,
23 commits, touching 45 src files including fx/shadows.js, fx/groundDecals.js,
core/Game.js, entities/player/Player.js, entities/enemies/Enemy.js and
combat/CombatSystem.js. Every earlier 27h measurement predates that merge and no
longer certifies anything. Re-run acceptance, the three-hero duel/pacing balance
and the full suites on the synchronized candidate.

Read first, in this order:
  1. TODO.md, section 27 (all the "27h ..." notes)
  2. docs/wiki/technical/tidewhisper-release.md — especially "Step 3 finding: the
     reference display's refresh rate and the frame-interval gate (2026-10-19)"
     and the "Acer session runbook (queued, 2026-10-19)" after it
  3. docs/wiki/technical/performance.md
  4. docs/logs/2610191019 todo-27h-refresh-rate-finding.md
  5. docs/logs/2610191629 todo-29-merge-to-develop.md, for what just landed

Step 0, synchronize: develop -> feat/todo-27 -> feat/todo-27h-campaign-release.
Expect conflicts in src/config/render.js (develop adds the `cave` budget, the
stage adds the `tidewhisper` ceiling and PERFORMANCE_REFERENCE — keep both) and
scripts/shots.mjs; TODO.md and the tour screenshots may also conflict, since 29f
retook the tour. Commit the synchronized candidate clean before measuring: the
collector refuses a dirty tree.

Step 0b, re-validate the stage's own render work against caves. The stage carries
two optimizations that are not in develop — a clean-immutable-subtree matrix skip
and conservative actor-frustum gating (src/render/actorCulling.js,
radialBounds.js, scene.js). Caves are a scene type they have never been tested
against: small enclosed rooms with local lights. Extend the existing pixel-
equivalence and world-matrix browser checks to cover a cave before trusting them,
and treat a mismatch there as a blocker, not a tuning note.

Confirm you are on the Acer Nitro ANV15-51 with the RTX 4050 as the active WebGL
renderer. If you are not, stop and say so — only that machine certifies.

Then do the runbook in order. The first step is unverified and matters most:
measure the panel's actual refresh rate. A previous session found the empty-page
clock reads 6.1 ms median, which suggests a ~165 Hz panel on which the fixed
16.67 ms p95 interval limit silently demands ~82 FPS rather than the 60 FPS it
stands for. Confirm or refute that with real measurement before anything else and
record what you find. If the panel is high-refresh, prefer setting the display to
60 Hz for acceptance runs — that needs no code and no rule change. If it is
genuinely 60 Hz, the hypothesis is dead, the shortfall is real, and you should
fall back to the remedy ladder in the handoff (callback p95, longer warmup,
Medium certification, dynamic quality scaling) rather than improvising.

Then run acceptance on a quiet host: nothing else open, no git or file activity
during the run, AC power, high-performance plan, clean committed candidate.
node scripts/tidewhisper-performance.mjs --release, all 18 cases.

Constraints:
  - Do not loosen the 60 FPS target, cherry-pick passing rows, freeze the
    acceptance simulation, or relabel a diagnostic as certification.
  - Do not add a 60 FPS frame cap until the refresh rate is settled; on a 165 Hz
    panel it would pin every interval at 18.18 ms and fail the gate harder.
  - Do not enable the Tidewhisper release flag until its full gate passes.
  - A release to master needs my confirmation; 27h ends at develop.

If acceptance passes: continue with "Finish 27h" steps 3-5 in the handoff — enable
the destination, verify the real production travel/Continue/save/completion path,
retake the screenshot tour (must end "errors: none") and review the shots, update
the wiki/TODO, run the full suites and browser checks on the synchronized stage,
then merge stage -> feat/todo-27 -> develop, push, and log it. The tour needs
retaking even though 29f just retook it, because enabling Tidewhisper changes
title, portal and journal content.

If acceptance fails again: record the matrix as another no-go, then apply the
agreed gate split — separate 27h's functional completion from its performance
certification so performance gates only the public master release, not TODO 28,
29g and 30. That split is approved and described in the handoff but is not yet
written into TODO.md; writing it is yours to do. Note 29g (Tidewhisper and
Duskhollow cave rollout) needs 29f + 27h + 30i, and 29f is now done, so 27h is
the live blocker there too.

Finish with the go/no-go verdict: actual session cost, what the TODO 26 groundwork
got wrong, and whether the 27 checklist was too large. That verdict gates
Duskhollow (30) and the optional otter pet.
