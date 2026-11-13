## Lab 03 Analysis

### What I did
I took the baseline model from Lab 01 and trained it on training sets where a share of the labels had been replaced with a different digit. The corruption levels were 0%, 5%, 10% and 20% of the 1,347 training records (0, 67, 135 and 269 labels changed). Each time I measured accuracy on the same 450 test images, whose labels were never touched (E03_corruption_results, E03_corruption_chart).

### What I measured
Clean test accuracy was 0.962, 0.960, 0.958 and 0.933 for the four levels. In test images that is 433, 432, 431 and 420 correct out of 450. The 5% and 10% levels cost only one and two images, which is too small a difference to call a trend from one seed and one split. The 20% level lost 13 images, about 2.9 percentage points, which is a clearer drop but still from a single run.

### What this does and does not show
The model tolerated random label corruption fairly well in this experiment. One possible reason is that wrong labels spread across all ten digits and partly cancel out, but I did not test that. I would not conclude that poisoning is harmless. Random label noise is not a targeted attack. An attacker who chooses which labels to change, or who plants a backdoor trigger, could do much more damage with fewer changes. This lab does not simulate that.

### Why the test labels must stay unchanged
The test set is the fixed answer key that every model is marked against. If I changed it, or let training data leak into it, the accuracy numbers would no longer be comparable between the four runs. That is why only the training labels were altered.

### Hypothetical incident: forensic chronology
Suppose an auditor finds that an upstream label-approval step was bypassed for part of the training data. Altered labels could enter the pipeline at these points:
1. **Collection or labelling:** a compromised annotator or tool assigns wrong labels.
2. **Storage and transfer:** the dataset file is edited after approval.
3. **Preparation:** a script or merge step overwrites labels.
4. **Training:** the model is trained on the changed data and passed to deployment.

The six questions from the worksheet, for my experiment:
* **What changed?** A set share of training labels, replaced at random with a different digit.
* **What did not change?** The test images and test labels.
* **How would it be detected?** A hash mismatch against the reference manifest, a gap in the approval history, or an unexplained fall in accuracy. In my hash check, changing one label out of 1,347 gave a different SHA-256 hash (E03_hash_check).
* **What was the measured impact?** Accuracy of 0.933 at 20% corruption, against 0.962 for the clean model.
* **What remains unknown?** Whether a targeted attack would do more harm, and how this transfers to other models or real systems.
* **How should the organisation respond?** Contain by stopping use of the affected model, compare dataset versions, have an independent person review the labels, roll back to the last verified version, retrain and retest, and record a sign-off.

### Escalation path for unexplained accuracy loss
1. **Monitoring** flags a fall in accuracy or a shift in label distribution.
2. **Data owner** checks recent dataset changes and the hash manifest.
3. **Security team** is notified if a hash mismatch or a bypassed approval is found, and investigates who changed what.
4. **Containment decision:** the model owner decides whether to pause the model or roll back.
5. **Independent review and retest** before any sign-off to return to use.

### Limits of this experiment
It used one seed, one split, one model, tiny 8×8 images, and random corruption only. A hash shows that something changed but not what or who, and it only helps if the reference hash is stored where an attacker cannot edit it. I assessed only the hash control in practice. The other controls in my Part B checklist are marked "Not assessed".