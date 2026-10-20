# Car damage segmentation: leak-free split

A cleaned re-split of the public **car_damage v6** dataset, used to train and test
[RepairLens](https://github.com/sparobanks/RepairLens).

## What changed from the original

The original export puts flipped, rotated and noisy copies of the same photo into its train, valid and test
folders. 84% of its test photos have a near-identical copy in its training folder, which makes any model look
better than it really is.

In this version:

- Every copy of a photo is kept in **one** folder only, so nothing in `valid` or `test` was seen in training in
  any form. Copies were found by comparing perceptual image fingerprints in all eight flips and rotations.
- `valid` and `test` contain only **original, unedited** photos (one per original photo).
- The two class names `Damage` and `damage` were the same thing, so they are merged into one class: `damage`.

| Folder | Images | Original photos | Damage outlines |
|---|---|---|---|
| train | 2,926 (includes the edited copies) | 1,089 | 5,437 |
| valid | 232 | 232 | 438 |
| test | 232 | 232 | 444 |

`manifest.json` lists every image, its folder, which original photo it belongs to (`group`) and whether it is an
original or an edited copy.

## Format

YOLOv8 segmentation format: one `.txt` per image, one line per damaged area:
`0 x1 y1 x2 y2 ...` (polygon corners, scaled 0 to 1). Images are 640 x 640.

## Credit and licence

Original dataset: **"car_damage"** by **sinfo** on Roboflow Universe,
https://universe.roboflow.com/sinfo/car_damage-4xqh8/dataset/6, licensed under
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

This re-split is shared under the same licence (CC BY 4.0). Changes: duplicate copies regrouped, images
re-assigned to train/valid/test, and class names merged, as described above.
