---
title: Open Problems
---

# Open Problems

Currently, these problems are just sorted by the order in which they
were emailed to me. As we accumulate more problems, I will organize
them by topic instead.

- **MCSP for Weak Classes:** We could study variants of MCSP such as:
  finding the sparsest polynomial threshold function, the sparsest
  linear combination of degree-2 polynomials, etc. In some cases
  (e.g. find the lowest degree threshold function) the problem is
  known to be in P. Scott Aaronson had a
  [paper](https://arxiv.org/abs/cs/0107010) about this. (contributed
  by: Ryan Williams)

- **Establish that FO Reductions to MCSP are Unlikely:** Prove a
  theorem of the form (MCSP is NP-complete under uniform AC^0
  m-reductions) implies (something unlikely). _[I have trouble
  believing that such a reduction really exists.  I'm less sure, when
  it comes to nonuniform reductions. -- Eric]_ (contributed by: Eric
  Allender)

- **Unconditional Circuit Lower Bounds for MCSP:** Prove that MCSP is
  not in AC0[2]. We know the related problem MKTP (which measures the
  time-bounded Kolmogorov complexity of a string) is indeed not in
  AC0[p], by two distinct proof techniques: a reduction from
  Determinant of [Allender, Hirahara 2017][AH17] and a pseudorandom
  generator argument of [Hirahara, Santhanam 2017][HS17]. Proving the
  bound for MCSP should be possible. (contributed by: Eric Allender).

- **Show that various results about MKTP also hold for MCSP:** For
  example, prove:
	- DET AC^0-many-one reduces to MCSP
	- Graph Isomorphism is in ZPP^MCSP
	
	(contributed by: Eric Allender)

- **NP-Hardness for restricted MCSP:** Either prove that MCSP for
  depth-3 AC^0 circuits is NP-complete, or understand why this is
  unlikely. The state of the art is a proof that MCSP for
  DNF-of-parities is NP-complete by 
  [(Hirahara, Oliveira, Santhanam 2018)][HOS18]. (contributed by: Eric Allender)

- **SZK-hardness for restricted MCSP:** Show that the minimum formula
  size problem is hard for SZK, or is at least hard for GI, under,
  say, P/poly reductions. (contributed by: Eric Allender)

- **Formal Relationships between MCSP and MKTP:** We know some
  settings in which (MCSP^A is hard for a class) implies (MKTP^A is
  hard for a class) from [(Allender, Hirahara 2017)][AH17b].  Can
  stronger results in this direction be proved? (contributed by: Eric
  Allender)
	

[AH17]: http://drops.dagstuhl.de/opus/volltexte/2017/8063/pdf/LIPIcs-MFCS-2017-54.pdf

[HS17]: http://drops.dagstuhl.de/opus/volltexte/2017/7540/pdf/LIPIcs-CCC-2017-7.pdf

[HOS18]: http://drops.dagstuhl.de/opus/frontdoor.php?source_opus=8883

[AH17b]: http://drops.dagstuhl.de/opus/volltexte/2017/8063/
