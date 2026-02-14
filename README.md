# rpeqw
An 'Equation Writer' utility for the HP 49/50 calculators which leverages the interactive RPN stack.

## Motivation
Ever since the HP 48 series introduced RPL, its variable length interactive stack has had tremendous potential for enabling users to build and manipulate complex mathematical and programming objects.

Nevertheless it is the considered view of this author that this initial promise was never truly fulfilled even with subsequent releases of the 49 and 50 series devices. As such, a fundamental issue remains with the official ROMs; namely, that the compromises necessary for a reasonable level of reverse compatibility with the original RPN paradigm, while at the same time incorporating certain features of modern line input of lengthy expressions and formulae has meant that users could never really replicate numerical expressions which perfectly match handwritten or printed ones 100 % of the time using only RPN entry methods. Indeed, RPL (and RPN before it) have always been known to simplify or evaluate numerical expressions on the fly.

To the best of this author's knowledge, no system flags or other built-in utilities exist which permit the deferment of simplification or numerical evaluation of expressions until the user explicitly executes EVAL or →NUM. This is where the 'RPN Equation Writer' utility provided in this repository comes in.

The main concept behind this utility is that it should ideally permit the user to build numeric and symbolic expressions, formulae and equations of arbitrary complexity using the interactive stack exclusively and permit matching a textbook or handwritten formula exactly, thus obviating the need for a separate equation writer app or algebraic line input altogether. The efficiency gains of such a feature seem to be self-evident, not to mention the resulting operational smoothness and ease of use inherent in sticking to RPN entry exclusively.

## Requirements
This utility makes extensive use of the →ALG and →LST routines included in Library 256; therefore, it must be attached prior to installing the RPN equation writer.

1. Ensure the active directory is set to HOME
2. Type `256 ATTACH` and press ENTER
3. Verify that the 'Developer lib' entry now appears at the bottom of the Apps menu

## Installation
1. Using an SD card or Kermit protocol over a standard mini USB cable, transfer either the [rpeqw.lib](https://github.com/d45h-d07/rpeqw/releases/download/v0.1.0-alpha/rpeqw.lib) library object or the [rpeqw.rpl](https://github.com/d45h-d07/rpeqw/blob/main/rpeqw.rpl) source file to your HP 49g+/50g calculator
   1. The rest of the instructions shall assume that the library file was chosen (menu 2269 has a library creator utility to package the source code). It is also strongly recommended to toggle system flag 117 to use soft menus.
2. Find the soft menu command corresponding to `rpeqw.lib` in the home directory and push its corresponding function key to place it on the stack
3. Now store it to a suitable port (e.g., `2 STO`)
4. Next, open the LIBRARY menu, select the appropriate port, and look for the soft menu entry `1613`
5. First press RSHIFT ALPHA(ENTRY), then hit the `1613` soft menu button to place its complete path on the command line, and then type ATTACH and press ENTER
6. Now go back to the main LIBRARY menu, and you should see an `RPEQW` folder soft menu entry in there -- press this key to go inside the menu
7. Press LSHIFT NEXT(PREV), and then the soft menu key corresponding to RPEQK (short for RPEQKEYS), which will take a second or so to generate the USER keyboard assignments for this utility
8. Enable the USER lock is enabled (LSHIFT ALPHA LSHIFT ALPHA, unless system flag 61 is set, in which case hitting this sequence just once will toggle the lock)
9. This utility is now ready for use -- try inputting some expressions using the interactive stack (see some demonstration examples below)

## Examples
For each of the examples below, start by toggling off the USER keyboard and try inputting these expressions directly into the interactive stack. Then lock the USER keyboard and try entering the same expressions again.

First, let us switch the calculator to Exact mode before trying any of the examples. Next, with the USER keyboard disabled, push '1.2 / 3' onto the stack.

Hit the SQRT button and then tell the calculator *not* to switch modes (we want to stay in Exact mode at all times) -- what happens? Now try the same exercise with the USER keyboard locked, using both partial (or fully) algebraic and pure RPN entry. Lastly, evaluate the expression once it's complete.

Here is a typical compounding amount calculation (again try it using the default settings followed by the USER keyboard, sticking with RPN all the way):

$$35689\left(1 + \frac{.057}{12}\right)^{144}$$

Now for a slightly more complex expression: on pp. 1-14 of the [HP 50g User's Guide](https://h10032.www1.hp.com/ctg/Manual/c00748644.pdf), the following formula is introduced:

$$\sqrt{\frac{3\left(5-\frac{1}{3\cdot 3}\right)}{23^3} + e^{2.5}}$$

Try it out using various methods of entry to see which you like best.

Finally, here is a typical probability calculation which one might encounter in a statistics class:

$$\frac{\frac{68}{306} - \frac{13}{298}}{\sqrt{\frac{68 + 13}{306 + 298}\left(\frac{1}{306} + \frac{1}{298}\right)}}$$

What is the best method to quickly replicate it exactly in the calculator, visually verify it's correct and then find the numerical result?

With Library 256 attached, it's also interesting to toggle between the →ALG, →LST and →PRG representations, so be sure to switch back and forth between them to get a better feel for the relationship between infix and postfix notations (actually, →LST and →PRG are essentially the same, except the former is a list object whilst the latter is an RPL listing with the usual User RPL delimiters dropped).

## Last but not least $\ldots$
I have endeavoured to stick to standard computational functions of the calculator as much as possible, but it seems the XROOT command doesn't play well with →ALG, likely because the $n^\text{th}$ root algorithm switches between different computational methods depending on all the permutations of the input argument types. Consequently, I have replaced it with my own routine which uses the multiplicative inverse of the second argument as the exponent -- this will likely have numerical implications, so results may not always match the equivalent computation done in normal mode (and the latter is more likely to be accurate).

Furthermore, in order to make it even easier to match typeset or handwritten formulae, I have provided a [textbook](https://github.com/d45h-d07/rpeqw/tree/textbook) variant in a separate branch, but this would of course introduce additional numerical inaccuracies, so please keep this in mind and periodically cross-check your results.