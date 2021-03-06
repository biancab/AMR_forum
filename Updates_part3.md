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


•  Use of <code>have-06</code>

For expressions like:


> • have an accident
>
> • have a hotdog/food/tea
>
> • have consequences
>
> • have a trip 

In situation where you can go to a predicate, <i>have</i> should be dropped, e.g.:

<i>have shower</i> --> <code>shower-01</code>

<i>have a vacation</i> --> <code>vacation-01</code>

If there is a good replacement verb, please use it, e.g.: 

<i>have a hotdog</i> --> <code>eat-01</code> <i>hotdog</i>

<i>have tea</i> --> <code>drink-01</code> <i>tea</i>

<i>have a cigaratte</i> --> <code>smoke-02</code> <i>cigarette</i>; 


If it's not too much of a stretch to use <code>have-03</code>, use it. Example: <code>have-03</code> <i>time</i>

For other true support verbs such as <i>to have an accident</i>, we will use <code>have-06</code> for the time being.


•  Annotation of fractions

Fractions should be annotated as "x/y", rendered as text. 

```lisp
(e / equal-01
      :ARG1 (d / diameter
            :poss (p / planet :name (n / name :op1 "Jupiter")))
      :ARG2 (a / about
            :op1 (p2 / product-of :op1 "1/10"
                  :op2 (d2 / diameter
                        :poss (s / sun)))))
```

<i>The diameter of Jupiter is about 1/10 the sun's diameter.</i>


Typed variants of fractions should also be mapped to the numerical form.

<i>one third</i> --> <i>1/3</i>

<i>a fifth</i> --> <i>1/5</i>


•  Annotation of emphasis

Emphasis, as used in the sentence <i>I do like to eat icecream.</i> should be ignored for now.


•  Annotation of politeness

You should use <code>:polite +</code> to annotate "textual decorations" such as <i>please</i> and <i>would you kindly</i> that make a sentence more polite.

We don't use <code>:polite +</code> when something is inheritently polite (such as <i>You are a wonderful cook.</i>) or more indirectly polite (such as <i>It was not the most accessible textbook I have read.</i>).

However, <code>:polite +</code> is not limited to (semantic) imperatives such as <i>Could you please close the door?</i>
It can also occur with (semantic) questions. For example, <i>Could you tell me what time it is?</i> would be annotated as <i>What time is it?</i> with an additional <code>:polite +</code>

```lisp
(c / close-01 :mode imperative :polite +
      :ARG0 (y / you)
      :ARG1 (d / door))
```

<i>Please close the door.</i>


•  Annotation of completely censored words

If the sentence contains a completely censored word, you should annotate it using <code>thing</code>.

```lisp
(t / throw-01
      :ARG0 (l / life)
      :ARG1 (t3 / thing)
      :ARG2 (y / you)
      :time (t2 / time
            :quant (a / all)))
```

<i>Life throws **** at you all the time.</i>


•  Annotation of <i>commander</i>

<i>commander</i> can have several meanings, even when used with <code>have-org-role-91</code>:

(1) <b>specific military rank</b>, e.g. in U.S. Navy (corresponding to Lieutenant Colonel in Army)

(2) <b>somewhat generic term for high-ranking officers</b>, e.g. <i>Medvedev asked military commanders to come up with a plan.</i>


In these cases, <i>commander</i> shouldn't be decomposed.

(3) <b>person that commands an entity</b> e.g. <i>company commander, Ivanov, commander of Russian Military Space Force</i>

In this case, <i>commander</i> should be decomposed into <i>person</i>, :ARG0-of <code>command-02</code>


•  Annotation of frequency and other types of rates

There is a new frame available, called <code>rate-entity-91</code>, which is used to express frequencies and other rate entities, like <i>We meet several times a month</i>, <i>We talk every day</i>, <i>20 students per teacher</i> etc.

Please check out the frame and examples in the link below:

http://www.isi.edu/~ulf/amr/lib/popup/rate-entity.html


•  Annotation of wishes/greetings

If you have structures like <i>May God 's peace , mercy , and blessings be upon you</i>, <i>May Allah grant him patience</i>, may should be annotated using <code>wish-01</code>.

```lisp
(w / wish-01
      :ARG1 (r / rest-01
            :ARG1 (h / he)
            :manner (p / peace)))
```            

<i>May he rest in peace.</i>

The same approach should be used even in cases where <i>may</i> is not explicitly stated.

<i>Peace be upon you!</i>


For the part "be upon you"/"be upon him" etc., we suggest that you use the reification of <code>:beneficiary</code>, i.e. <code>benefit-01</code> or <code>receive-01</code>.


•  Annotation of <code>:time</code> <i>before</i> or <i>after</i> 

The purpose of the annotation method presented below is to provide consistency across all time structures built around a fixed point in time like <i>20 minutes ago</i>, <i>in 10 years</i>, <i>in the 2 months after ... </i>.

<i>after</i> should be used to express the time of an event which succeeds another (whether in the past or future):

```lisp
(l / leave-01
  :ARG0 (i / i)
  :time (a / after
          :op1 (n / now)
          :quant (t / temporal-quantity :quant 20
                   :unit (m / minute))))
```

<i>I will leave in 20 minutes.</i>

The <code>:quant</code> role indicates how much time has elapsed between the 2 moments.

```lisp
(i / interview-01
  :ARG0 (p / police)
  :ARG1 (p2 / person
           :ARG0-of (w / witness-01)
           :quant (m3 / more-than :op1 100))
  :time (a / after
          :op1 (m / murder-01)
          :duration (t / temporal-quantity :quant 2
                      :unit (m2 / month))))
```

<i>The police interviewed more than 100 witnesses in the 2 months after the murder.</i>

<code>:duration</code> indicates that the second action took place (several times) in a given time span after the first event.

<i>before</i> should be used to indicate that an event took place before another moment in time. <i>before</i> should replace <i>ago</i> in all structures of this kind:

```lisp
(r / retire-01
      :ARG0 (h / he)
      :time (b / before
            :op1 (n / now)
            :quant (m / multiple
                  :op1 (t / temporal-quantity :quant 1
                        :unit (y / year)))))
```

<i>He retired years ago .</i>

For more details and examples, please check the help page: http://www.isi.edu/~ulf/amr/lib/popup/time-before-after.html

