# Synthetic Division — TI-84 EVO & Plus CE

A TI-BASIC program for the **TI-84 EVO and Plus CE** that finds rational-root candidates, tests them using synthetic division, and helps reduce a polynomial to lower-degree factors.

Enter a polynomial's integer coefficients, inspect its possible rational roots, see the confirmed roots, and choose one to perform synthetic division. The program can also assemble a factored equation from the rational roots it finds.

> **Note:** This is a *rational-root finder and synthetic-division helper*, not a computer algebra system (CAS). It does not guarantee complete factorization into linear factors over the real or complex numbers.

## Features

<img width="324" height="244" alt="ticevo_screenshot_20261017_220918-screen1" src="https://github.com/user-attachments/assets/754cf740-2ce9-4ca8-b677-682515b08a19" />
<img width="324" height="244" alt="ticevo_screenshot_20261017_220813-screen2" src="https://github.com/user-attachments/assets/b4811ebe-a3ff-4d67-bf9c-59cf5568ee38" />
<img width="324" height="244" alt="ticevo_screenshot_20261017_220824-screen3" src="https://github.com/user-attachments/assets/0f2ab18f-f215-460f-aa21-df3f9aef0d3f" />
<img width="324" height="244" alt="ticevo_screenshot_20261017_220904-screen4" src="https://github.com/user-attachments/assets/2d9c0529-cedb-4415-92c3-0aa0c2e48d1e" />
<img width="324" height="244" alt="ticevo_screenshot_20261017_221042-screen5" src="https://github.com/user-attachments/assets/3a2f7a57-d21b-40ee-8b48-04ab7db9e70c" />
<img width="324" height="244" alt="ticevo_screenshot_20261017_221102-screen6" src="https://github.com/user-attachments/assets/c894ccd1-98e4-42c3-99f6-aed67645a653" />

- Supports polynomial degrees **1 through 10**.
- Accepts **integer coefficients**, including zero coefficients for missing powers, with absolute values up to **1,000,000**.
- Generates factors of **p** (the relevant nonzero constant term) and **q** (the leading coefficient), and candidate roots **±p/q** using the Rational Root Theorem.
- Tests candidates and reports **distinct rational roots** whose calculated remainder is approximately zero.
- Handles **zero as a root** and can account for **repeated roots** when building the factored equation.
- Lets you choose a confirmed root for synthetic division (first root or an indexed root).
- Saves the selected division's **quotient coefficients and remainder** for use with the polynomial root solver.
- Shows the **carry, product, added coefficient, and result** for each synthetic-division step.
- Displays a **factored equation**, retaining an unfactored polynomial factor if no further rational roots are found.
- Includes a list legend when exiting.
- Conversation with AI that generated the program: https://chatgpt.com/share/6ad42f54-bb10-83e9-8cd6-459ba50a5004

## Example

Given:

$$
x^3-6x^2+11x-6=0
$$

Enter degree `3` and these coefficients **in descending order**:

| Power | Coefficient |
| --- | ---: |
| $x^3$ | `1` |
| $x^2$ | `-6` |
| $x$ | `11` |
| constant | `-6` |

The possible rational roots are derived from:

$$
p=\{1,2,3,6\},\qquad q=\{1\},\qquad r=\pm\frac pq
$$

The program identifies the distinct rational roots:

```text
1, 2, 3
```

Choose root `1`. Synthetic division produces:

```text
Original coefficients:    1|  -6  11  -6
Products:                 ⬇   1  -5   6
Bottom row:               1   -5   6   0 | r=0
```

The saved quotient is:

$$
x^2-5x+6
$$

The factored equation is:

$$
\boxed{(x-1)(x-2)(x-3)=0}
$$

### Missing powers

For $x^3+x+1=0$, enter `1, 0, 1, 1`. The **zero coefficient for $x^2$** is required. This example has no rational roots, although it does have a real irrational root.

## Installation

The repository contains TI-BASIC **source text** intended for a TI-84 EVO tokenizer.

1. Copy the full TI-BASIC program into your EVO-compatible tokenizer/editor.
2. Convert/tokenize it to the calculator's **`.8xp2`** program format.
3. Transfer the generated program to your TI-84 EVO using a compatible transfer tool.
4. Launch the program from the calculator's program interface.

### Tokenizer-specific source requirements

The current source has been adapted to the tokenizer used for this project:

- **Do not prefix every source line with `:`.**
- Every `Pause` must have an argument. To pause without displaying a value, use **`Pause ""`**.
- The temporary custom list is **`ʟEXPR`**. Its first character is **`ʟ` (U+029F, LATIN LETTER SMALL CAPITAL L)**, *not* the similar-looking **`∟`** character. It must be recognized by your tokenizer as the named-list prefix token.
- Numbered list names appear as `L1` through `L6` in the source format used by the tokenizer.

