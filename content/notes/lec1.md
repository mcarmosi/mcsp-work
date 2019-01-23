---
title: Lecture 1 - Circuit Minimization Problem
---

$$
\newcommand{E}{\mathsf{E}}
\newcommand{NP}{\mathsf{NP}}
\newcommand{P}{\mathsf{P}}
\newcommand{PH}{\mathsf{PH}}
\newcommand{BPP}{\mathsf{BPP}}
\newcommand{ZPP}{\mathsf{ZPP}}
\newcommand{mcsp}{\mathtt{MCSP}}
\def\bold#1{{\bf #1}}
$$

# Lecture 1: Circuit Minimization Problem

## Introduction
These notes abstract [@DBLP:conf/stoc/KabanetsC00], which sparked
Western interest in the Minimum Circuit Size Problem ($\mcsp$). This
paper contributed a clear definition of MCSP, and formal evidence that
resolving the complexity of MCSP will be *difficult.* Kabanets and Cai
gave two kinds of evidence:

1. MCSP is Easy $\implies$ Circuit Lower Bounds \& Derandomization
2. A "simple" proof that MCSP is NP-hard $\implies$ Circuit Lower Bounds

Very roughly: "understanding the complexity of MCSP is as hard as
proving circuit lower bounds." Though we generally expect that circuit
lower bounds are *true*, there is formal evidence that they will be
hard to prove [@DBLP:journals/jcss/RazborovR97]. Thus, while we are
free to conjecture that MCSP is NP-complete, we expect this will be
difficult to prove.

Here we give: the basic definitions, a couple of results demonstrating
each type of implication, and an updated discussion of the open
problems from [@DBLP:conf/stoc/KabanetsC00].

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

### Required Background
You should be familiar with time-based deterministic,
nondeterministic, and randomized complexity classes. You should also
know the basic definitions of general circuit complexity. This
material is covered in chapters 1 - 7 of
[@DBLP:books/daglib/0023084]. Most introductory classes about
complexity theory will teach these topics during the first half of the
course. This note will define all other necessary concepts.

## What if MCSP is Easy?
If there is an efficient algorithm for MCSP, dramatic consequences for
both lower bounds and algorithms follow. Therefore, it should be very
difficult to give efficient algorithms for MCSP. For the duration of
this section, we assume:

:::: {.assumption title="MCSP is Easy"}
$\mcsp \in \P$ 
::::

<!-- The interested reader should ask: what is the minimal efficincy
assumption about MCSP, weaker than $\mcsp \in \P$, that suffices to
prove some version of each result? When are tradeoffs present, and
when not? -->

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

This section will just *state* this type of result without proof, and
point to notes on other topics that make these proofs in more detail. 

### Maximum-Complexity Functions in $\E^{\NP}$
It seems very difficult to exhibit uniform functions that are hard to
compute with general circuits. In this section we show that if MCSP
were *easy*, then we could produce functions that require *maximum*
circuit size in a uniform complexity class.

At each input length, there is some maximum circuit complexity. This
is a well-defined function for any number of bits $n$, though more
than one function might require the maximum circuit complexity at any
particular $n$.

:::: {.definition title="Maximum Circuit Complexity"}
$$MH(n) = \max_{f \in \mathcal{F}_n} CC(f)$$
::::

For each $n$, $MH(n)$ is the maximum number of gates *required* to
compute some function on $n$ bits. There could be more than one
function on $n$ bits that requires $MH(n)$ gates to compute. It is
natural to ask for the uniform complexity of computing such a
function.

Unconditionally, $\E^{\Sigma_2^P}$ can produce maximally hard
functions (**todo:** reference, link to proof?). We show that the
uniform complexity of maximally hard functions drops down to $\E^\NP$,
an entire "level" of the exponential hierarchy, assuming $\mcsp \in
\P$. This consequence seems dramatic, even though it is unclear if the
exponential hierarchy should be strict. We'll now proceed by
formalizing questions about circuit lower bounds into decision
problems, to support the proof.

To compute maximally hard functions, it would help to know $MH(n)$. To
find it, we'll define a conveniently padded language that corresponds
to determining the existence of $s$-hardness at a particular input
length.

:::: {.definition title="s-Hardness at length n"} 

The relation $H(n,s)$ is true if there *exists* a Boolean function on
$n$ bits that requires *at least * $s$ gates to compute. The following
padded decision problem codes this relation.  $$H(n,s) = \{ \langle
1^{2^n}, 1^s \rangle : \exists f \in \mathcal{F}_n. \langle f, (s-1)
\rangle \not\in MCSP \}$$

::::

To actually find a particular hard function, we'll define another
conveniently padded language that asks if the input string can be
extended to produce a truth table on $n$ bits that requires at least
$s$ gates to compute.

:::: {.definition title="s-Hard Prefix at length n"}

The relation $HP(x,n,s)$ is true if $x$ is the *prefix* of a Boolean
function on $n$ bits (considered as a truth table) that requires at
least $s$ gates to compute. The padded decision problem below encodes
this relation.

$$HP(x,n,s) = \{ \langle x, 1^{2^n}, 1^s \rangle : \exists y \in
\{0,1\}^{2^n - |x|}. \langle xy, (s-1) \rangle \not\in MCSP \}$$
::::

:::: {.theorem title="MCSP is Easy Implies Uniform Max-Complexity Functions"}
If MCSP is in P, then $E^{NP}$ contains a family of Boolean functions of
maximum circuit complexity.
::::

:::: {.proof}

This proof uses two steps. First, figure out what the maximum possible
circuit complexity on $n$ bits actually is. Second, use a standard
"extend the solution" self-reduction to search for the
lexicographically-first function of maximal circuit complexity on $n$ bits.

