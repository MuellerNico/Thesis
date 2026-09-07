# Thesis review – key issues

Reviewed: abstract, introduction, theory, results, performance, appendix. Turbulence section skipped (in progress). Existing `\todo`s not repeated. Ordered by importance.

## Must fix

4. **AV sign** (theory.tex eq:av_Pi): with `w_ab = v_ab·r̂ < 0` for approaching pairs the linear term is negative and the quadratic positive, so they oppose. Standard form has a leading minus on the linear term (or define `w_ab` with the opposite sign).

## Should fix

7. **Loop: α_B=0 run is plotted twice but never discussed**, and the "28% less heating" number collides with the commented note at results.tex:179 ("14% vs 28% vs 127%") where 28% refers to a different comparison. Report the α_B=0 outcome and re-verify the 28%.
8. **Partition-of-unity condition** (theory.tex:130): `k_a X_a = m_a` is dimensionally off given `X_a = m_a/ρ⁰_a`. The condition is `k_a = 1`.
9. **eq:fdivb missing 1/μ₀** (theory.tex:238): the Maxwell stress carries 1/μ₀, so the divB correction must too. Harmless numerically (μ₀=1 everywhere) but inconsistent on paper.
10. **SLRB modulator is the Tricco & Price switch you criticised** (theory.tex:347 vs 393). `m_a` is exactly the "one scalar cannot separate resolved gradient from discontinuity" detector. Fine as a deliberate conservative fallback, but say so and name the regime where it over-dissipates (resolved but steep structure, `h|∇B| ≳ |B|`).
11. **F_ab unguarded** (eq:vanleer): denominator vanishes generically at field extrema. State the regularisation actually used in the code. The `min(1,·)` is redundant since `4F/(1+F)² ≤ 1`.
13. **Sedov divB error is compared but never stated** (results.tex:136). Quote the number. Also state per test which AR scheme was used for Sedov/OT/KH (only the default paragraph implies SLR).
14. **Rotor slice plane**: text says z=0, caption z=0.0625 (results.tex:274 vs 279). Caption is right.
15. **Intro promises discussion inside the performance chapter** (introduction.tex:15: "In chapter \ref{sec:performance} ... Finally, the key findings are discussed"). Point to the discussion chapter instead.
16. **Performance: weak-scaling GPU counts never stated**; strong scaling explains speedup relative to 4 GPUs but not why (memory?). The "~60% total overhead" is not reconcilable from the per-kernel numbers given; say it is read off total iteration time.
17. **Implementation chapter stub** (implementation.tex) still says "maybe remove"; appendix sections are never referenced from the main text. Decide, and add one forward ref to the appendix.

## Minor (only if time)

- theory.tex:343 "transverse velocity differences are the only thing creating discontinuities in B" is false (fast/slow shocks compress B_⊥) and contradicts the current-sheet discussion at line 385. Soften to "dominant source".
- theory.tex:228 `√(c_s²+v_A²)` is the *maximum* fast speed, not "the" fast magnetosonic speed.
- theory.tex:214 `K` undefined in eq:vel_jacobian.
- theory.tex:302 "not reinjected as heat since hyperbolic cleaning transports errors away" is a non sequitur; the energy is removed by the parabolic damping. Just say it is discarded as in Phantom and monitored.
- results.tex:296 KH "mirror image": B is a pseudovector, so this is reflection plus B→−B invariance, not a pure mirror.
- results.tex:222 `ρ_0 = γ P_0 M_0` should be `M_0²` (same value at M_0=1).
- Kernel-comparison caption blames "node-to-node noise" but the methodology describes a single run per point.
