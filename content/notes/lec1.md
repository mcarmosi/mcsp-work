---
title: Lecture 1 - Circuit Minimization Problem
---

# Lecture 1: Circuit Minimization Problem

## Introduction
These notes abstract [@DBLP:conf/stoc/KabanetsC00], which sparked
Western interest in the Minimum Circuit Size Problem (MCSP). This
paper contributed a clear definition of MCSP, and formal evidence that
resolving the complexity of MCSP will be *difficult.* Kabanets and Cai
gave two kinds of evidence:

1. MCSP is Easy $\implies$ Circuit Lower Bounds \& Derandomization
2. A "simple" proof that MCSP is NP-hard $\implies$ Circuit Lower Bounds

Roughly: "settling the complexity of MCSP is as hard as proving
circuit lower bounds." Though theorists generally expect that circuit
lower bounds are *true*, there is formal evidence that they will be
hard to prove [@DBLP:journals/jcss/RazborovR97]. Thus, while we are
free to conjecture that MCSP is NP-complete, we should expect that
this will be difficult to prove.

Here we give: the basic definitions, a couple of results from each
type of implication, and an updated discussion of the open problems
from [@DBLP:conf/stoc/KabanetsC00].

## Motivation
Valentine mentioned that he was interested in MCSP because of the
problem's connection to pseudo-randomness. At the time, breakthrough
hardness-to-randomness tradeoffs had just been completed
[@DBLP:conf/stoc/ImpagliazzoW97]. The utility of access to hard truth
tables was clear. Lacking circuit lower bounds, one motivation for
studying MCSP is "can we at least recognize a hard truth-table when we
see it?".

TODO: ask valentine for more commentary and stories.

## Definitions \& Preliminaries
We begin by formally defining the problem.

:::: {.definition title="Minimum Circuit Size Problem (MCSP)"} 
***Input:***
:    A Boolean function $f_n : \{0,1\}^n \to \{0,1\}$ given as a
truth table (length $2^n$) and a number $s_n \in \mathbb{N}$ (in
binary).

***Output:***
:    Is $f_n$ computable by a Boolean circuit of size at most $s_n$?

***Formally:***
: $MCSP = \{ \langle f, s \rangle : CC(f) \leq s \}$
::::

MCSP is clearly in NP. The maximum circuit size for any function is
$O(2^n/n)$, and we have $2^n$ bits of input. Therefore, an NP
computation has time to guess and check every possible circuit of size
less than or equal to $s$.

MCSP is linked pseudorandomness. But observe that it operates on the
*truth tables* of functions. So, if we want MCSP to interact with a
pseudorandom object, that object must be "local" in the following
sense:

:::: {.definition title="Local Pseudorandom Functions"}
A function $f$ is a local pseudorandom function against $\Lambda$ if:

$$ |\Pr_{g \sim G}[C^g = 1] - \Pr_{f \sim F_n}[C^f = 1]| < \epsilon$$

and the image of $g$ is locally computable in $\Lambda$.
::::

## What if MCSP is Easy?
If there is an efficient algorithm for MCSP, dramatic consequences for
both lower bounds and algorithms follow. Therefore, it should be very
difficult to give efficient algorithms for MCSP. For the duration of
this section, we assume:

:::: {.assumption title="MCSP is Efficient"}
MCSP is in PTIME
::::

Some of the results in this section should be provable under milder
assumptions, like "MCSP is in SUBEXP." 

### No Pseudorandomness
This is really about natural proofs; thus I'm not sure if it should be
included in these notes. Essentially we observe that MCSP is a
*better* Natural Property than any normal Natural Property, so we can
invoke anything in [@DBLP:journals/jcss/RazborovR97] or
[@DBLP:conf/coco/CarmosinoIKK16] up to and including:

+ No PRFGs in P/poly
+ Discrete Log is easy
+ Everything in P/poly can be learned
+ etc...

Actually, perhaps it is *very good* to include this section, because
then we can give a little roundup of the many applications of the
generic "Break a PRFG" idea that show up in this literature, and note
that this has been a trend in Western MCSP-studies since the paper
that started it all.

### Maximum-Complexity Functions in $E^{NP}$
At each input length, there is some maximum circuit complexity. This
is a well-defined function for any number of bits $n$.

:::: {.definition title="Maximum Circuit Complexity"}
$$MH(n) = \max_{f \in \mathcal{F}_n} CC(f)$$
::::

For each $n$, $MH(n)$ is the maximum number of gates *required* to
compute some function on $n$ bits. There could be more than one
function on $n$ bits that requires $MH(n)$ gates to compute.  To
actually find this number, we'll define a conveniently padded language
that corresponds to determining the existence of $s$-hardness at a
particular input length.

:::: {.definition title="s-Hardness at length n"} 
The relation $H(n,s)$ is true if there *exists* a Boolean function on
$n$ bits that requires $s$ gates to compute. We define the following
padded decision problem corresponding to this relation.
$$H(n,s) = \{ \langle 1^{2^n}, 1^s \rangle : \exists f \in
\mathcal{F}_n. \langle f,s \rangle \in MCSP \land \langle f, (s-1) \rangle
\not\in MCSP \}$$
::::

To actually find a particular hard function, we'll define another
conveniently padded language that asks if the input string can be
extended to produce a truth table on $n$ bits that requires $s$ gates
to compute.

:::: {.definition title="s-Hard Prefix at length n"}
The relation $HP(x,n,s)$ is true if $x$ is the *prefix* of a Boolean
function on $n$ bits (considered as a truth table) that requires $s$
gates to compute. We define the following padded decision problem
corresponding to this relation.
$$HP(n,s) = \{ \langle x, 1^{2^n}, 1^s \rangle : \exists y \in
\{0,1\}^{2^n - |x|}. \langle xy,s \rangle \in MCSP \\ \land \\ \langle xy, (s-1) \rangle
\not\in MCSP \}$$
::::

:::: {.theorem title="MCSP is Easy Implies Uniform Max-Complexity Functions"}
If MCSP is in P, then $E^{NP}$ contains a family of Boolean functions of
maximum circuit complexity.
::::

### Derandomization into Zero-Error

### Conclusions & Discussion

## What if MCSP is NP-Complete?


### High-Complexity Functions in E

### Derandomization into Subexp-Time

### Conclusions & Discussion

## Open Problems

## References


