---
title: Open Problems
---

Currently, these problems are just sorted by the order in which they were emailed to me. As we accumulate more problems, I will organize them by topic instead.

* **MCSP for Weak Classes:** We could study variants of MCSP such as: finding the sparsest polynomial threshold function, the sparsest linear combination of degree-2 polynomials, etc. In some cases (e.g. find the lowest degree threshold function) the problem is known to be in P. Scott Aaronson had a [paper](https://arxiv.org/abs/cs/0107010) about this. (contributed by: Ryan Williams)

* **Establish that FO Reductions to MCSP are Unlikely:** Prove a theorem of the form (MCSP is NP-complete under uniform AC^0 m-reductions) implies (something unlikely). *[I  have trouble believing that such a reduction really exists.  I'm less sure, when it comes to nonuniform reductions. -- Eric]* (contributed by: Eric Allender)

* **Unconditional Circuit Lower Bounds for MCSP:** Prove that MCSP is not in AC0[2]. We know the related problem MKTP (which measures the time-bounded Kolmogorov complexity of a string) is indeed not in AC0[p], by two distinct proof techniques: a reduction from Determinant of [[Allender, Hirahara 2017]](http://drops.dagstuhl.de/opus/volltexte/2017/8063/pdf/LIPIcs-MFCS-2017-54.pdf) and a pseudorandom generator argument of [[Hirahara, Santhanam]](http://drops.dagstuhl.de/opus/volltexte/2017/7540/pdf/LIPIcs-CCC-2017-7.pdf). Proving the bound for MCSP should be possible. (contributed by: Eric Allender).
