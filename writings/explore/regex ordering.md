# problem

Order regular expressions by the power of their languages.

Extension goal 1: make it total
Extension goal 2: make it cacheable (ideally, derive some precomputed value with easy comparison)

## occurence

One time I was working on a rule engine for the web where metadata and other rules were to be applied to web pages based on some URL patterns.
Patterns and rules were changing too often to keep them encoded in the codebase.
Apparently pattern matching features were sufficiently covered by regexes, and related rules could be fetched based on what patterns matched what URLs.
The issue arises when there is more than one matching pattern.

# rejected solutions

## manual ordering (nonsolution)

The possibly simplest solution imaginable could be attaching a global manual ordering property to the pair of pattern-rules.
But that would in essence just put the burden of *total* ordering patterns on a person.
Even with all included tools, like being able to quickly find what kinds of pages what patterns apply to, and what patterns were applied in what order to a page, it is too burdensome and inprecise.

And the other thing is, such solution cannot be total.

## numerical estimation

Since the grammar for URL is limited (G), and the reasonable size of a URL is also limited (L), potentially a purely numerical solution could be derived (not enumeration).
This way a fixed numeric rank could be assigned for all regular expressions, resulting in total ordering.
In could maybe solve the original problem more accurately in some cases, but maybe less precisely in others if using floating point arithmetic.
I see three possible approaches:
1. Ground truth - derive and solve equations from the patterns and subpatterns that would take L into account. This should take into account all combinations of all permutations of subpatterns.
2. Heuristic A - for all kleene stars just count the number of permutations (with repeats) for G from 0 up to L (a geometric series formula?) and then multiply all, do this recursively. This does not look correct since it would include patterns that exceed L by a "lot".
3. Heuristic B - divide maximum allowed "entropy" (L) between subpatterns and then count permutations, and then multiply.

The problem is, my intuition about this is poisoned in such a way that the system-1 estimated magnitudes seem much lower than ones acquired through rigor. It seems that such solution will be too inaccurate to discern regexes even with 1 position of a constant symbol of difference.

Another thing is, since there are so many preconditions, this solution is terribly non total and too subjective and fallible.

## duct taping

Fortunately, in my case, the required regular language was much less powerful than PCRE - more like a step up from globbing.
Remapping the domain of "regular parts" (constant expressions, alterations, dicts and wildcards) onto a simple language (decimal numbers...) based on some heuristics.
Provided strings then could be ordered lexicographically and resulting ordering satisfied all neccessary cases.
The solution is not total at all, but worked because all regexes were matching the same string, so a total ordering wasn't neccessary in the first place.
But the solution is also not entirely correct for all possible cases within this system, it only solves actually used cases, basically an opportunistic duct taping.

Well, this is bad since it is not only not total, but also simply invalid within the defined range.

# other potential solution insights

## infinity comparison

I hope I'll ever come around to testing an approach where I try to count power of infinities for the regular expressions and order them by that.
Such solution will also probably not allow total ordering, but it will be able to more accurately solve the original task.
I also have a feeling that it won't be total for the subset of a more global problem as well (only ordering expressions that match the same string, and thus have intersecting language).

## automaton analysis

Something could probably be done by carefully analyzing the expressions and comparing their parts. There is some research on related properties of regular languages and corresponding automatons.

## asymptotic analysis

Another idea is to reduce languages to the DFA and see if it has cycles to determine finiteness. For finite languages we could compute a total number of strings, and for infite languages we could compare growth rates (asymptotic profiles). Growth rates alone wouldn't suffice, so a constant would also need to be extracted. At this point possibly the same flow could be used for finite languages if it is as performant. While such attributes seem hard to compute they are at least as well seemnigly decidable, and "absolute", so in worst case are trivially cacheable.

After acquiring these numbers, we could compare them from most to least significant to get a good estimate for the ordering.

