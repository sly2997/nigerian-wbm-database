# Nigerian Water-Based Mud Formulation Database

A hand-built database of **71 drilling mud formulations** extracted from four published
studies of Nigerian clay, benchmarked against **API Specification 13A**.

Built as a petroleum engineering data analysis project by **Sylvia Igbafe**, Petroleum
Engineer and PhD researcher.

---

## The question

Nigeria imports drilling bentonite despite holding large clay deposits. Beneficiation
with sodium carbonate is the usual proposed route to using local clay instead.

**Does the published evidence show that a beneficiated Nigerian clay meets API 13A?**

## The short answer

No, and the reason is more interesting than a simple failure.

1. **Beneficiation cuts fluid loss by 59 to 82 percent, and never below the 15 mL limit.**
2. **Beneficiation lifts viscosity past the 30 minimum in 45 of 66 treated samples.**
   Raw clay sits between 3 and 6.5. Viscosity is the property beneficiation fixes.
   Fluid loss is the one it does not.
3. **In the one dataset with replicates, the experimental noise exceeds the effect
   being measured.** Seven repeats of an identical recipe spread 49 dial units, while
   sodium carbonate across its full range moves the reading by 31. No dose response
   can be resolved at that level of precision.
4. **Of 71 samples, only 12 were measured on both API tests.** Of those 12, one passes
   both, and it is the imported reference. Not because Nigerian clays failed, but
   because the published studies measure viscosity and filtration on different samples.
5. **Local Nigerian clay is not one material.** The Ondo deposit moves from 3 to 7 at
   600 rpm under treatment, while Akwa Ibom and Ogun deposits clear 30. Deposit
   identity must be carried as a feature in any model built on pooled data.

## The methodological finding

**None of the four studies tested on the API basis.** API 13A specifies 22.5 g of clay
per 350 mL of water. The four papers used 17.5, 20, 25, 30, 35 and 40 g. Every
comparison in this project is therefore indicative rather than a formal pass or fail,
and part of any apparent pass reflects clay loading rather than clay quality.

---

## What is in this repository

| File | What it is |
|---|---|
| `P1_WBM_Database_4PAPERS.xlsx` | The database. 71 rows, 34 columns, four sheets |
| `P1_WBM_Data.ipynb` | The analysis notebook, eight cells, runs top to bottom in Google Colab |
| `chart1_fluid_loss.png` | Fluid loss before and after beneficiation, three deposits |
| `chart2_viscosity.png` | Viscosity of all 71 samples against the API minimum |
| `chart3_soda_ash_noise.png` | Sodium carbonate dose against replicate scatter |
| `chart4_both_tests.png` | Both API tests at once, for the 12 samples that carry both |

### The workbook

Four sheets: `README`, `Data`, `Sources`, `API_13A_Spec`.

In the `Data` sheet, **yellow cells are entered by hand from the papers** and **green
cells are calculated by formula**. Plastic viscosity, apparent viscosity, yield point,
the YP/PV ratio and the API verdicts are never typed in. They are derived from the
600 and 300 rpm dial readings.

This doubles as an arithmetic check on the sources, and it found two real defects
(see below).

---

## Sources

| ID | Study | Deposit | Rows |
|---|---|---|---|
| S01 | Afolabi, R.O.; Ogunkunle, T.F.; Olabode, O.A.; Yusuf, E.O. (2018). Dataset on the beneficiation of a Nigerian bentonite clay mineral for drilling mud formulation. *Data in Brief* 20, 234 to 241. DOI 10.1016/j.dib.2018.07.071 | Ewekoro, Ogun State | 31 |
| S02 | Azeez, G.O.; Dada, E.O.; Muriana, M.; Lawal, I.A.; Arinkoola, A.O. (2018). Modification of Nigerian bentonite for utilization in oil well drilling operations. *LAUTECH Journal of Engineering and Technology* 12(1), 74 to 84 | Gombe State | 28 |
| S03 | Edenseting, B.O.; Bassey, E.N.; Babalola, R.; Gumus, R. (2023). Characterization and beneficiation of some Nigeria bentonitic clays for formulation of drilling mud in oil and gas industry. *ASRIC Journal on Engineering Sciences* 1, 50 to 56 | Edikor and Ukuku-Udung, Akwa Ibom State | 5 |
| S04 | Anthony, A.A.; Esther, O.C.; Chris, D.O.; Oni, B.A. et al. (2020). Assessment of clay materials for suitability in drilling mud formulation from part of Ondo State, South-West Nigeria. *Journal of Petroleum Exploration and Production Technology* 10(7), 2815 to 2828. DOI 10.1007/s13202-020-00947-9 | Ibule-Soro, Ifedore LGA, Ondo State | 7 |

Every row carries its source ID, so any value can be traced back to the table it came from.

---

## Two defects found in the published data

The calculated columns disagreed with the printed values in two places.

**S02-25** (Azeez, Table 8, run 7). Printed dial readings of 45 at 600 rpm and 21 at
300 rpm give a yield point of **minus 3**. A negative yield point is physically
impossible. Entered as printed and flagged for exclusion.

**S03-04** (Edenseting, Ukuku-Udung beneficiated). The printed apparent viscosity of
15.10 implies a 600 rpm reading of 30.2, while the printed plastic viscosity and yield
point imply 27.66. Both cannot be true. The plastic viscosity and yield point agree
with the paper's own ratio, so the dial readings were taken from those.

For contrast, all 21 calculated values in S04 reconcile exactly with the printed values.
The check is capable of detecting a problem and did not find one there.

---

## Limitations

- **No study tested on the API basis of 22.5 g per 350 mL.** All comparisons are indicative.
- **Only 12 of 71 samples carry both API measurements.** A missing point is not a
  failing point, and chart 4 cannot distinguish the two.
- **No sample was replicated except the S01 centre points**, so no point on any chart
  carries an error bar, and chart 3 shows that the uncertainty is not small.
- **Each deposit appears in one study from one laboratory.** Between-laboratory
  variation is not represented.
- **Three deposits only** have raw clay data, and the S03 imported reference is a
  secondary citation.
- Test temperature, aging condition and filter cake thickness are unreported for S04.

---

## Reproducing the analysis

1. Open `P1_WBM_Data.ipynb` in Google Colab.
2. Upload `P1_WBM_Database_4PAPERS.xlsx` to the session, into `/content`.
3. Runtime, then Run all.

Cell 1 should print `(71, 34)`. Cells 4 to 8 draw the four charts.

Built with Python, pandas and matplotlib.

---

## Status

Database and analysis complete. Written report in progress.

Future work: extend to deposits that report both API tests on the same sample, and to
any study testing at 22.5 g per 350 mL.