It is not important to obtain the lex-first maximally hard function;
it is just important to identify a *unique* such function at each
input length to ensure that our machine decides a well-defined
language. Any other insurance of uniqueness would also work (eg,
lex-last). On input $x$, run the following algorithm:

1. For $s$ from $2^n$ to $0$:
   a. if $H(n,s)$ then: $s^\star \gets s$ and break
2. Let $T$ be an empty binary string
3. Repeat until $|T| = 2^n$:
   * if $HP(T0, n, s^\star,)$ then: $T \gets T0$
   * Else, $T \gets T1$
4. Print $T[x]$, the value of $f_T(x)$

The point is that if $\mcsp$ is in $\P$ then HP and H are $\NP$
languages. This is because we need $co\mcsp$ to define these
languages; hardness is about when circuits of size $s$ do *not*
exist. If MCSP is in P, then coMCSP is also in $\P$ because $\P$ is
deterministic and thus closed under complement. So the inner relation
of both these languages can be computed in polynomial time. The
existential quantifier over truth tables, given $2^n$ bits of padding,
guesses a polynomial number of bits. So, both languages are in $\NP$.

Time required to produce the necessary padding to print H and HP
instances is $2^n$. So the above algorithm executes in $\E^{\NP}$
using the $\NP$ oracle to answer queries to H and HP. Since we start
$s$ at $2^n$, the algorithm will correctly identify the maximum
hardness $MH(|x|)$, discover the lex-first maximally hard function,
and answer accordingly. This completes the proof.

::::

### Derandomization into Zero-Error
The standard formalization of efficient randomized computation,
$\BPP$, allows randomized algorithms some small probability of
error. The "zero error" formalization of efficient randomized
computation, $\ZPP$, is required to *always* output the correct answer
or a special "don't know" symbol ($\bot$), and it may not output
'$\bot$' more than half the time.

Many open questions in complexity theory concern *derandomization,*
attempts to transform randomized algorithms in deterministic
algorithms, perhaps by allowing some additional time. The most
ambitions derandomization asks "does $\BPP = \P$?". But, this is just
one natural question. We could hope (somewhat more modestly) to remove
all possibility of error from efficient randomized algorithms. One way
to formalize this is to ask "does $\BPP = \ZPP$?". Under the
assumption that $\mcsp$ is easy, we can efficiently remove all errors
from any efficient randomized computation.

:::: {.theorem title="Hardness Tests Imply Derandomization into Zero-Error"}

If $\mcsp \in \P$, then $\BPP \subseteq \ZPP$

::::

The proof combines hardness-to-randomness trade-offs from
pseudorandomness with non-constructive circuit lower bounds and the
ability of a $\ZPP$ algorithm to toss coins. Briefly, we generate a
random truth table $T$. With high probability, $T$ is the truth table
of a hard function. Use the assumed $\mcsp$ algorithm to check if $T$
is a hard function. Since $\mcsp \in \P$, this procedure is
deterministic and error-free. If $T$ is not hard, print '$\bot$'. If
$T$ is hard, then use it to construct an efficient pseudorandom
generator (PRG). With a PRG, we can transform any $\BPP$ algorithm
into a fully deterministic algorithm, thus eliminating any possibility
of error. The only source of error in the above sketch is thus the
chance that we are *wildly* unlucky, and generate an easy $T$ at
random.

(**todo:** detailed proof of the above. actually define PRG and
compute bounds on size of $T$ necessary to prove the result.)

### Conclusions & Discussion of "Easy $\mcsp$"
We sketched three results demonstrating the consequences of efficient,
deterministic algorithms for $\mcsp$. Though all these consequences
seem dramatic, we can only use one of them as evidence that $\mcsp
\not\in \P$. Consider:

1. Though we only know how to produce maximally-hard functions in
   $\E^{\Sigma_2\P}$, for all we know $\E^{\Sigma_2\P} = \E^\NP$. It
   is not at all clear if we should believe the exponential time
   hierarchy is strict (**todo:** reference).
2. We expect far more dramatic derandomization than $\ZPP = \BPP$. In
   fact, reasonable circuit lower bounds imply that $\BPP = \P$, via
   the same hardness-to-randomness tradeoffs used to derandomize
   $\BPP$ under our assumption that $\mcsp$ is easy.
   

That being said, both the lower-bound and derandomization consequences
we get from $\mcsp \in \P$ seem beyond current techniques. So these
results at least show that exhibiting an efficient algorithm for
$\mcsp$ should be quite difficult.

On the other hand, if we believe in cryptography, we have to believe
in local pseudorandom functions (**todo:** reference). If $\mcsp \in
\P$, such objects *cannot exist,* as demonstrated above. So the
conclusion is: if we believe cryptographic assumptions, we *must*
believe $\mcsp \not\in \P$.


## What if MCSP is NP-Complete?

First, we define some reductions. Most NP-complete problems are
NP-complete under even very weak reductions.

:::: {.definition title="Many-one (Karp) Reduction"}

Let $A$ and $B$ be two decision problems. A many-one reduction $f$
from $A$ to $B$, denoted $A \leq_m B$, is some function $f: \{0,1\}^*
\to \{0,1\}^*$ such that:

$$
\forall x x \in A \iff f(x) \in B
$$

::::

By restricting the complexity of the map $f$, we produce efficient
reductions. The most natural is a $\P$-many-one reduction, where the
map is a function running in some fixed polynomial time.

:::: {.definition title="Natural Reductions"}

Let $A$ and $B$ be two problems. For any Karp (many-one) reduction
from $A$ to $B$ $f$,

::::

### High-Complexity Functions in E

### Derandomization into Subexp-Time

### Conclusions & Discussion

## Open Problems

## References