- [Finding the growth rate of a regular language in polynomial time](https://arxiv.org/pdf/0711.4990)
- [A characterization of poly-slender context-free languages](https://www.numdam.org/item/ITA_2000__34_1_77_0.pdf)

# observations

## definability

Some say that total ordering of regular languages cannot be defined, related to how languages can contain the other, partially intersect or not intersect at all.

## complexity

The complexity of the problem explodes if we try to also measure this for more complicated regular languages, like PCRE, that allow for lookaheads. Backtracking is also complicated.

## sugar

Some regular expression features can be seen as sugar and therefore simplified to other equivalent expressions, e.g. unrolling wildcards: `..* === .+`.
Something of this sort should already be happening inside a regex engine.
For the purpose of only answering whether the expression matches the string, e.g. following kinds of equivalence could be made `^abc === ^abc.*`.
They would not be applicable to regular expressions in more general sense.

## canonization of redundant parts

It seems apparent that beside desugaring, a pass to remove redunand pieces is mandatory to simplify further computations, for example, like joining `.*.*` => `.*`.

## canonization of constants

For the purpose of comparison of sets, the particular alphabet and used symbols actually do not matter (proof?). Since we are comparing by cardinality (the language size), not the actual symbols of language. Apparently, expressions like `aa` `bb` `ab` would self evidently have the same cardinality `1`. So in the comparison engine only the number denoting the lenght of the constant string has a significance.

## canonization of order of sub expressions

For the purpose of cardinality comparison, the order of the parts of the expression, and its sub expressions (not the order of _tokens_ that make up the regular language), does not matter as long as cardinality stays the same. This has an effect that a canonic form can be achieved using some defined order which might simplify further computations. This can for example potentially improve the duct taped solution by compensating token order related errors of lexicographic sorting.

Ordering can be done from most to least significant sub expression in terms of its size, down to the level at which size can be trivially compared.

The important distinction has to be made such that the resulting expression should not be equated to a normal epxression for the purpose of some other canonizations. Two expressions `.*a.*` and `.*.*a` can be canonized as `.*a.*` and `.*a`, and then order-canonized as `.*.*a` and `.*a` - and here the further joining cannot be applied, since this form is in a sense a "view" into the original expression, otherwise important information about cardinality will be lost. Therefore it is even better to avoid expressing order-canonical in such a form.

# materials

- [Regular Expression Matching Can Be Simple And Fast](https://swtch.com/~rsc/regexp/regexp1.html)
- [Derivatives of Regular Expressions](https://lcs.ios.ac.cn/~chm/papers/derivative-tr200910.pdf)
- [Derivatives of Regular Expressions - Janusz A. Brzozowski (Modified)](https://github.com/katydid/regex-deriv-coq/blob/main/src/Brzozowski/Derivatives%20of%20Regular%20Expressions%20-%20Janusz%20A%20Brzozowski.md)
- [Rewriting Extended Regular Expressions](https://tidsskrift.dk/daimipb/article/download/6934/5897)
- [Testing the Equivalence of Regular Languages](https://arxiv.org/pdf/0907.5058)
- [Regular-expression derivatives reexamined](https://www.khoury.northeastern.edu/home/turon/re-deriv.pdf)
- [DFA minimization](https://en.wikipedia.org/wiki/DFA_minimization)
- [Brzozowski derivative](https://en.wikipedia.org/wiki/Brzozowski_derivative)
- [Testing the equivalence of regular expressions](https://www.dcc.fc.up.pt/Pubs/TR07/dcc-2007-07.pdf)
- [regexpr-symbolic on hackage](https://hackage.haskell.org/package/regexpr-symbolic)
- [Equality, containment and intersection among regular expressions via symbolic manipulation](https://sulzmann.blogspot.com/2008/12/equality-containment-and-intersection.html)
- [Partial derivatives of regular expressions and finite automaton constructions by Valentin Antimirov](https://pdf.sciencedirectassets.com/271538/1-s2.0-S0304397500X00084/1-s2.0-0304397595001824/main.pdf?X-Amz-Security-Token=IQoJb3JpZ2luX2VjEEUaCXVzLWVhc3QtMSJIMEYCIQDEJpZjroDezSmvQOkqG5g7Kr%2BKDBipQRHf2ueXwL1DTAIhANB8Nj%2BzmVki9hrxTwzbQCEbx8RsiuFr2J1VwEpiHq0QKrMFCH4QBRoMMDU5MDAzNTQ2ODY1IgwF5C4x30Yzg4UocywqkAUIvcTc1lRQpMY%2F5%2Beccr6ND5nHEOCJPXwa39ATwJtHTOBymOqYSTZLOgS7lrArtMVakBJymzKpSoz%2BHRcGh1xrtJ0NXzWfBryaYcuQbSvG%2FRvJi6GVMkeXt4N3xE3fZWIkTK3sCHzvtetgEN2xZatroHURtuBKDE%2BuuDgIEfbMg5FkCH54zK8xwDn3meqEvuaLUeSnMK%2BgvVpfBwdtj9k24B14Pe1BYXMAHXlhfzUALqtSK7vYKpzPr4I%2Bs6OEsPXhYDtgYTZ2qRJaiBbXvTODE47WLT1xG3oaYcz6TppNQ4%2F1umUzgpdDqec%2BD0wHTu5ia4w26R938vrliEuh7ITkFpMJ9XCVtuCPbqIWqANTKS%2Bd3ziSkOVFyQg5Ff%2BhvJ3SPaRin%2FITyDLzbVQZN%2Bf5UEOFcvZeMPvef4GTGwOgiAGpiIJIB%2BSJv6L2ztc7ofJ81R9%2FLpSXPil1j%2BM%2FSqW%2B33NA7aa8SUREYikXlFmqCzFQeUpfkjwR3XhYNQ9FCy6soW%2B7y5IFac9e1BQSniXld0ujDAsZ3R7RYxrZgNcoDmofLix%2B2PMgb6x39ljmFH5TVfHSDK9O5M3Z4P7%2FU8rkUboprjL8mbLIJJGudCbYkk1f%2FKMPUA%2F1LaHftKJUNGgVlSTI47TMd5o0ARbH5gY2jbb0uY35%2FfHjB9n8NxNtf5EFVG881CPtrE%2Fq%2FnQTwN7VgExLwKCsQE31efJX1AI8VuTJRgPhGvhxSUEXU0hTsCSNTqMU9yKZUQF7bIqO%2Fv6Wz45leV%2BiRH%2FEUVORqbkE6f1rn13YQ5bURXx34oHfQD%2FOyMKQ0dxtILynhCN70BSgQMAQqEu9r4W6BH0HKtbBvL0CuyeCijURE9MHyme6FTCNoYO%2BBjqwAd%2F4wvBhiogJBrroHQTEYCMpzr6xYdGSyrTZX%2FJ4xLF%2FFh3t60JbpK0gnrbR%2BxyaTXr%2FnpxmhdbQtlIwozJE0D4j4c1pkiX8aRXni8HU08utwPI3IzsULFgpkYP5Ycqgnk0iUQv5T7oQ03mYVF%2BsAaq3slXjXbl%2FAqm8a7N%2BkwhYM023uQiDC2opXw%2FiYSFNLe2%2BztYqw%2FOcAX2Nzklbpo08KkFBRL%2B2oPEf7tcpz3J0&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20250227T213636Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAQ3PHCVTYTN2A6TH3%2F20250227%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=4bb717bcd83fb0b6e22094dd047ab066e0291eab29970fcec68c2fa02e7684fc&hash=9b2a99f879d1b4d0a63ea33e76443ff8e186aaeaaac56a9a61ee433d254c5b44&host=68042c943591013ac2b2430a89b270f6af2c76d8dfd086a07176afe7c76c2c61&pii=0304397595001824&tid=spdf-8c22af76-e505-42b3-bda5-95de7ad03e1c&sid=278d522e3d66a9482f0a7aa63b840516ba7egxrqb&type=client&tsoh=d3d3LnNjaWVuY2VkaXJlY3QuY29t&rh=d3d3LnNjaWVuY2VkaXJlY3QuY29t&ua=17135d53570353010252&rr=918b4fb58db10a18&cc=ru)
- [Burrows-Wheeler transform](https://en.wikipedia.org/wiki/Burrows%E2%80%93Wheeler_transform)
- [Wheeler graphs: A framework for BWT-based data structures](https://www.sciencedirect.com/science/article/pii/S0304397517305285)
- [Ordering regular languages: a danger zone](https://arxiv.org/abs/2106.00315)
- [Co-lexicographically Ordering Automata and Regular Languages -- Part II](https://arxiv.org/abs/2102.06798)
