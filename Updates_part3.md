•  Annotating alternatives

a) You should use the concept <code>and-or</code> followed by 2 :ops whenever the sentence contains the alternative “and/or”.


```lisp
(c / component
      :mod (a / and-or
            :op1 (a2 / audio)
            :op2 (v / video)))
```            

<i>audio and/or video components</i>

b) You should use <code>slash</code> concept, followed by 2 :ops whenever the text contains 2 alternatives of the type “x/y”:

```lisp
(t / testify-01
      :ARG0 (s / slash
            :op1 (s2 / she)
            :op2 (h / he)))
```

<i>She/he testified.</i>


•  Use of <code>multi-sentence</code>

A sentence should be annotated as a multi-sentence if is or it ought to be split by an end-of-sentence punctuation (such as a period), so both in cases where that end-of-sentence marker has been omitted (due to sloppy writing, for example) and where it has not. AMRs should not depend on bad punctuation.

Please pay attention NOT to use co-reference beyond the sentence boundary, even if logically you know for instance that a certain person is the agent of both sentences. 

```lisp
(m / multi-sentence
      :snt1 (c / come-01
            :ARG1 (i / i))
      :snt2 (s / see-01
            :ARG0 (i2 / i))
      :snt3 (c2 / conquer-01
            :ARG0 (i3 / i)))
```

<i>I came. I saw. I conquered.</i>


•  Annotation of slang contracted forms

You should expand contractions such as <i>gotta keep'em to got to keep them</i> etc., just as we have been expanding more mainstream contractions such as <i>can't</i>, <i>we'll</i>, <i>it's</i>.

<i>gov't</i> should be treated like <i>government</i>, which we then represent as government-organization that governs.

The only exception: <i>friggin’</i> (should be kept as such)


•  Annotation of substances

We treat substances as "common nouns", not NEs, and that should apply to drugs as well. Named entities (NEs) are individuals, such as a specific animal (<i>Lassie</i>), as opposed to a class of entities (<i>dog</i>).

<b>Please remember!</b> In order to enter upper-case concepts such as LSD in the AMR Editor, enter !LSD (with a <b>!</b>) to overwrite the AMR Editor's default assumption that upper-case items are strings (and not concepts).

```lisp
      :op2 (l / like-02
            :ARG0 (i / i)
            :ARG1 (t / try-01
                  :ARG1 (o / or
                        :op1 (l2 / LSD)
                        :op2 (r / relative :quant 1
                              :ARG1-of (i2 / include-91
                                    :ARG2 (r4 / relative
                                          :poss l2))
```

<i>I'd like to try LSD or one of its relatives</i>


•  Annotation of slang variants of drugs/substances

We currently don't normalize synonyms such as <i>meth</i>, <i>LSD</i> to a canonical form: <i>methamphetamine</i>, <i>lysergic acid diethylamide</i> 

We do correct typos and expand true abbreviations such as <i>Dr.</i> -> <i>doctor</i> and <i>sen.</i> -> <i>senator</i>, but we keep acronyms such as <i>CEO</i> and <i>LSD</i> and we keep clipped forms such as <i>gym</i>, <i>phone</i>, <i>exam</i>, instead of expanding to <i>gymnasium</i>, <i>telephone</i>, <i>examination</i>

