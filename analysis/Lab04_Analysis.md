## Final practical evidence and risk conclusion

### 1. Clean and attacked accuracy for both models
| Variant | Clean | FGSM | PGD |
|---|---|---|---|
| Baseline | 0.962 | 0.516 | 0.489 |
| Augmented, augmentation epsilon 0.10 | 0.940 | 0.284 | 0.260 |
| Augmented, augmentation epsilon 0.05 | 0.958 | 0.433 | 0.402 |
| Augmented, augmentation epsilon 0.03 | 0.962 | 0.467 | 0.438 |

Every model was attacked with examples generated against that model, on the same 450 test images (E04_metrics_table, E04_comparison_chart, E04_improvement_variant).

### 2. Why the defended model itself must be tested
An attacker targets what is actually deployed. If I had tested the retrained model only with images crafted for the baseline, the result would have measured the wrong thing and could have made the defence look better than it is. Generating FGSM and PGD examples against each candidate gives a fairer comparison.

### 3. Limitations
* The dataset is tiny (8×8 images, 1,797 samples) and the model is a simple linear classifier.
* The attacks are white-box and short, with a limited number of steps, and I used one seed and one split.
* I tested one type of defence, simple FGSM augmentation, at three augmentation strengths. Other defences were not tested.

### 4. Decision memo
**To:** Technical review board (hypothetical)
**From:** Janet Anya Okewu-Ihezie
**Date:** 14 November 2026
**Decision:** Reject this mitigation as tested. Carry out further controlled testing of alternatives before any adoption.

**Evidence:** In my run, simple adversarial augmentation did not improve robustness at any setting. Under FGSM and PGD, accuracy fell by about 5 points at augmentation epsilon 0.03, 8 to 9 points at 0.05 and 23 points at 0.10, relative to the baseline. Clean accuracy was unchanged at 0.03 and fell by 2.2 points at 0.10.

**Improvements and regressions:** There was no robustness improvement. The regressions grew with the augmentation epsilon. Retraining also adds cost and complexity (a larger training set and more steps) without a measured benefit.

**Rationale:** Adopting a control that lowers measured robustness would make the system less safe while appearing more secure. The intention behind the defence does not change the measured result.

**Possible explanations (not tested):** limited capacity of a linear model, augmented images generated once from the baseline model, and a mismatch between augmentation and attack strength.

**Conditions to revisit:** repeat with several seeds, test other training mixtures and model types, and use a stronger or different adaptive attack set. Any new candidate must be tested against itself, on the same held-out data, before sign-off.

**Residual risk:** Black-box, targeted and physical-world attacks were not tested. This is a local learning exercise and not a certification of model security.s