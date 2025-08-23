# Part 2: Reasoning-Based Questions

## Q1: Choosing the Right Approach  
For checking if a product has its label or not, I’d go with **object detection**. Detection lets the model spot if the label is present in the correct region of the product. If I used classification, it might confuse cases where the product looks fine but the label is missing, since the whole image is treated as one class. Segmentation could work too, but it feels like overkill here unless I need pixel-level precision. If detection fails, my fallback would be a simple image classification model focused only on cropped label regions, since that’s faster and easier to train.

---

## Q2: Debugging a Poorly Performing Model  
If my model struggles on new factory images, I’d first check for a **data mismatch** between training and test sets (different lighting, angles, or product batches). I’d visualize a batch of predictions to see if the model is consistently failing on certain cases. Next, I’d look at the label quality — maybe some annotations were off. I’d also run experiments like training on a smaller subset with heavy augmentation to see if it improves generalization. Finally, I’d track metrics like precision/recall per class instead of just overall accuracy to find weak spots.

---

## Q3: Accuracy vs Real Risk  
In this situation, accuracy isn’t the right metric because missing even one defective product can be costly. I’d pay closer attention to **recall (sensitivity)**, since we want to catch as many defective products as possible. Precision is also important, but recall carries more weight here — it’s worse to miss a bad product than to flag a good one. I might also look at the **confusion matrix** to see where exactly the model slips. Basically, I’d optimize for reducing false negatives, even if it means tolerating a few more false positives.

---

## Q4: Annotation Edge Cases  
Blurry or partially visible objects are tricky, but I’d generally keep them in the dataset. In real-world factory conditions, the camera won’t always capture perfect images, so the model should learn to handle imperfect data. The trade-off is that too many low-quality labels can confuse training and reduce accuracy on clean images. To balance it, I’d keep a mix: include enough edge cases so the model is robust, but not so many that they overwhelm the clean examples. This way, the model learns resilience without drifting off.

---