Other tokenizers can use different textual spellings for the same calculator tokens. If tokenization fails, check the specific tokenizer's syntax before changing the calculation logic.

> **Compatibility:** The source has been prepared for the TI-84 EVO/tokenizer workflow, but compatibility across all tokenizer versions and calculator firmware versions has not been independently verified.

## Using the program

1. **Enter the highest polynomial degree** (`1`–`10`).
2. **Enter each coefficient**, starting with the highest power and ending with the constant. Use `0` for any omitted powers.
3. Review the number of rational roots found. The confirmed distinct roots are in `L2`.
4. From **Show Results**, choose:
   - **Show Roots** — inspect confirmed rational roots.
   - **Show p Factors** — inspect factors of the relevant constant term.
   - **Show q Factors** — inspect factors of the leading coefficient.
   - **+/- p/q** — inspect the tested rational-root candidates.
   - **Show Factored Eq** — display the polynomial factored as far as the discovered rational roots allow.
   - **Save Divisor** — choose a confirmed root for synthetic division.
   - **EXIT** — show a legend for the lists.
5. Under **Save Divisor**, choose **First Root** or **Choose N'th Root**. The program stores the resulting quotient and remainder in `L6`.
6. From **Synthetic Division Results**, select **Show Solve Steps** to inspect each calculation.

When a screen says **Enter To Continue...**, press Enter to proceed.

## List and string usage

**Warning:** The program writes to calculator lists and strings. Back up existing values you want to keep before running it.

| Variable | Purpose |
| --- | --- |
| `L1` | Original input coefficients, highest degree first |
| `L2` | Distinct rational roots confirmed by synthetic division |
| `L3` | Positive factors of **p** |
| `L4` | Positive factors of **q** |
| `L5` | Candidate values of **±p/q** (up to the list limit) |
| `L6` | Chosen synthetic-division bottom row: quotient coefficients, then remainder |
| `ʟEXPR` | Temporary working list used to construct the factored expression |
| `Str1`–`Str4` | Working/result strings used to build and display the factorization; `Str3` holds the factored equation |

The program also uses ordinary single-letter numeric variables. Their existing values may change.

**Example:** If `L6` contains `{1, -5, 6, 0}` after dividing a cubic, the quotient is $x^2-5x+6$ and the remainder is `0`.

## How rational-root testing works

For an integer-coefficient polynomial with nonzero constant term, any rational root in lowest terms $r=a/b$ must satisfy:

$$
a\mid a_0,\qquad b\mid a_n
$$

where $a_0$ is the constant coefficient and $a_n$ is the leading coefficient. The program generates **±p/q** candidates and evaluates them by synthetic division (Horner's method). When the computed remainder is sufficiently close to zero, it records the candidate as a root.

If the polynomial has a factor of $x$, the program includes zero among its roots and works with the reduced nonzero constant term to generate the other rational candidates.

## Known limitations

- **Rational roots only.** Irrational and complex roots are not found by this search. Try the EVO Polynomial Root Finder for numerical solutions.
- **Distinct-root display.** `L2` lists a repeated root only once; repeated factors may appear as powers in the factored equation.
- **Floating-point tolerance.** A remainder with absolute value below `0.00000001` is treated as zero. Large coefficients, high degrees, or roundoff may produce misleading results.
- **Candidate list capacity.** `L5` holds at most 999 candidates; the program may continue testing candidates it cannot save in the list.
- **Not necessarily a complete factorization.** Any residual quadratic or higher-degree polynomial may remain displayed as a factor.
- **Display formatting.** Long expressions are split across lines/screens; decimal roots are shown numerically rather than necessarily as exact fractions.
- **Input restrictions.** Only integer coefficients (with absolute values at most 1,000,000) and degrees 1–10 are accepted.
- **Calculator state.** Lists `L1`–`L6`, the temporary list `ʟEXPR`, result strings, and single-letter variables can be overwritten.

## Suggested tests

| Coefficients (highest power first) | Expected rational factorization |
| --- | --- |
| `1, -6, 11, -6` | $(x-1)(x-2)(x-3)$ |
| `1, -3, 3, -1` | $(x-1)^3$ |
| `1, -2, 0, 0` | $x^2(x-2)$ |
| `2, -3, 1` | $2(x-1)(x-\tfrac12)$ |
| `1, 0, 0, -1` | $(x-1)(x^2+x+1)$ |
| `1, 0, 1, 1` | No rational linear factor found |

## License

This project is licensed under the **MIT License**. You may use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the software, provided that the original copyright and permission notice are included in copies or substantial portions of the software.

Copyright © 2026 Chris Athanas. See the [LICENSE](LICENSE) file for the complete license terms, including the warranty disclaimer.
