# Thesis review – key issues

Reviewed: abstract, introduction, theory, results, performance, appendix. Turbulence section skipped (in progress). Existing `\todo`s not repeated. Ordered by importance.

## Must fix

1. **SLRB / SLRB2 never appear in any result.** Derived in theory (eq:slr_B_mod, tab:ar_schemes), announced in results naming paragraph, but every figure is a05 vs SLR only. Either add them to Brio-Wu (the case that motivates them) or demote to "implemented, not evaluated" in theory and drop from the naming paragraph.
2. **Broken refs.** `\eqref{eq:res_heating}` has no label anywhere (results.tex:111, 210). `\ref{sec:ac}` points to a commented-out label (theory.tex:435, used results.tex:17). Define the heating equation (or point to eq:ar_du) and either uncomment AC or say "AC not used" without a ref.
3. **Alfvén ICs wrong as written** (results.tex:45-47): `v_1` assigned twice. Should be `v_1 = 0`, `B_2 = v_2 = ...`, `B_3 = v_3 = ...`. Also text says t=5 periods, caption says t=4 (results.tex:49 vs 57).
4. **AV sign** (theory.tex eq:av_Pi): with `w_ab = v_ab·r̂ < 0` for approaching pairs the linear term is negative and the quadratic positive, so they oppose. Standard form has a leading minus on the linear term (or define `w_ab` with the opposite sign).
5. **AVSLR sentence contradicts theory** (results.tex:170): "AVSLR subtracts the linear part fully *due to the Balsara-modulator*". Plain AVSLR has no Balsara weighting, and where Balsara is used it *suppresses* the reconstruction. Rewrite: AVSLR removes the resolved linear shear and therefore leaves sub-resolution shear noise largely undamped, which is why it ranks below constant AV here.

## Should fix

6. **Brio-Wu headline claim has no numbers** (results.tex:111). The `osc` metric is defined at length, then SLR is praised for "slightly less ringing" with no value quoted. Give L1 and osc for a05 vs SLR on B_y.
7. **Loop: α_B=0 run is plotted twice but never discussed**, and the "28% less heating" number collides with the commented note at results.tex:179 ("14% vs 28% vs 127%") where 28% refers to a different comparison. Report the α_B=0 outcome and re-verify the 28%.
8. **Partition-of-unity condition** (theory.tex:130): `k_a X_a = m_a` is dimensionally off given `X_a = m_a/ρ⁰_a`. The condition is `k_a = 1`.
9. **eq:fdivb missing 1/μ₀** (theory.tex:238): the Maxwell stress carries 1/μ₀, so the divB correction must too. Harmless numerically (μ₀=1 everywhere) but inconsistent on paper.
10. **SLRB modulator is the Tricco & Price switch you criticised** (theory.tex:347 vs 393). `m_a` is exactly the "one scalar cannot separate resolved gradient from discontinuity" detector. Fine as a deliberate conservative fallback, but say so and name the regime where it over-dissipates (resolved but steep structure, `h|∇B| ≳ |B|`).
11. **F_ab unguarded** (eq:vanleer): denominator vanishes generically at field extrema. State the regularisation actually used in the code. The `min(1,·)` is redundant since `4F/(1+F)² ≤ 1`.
12. **Divergence plateau overclaim** (results.tex:228): a plateau is equally consistent with source saturation (your own note at line 25 says so). Soften to "bounded and source-limited rather than cleaning-limited". Also state the OT run duration.
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
