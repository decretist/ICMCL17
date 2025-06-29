---
title: |
  The Vocabulary of Gratian's *Decretum*: Change Over Time
author: Paul Evans
bibliography: ../bib/ICMCL17.bib
csl: ../csl/chicago-fullnote-bibliography.csl
reference-section-title: Bibliography
suppress-bibliography: false
abstract: |
  The textual history of Gratian's *Decretum* is now understood
  well enough to enable researchers to compare different recensions
  of the text in order to identify evolutionary changes in its
  doctrine. Specific developments can be identified by close reading
  well-chosen selections from the text (e.g., Pennington, "The Law's
  Violence against Medieval and Early Modern Jews"). However, a
  systematic search for such doctrinal developments is best conducted
  with computational assistance, taking advantage of recent advances
  in the application of large language models to natural language
  processing tasks. Using the PIE lemmatizer in conjunction with
  the LASLA Latin models, it is possible to lemmatize samples
  reflecting different compositional stages of sections of the
  *Decretum* and to compare the results, isolating lemmas unique
  to specific stages in the development of the text. Distinctive
  vocabularies of different compositional stages revealed by this
  method then provide a roadmap for close reading.
---
This paper presents work that is part of a larger project to enhance
the effectiveness of close reading medieval texts, Gratian's
*Decretum* in particular, using computational assistance. The Digital
Humanities community uses the term "distant reading" to describe
this kind of computational assistance, emphasizing both its connection
to and its contrast with traditional close reading. Each project
that uses a distant or machine reading approach aims to answer
different questions, and therefore uses different tools and techniques.

The original project from which the current work grew was concerned
with the question of the authorship of the case statements and the
first- and second recension *dicta* in Gratian's *Decretum*, including
the *dicta* in *de Penitentia*. It employed stylometric authorship
analysis using a statistical technique from computational linguistics,
principal component analysis of the frequencies of commonly occurring
function words, to obtain its results. Its conclusion was that the
case statements were written by a single author who was not the
author of the *dicta* either in the first or second recensions or
in *de Penitentia*. Results from stylometric analysis for authorship
of the *dicta*, however, were not consistent with either the
one-author theory championed by Kenneth Pennington or the two-author
theory championed by Anders Winroth. Instead, the results suggested,
but did not conclusively prove, that both the first and the second
recension *dicta* were the work of multiple authors.[@evans_distant_2022]

In contrast, the current work concerns changes in the teaching or
doctrine of the *Decretum* between the first and second recensions
as indicated by the use of distinctive vocabulary in the *dicta*
of the two recensions. It employs another computational linguistic
technique, lemmatization, using the PIE lemmatizer and a large
language model (LLM) based on the LASLA
corpus.[@manjavacas-etal-2019-improving] The two projects share a
common data set. The original project relied on a very carefully
prepared data set of the texts of the case statements and the first-
and second-recension *dicta*.[^3] The current work uses the same
data set. The overarching goal of the two projects is the same---to
use computational distant reading techniques to enhance our close
reading of the *Decretum*---but each individual project attempts
to answer different questions using different tools and techniques
on the common data set.

This is not my first attempt to make progress on the problem of
computationally identifying topics added to the *dicta* between the
first and second recensions. Around 2012, there was tremendous
enthusiasm in the Digital Humanities community for a technique
called unsupervised topic modeling and in particular for a
topic-modeling tool called MALLET.[^4] Inspired by Pennington's
observation that most passages in the *Decretum* dealing with the
legal status of Jews, particularly those dealing with forced
conversion, were introduced only in the second recension,[^5] I
hoped to use MALLET to identify other new topics added in the second
recension. The approach was to topic model the first- and
second-recension *dicta* together, then separately, which would
show which topics were left when the first recension topics were
subtracted. (It would not be enough to just topic model the
second-recension *dicta* because many of the topics present in the
second recension *dicta* are also present in the first-recension
*dicta*.) This approach was simple in concept, but prohibitively
difficult in practice, for two reasons: first, because of the
difficulty in determining the number of topics to look for, a
necessary precondition for unsupervised topic modeling, and second,
because of the fact that there was no obvious way to subtract topics.

For the purpose of the discussion that follows, I am defining
"first-recension *dicta*" as the text of the *dicta* as they are
listed in the appendix of Winroth's *The Making of Gratian's
Decretum*, and I am defining "second-recension *dicta*" as the words
in the text of the *dicta* as they appear in the Friedberg edition
when the words in the *dicta* listed by Winroth in the appendix
have been taken away. D.54 d.p.c.23 is a good example, Winroth's
appendix indicates that only the first sentence of the *dictum*
appears in the first recension. Therefore, the first sentence of
the *dictum* is assigned to the first recension text sample:

> *Ecce, quomodo serui ad clericatum ualeant assumi, uel quomodo
non admittantur.* Liberti quoque non sunt promouendi ad clerum,
nisi ab obsequiis sui patroni fuerint absoluti. Unde in Concilio
Eliberitano:

The remainder of the dictum is assigned to the second recension
text sample:

> Ecce, quomodo serui ad clericatum ualeant assumi, uel quomodo non
admittantur. *Liberti quoque non sunt promouendi ad clerum, nisi
ab obsequiis sui patroni fuerint absoluti. Unde in Concilio
Eliberitano:*

By this definition, the first- and second-recension *dicta* contain
56,713 and 14,255 words respectively.

Once it became clear that unsupervised topic modeling using MALLET
was not going to be an effective way to identify topics added to
Gratian's *Decretum* between the first and second recensions, the
most promising alternative approach to the problem appeared to be
using lemmatization to identify distinctive vocabulary as an indicator
pointing to new ideas added between the first and second recensions.
When working in a highly inflected language like Latin, using words
as the indicators pointing to corresponding ideas is not sufficiently
precise. As an example that we will look at more closely later in
this paper, the noun *calumnia* has 6 declined forms. A regular
first conjugation deponent verb like *calumnior*, *calumniari*,
*calumniatus* has 120 conjugated forms, around 80 of which are
unique, not including participial forms. Therefore if we want to
use distinctive vocabulary as a basis for determining whether or
not an idea or topic is present in a Latin text, we need to lemmatize
every word form we encounter, that is, reduce it to its dictionary
headword or *lemma*. Once text samples for the first- and second
recension *dicta* have been reduced to corresponding lists of lemmas,
those lists can be compared to generate three further lists, (i)
lemmas that appear in both the first- and second-recension *dicta*,
(ii) lemmas that are unique to the first-recension *dicta*, and
(iii) lemmas that are unique to the second-recension *dicta*. It
is the list of lemmas unique to the second-recension *dicta* that
is relevant to the problem of topics added to the *Decretum* in the
second recension.

The results of my initial experiments with the Classical Language
Toolkit (CLTK), built on top of the Python Natural Language Toolkit
(NLTK) and the best lemmatization tool available at the time, were
not encouraging.[^6] The first- and second-recension *dicta* might
reasonably be expected to include a few hundred unique lemmas, but
CLTK reported many thousands (over four thousand just for the
first-recension *dicta*), the overwhelming majority of which were
false positives. Lemmatization was not ready for the purpose of
this project, and that remained the case for many years, from around
2014 through around 2020.

In early 2021, Mike Kestemont made me aware of the PIE lemmatizer.
Kestemont is a researcher at the University of Antwerp specializing
in medieval Latin and Middle Dutch literature and also a leading
figure in the field of computational text analysis. PIE is not an
application or program---the user does not simply type a command
or click a button and get lemmatized text as output. Instead, PIE
and PIE extended are a collection of libraries, packages, and
toolkits, that provide an extremely versatile set of software
building blocks that can be called upon to perform a wide range of
natural language processing functions, like part-of-speech tagging
or lemmatization, in a Python program.[^7] They are based on large
language models (LLMs) trained using machine learning techniques
on annotated corpora of texts in the target language. In this case,
I am using a model trained on the LASLA corpus of 1.7 million words
or tokens of classical Latin, each annotated with lemma, part of
speech, and other morphological and syntactic information. (If the
term large language model or the acronym LLM sound familiar, they
should. LLMs are the basis for the growing family of generative AI
tools, such as ChatGPT and friends, that have been the subject of
so much attention for the last several years.) Once the PIE
lemmatization environment had been set up, I wrote a Python program
that used PIE to create separate lists of every lemma found in the
first- and second-recension *dicta*, and then to compare the two
lists to identify lemmas that appear only in the second-recension
*dicta*. The program produced a list of 725 unique lemmas present
only in second-recension *dicta*.[^8]

An understanding of whether an idea or topic is present in or absent
from a selection of text can almost never be arrived at based on
the presence or absence of a single lemma. Instead, human, as opposed
to machine, readers must look for the presence of families of related
lemmas to indicate the presence of an idea or topic in a selection
of text. In reviewing the list of the 725 lemmas unique to the
second-recension *dicta*, one such family, all related to the concept
of calumny, stands out in particular. This family will be the
exemplar of what new computational techniques are able to reveal
about the evolution of the text and ideas of the *Decretum*.

Calumny is a promising lead because we know that between 1140 and
1234, what we think of as the classical period in the history of
medieval canon law, the concept of calumny took on a significance
and a formal legal meaning that was derived from but was considerably
more precise than its previous general use in Christian discourse.
For example, during this period, oaths of non-calumniation at the
onset of legal proceedings came to be required of all litigants in
canonical courts.

We should expect to see at least three Latin lemmas associated with
the concept of calumny:

+ the deponent verb *calumnior*, *calumniari*, *calumniatus* including
participial forms like *calumnians* and *calumniatus*,

+ the feminine noun *calumnia* corresponding to the idea of calumny
in the abstract,

+ and the masculine noun *calumniator*.

PIE does report three lemmas from this family among the 725 unique
to the second-recension *dicta*: *calumnia*, *calumniator*, and
*calumniatus*. It does not report the lemma *calumnior* because,
as we shall see, the word *calumniantibus* appears in a first-recension
*dictum*, and therefore the verb form does not appear on the list
of lemmas unique to the second-recension *dicta*.[^9]

[^9]: PIE reports the lemmas as *calumpia*, *calumniator*, and
*calumpniatus*. *calumpia* is almost certainly a typo in the LASLA
Latin language model for *calumpnia*. PIE reports the lemma of
*calumpniantibus* as *calumpnio*. The spelling is consistent with
the orthographic conventions of the Friedberg edition, from which
the text samples of the first- and second-recension *dicta* are
ultimately derived.

When we turn our attention to the substantive treatment of the topic
of calumny in the *dicta*, there is variation in terms of the legal
sophistication with which the concept is handled, moving generally
in the direction of greater technical precision and sophistication.
(I say "generally" because while we can assume the first recension
*dicta* were written before the second recension *dicta*, we do not
have enough information to speculate about the temporal relationship
among the second recension *dicta*.)

<!-- Introduce table here. -->

The concept of calumny makes its initial appearance in the form of
a slightly misquoted scriptural reference in the first-recension
*dictum* C.24 q.3 d.p.c.9:

> Ait enim Christus in euangelio: "Orate pro persequentibus et
calumpniantibus uos, benefacite his, qui oderunt uos."

The treatment of the concept in the second-recension *dictum* C.23
q.4 d.p.c.23 §3 is in a similar spirit, although there the scriptural
allusions are mediated through a patristic source, Augustine's *de
Dono perseverantiae*, a treatise on predestination.

> "Quare autem hoc negatum eis fuerit, dicant, si possunt, qui
calumpniantur, et ostendant, cur apud eos Dominus mirabilia, quibus
profutura non erant, fecerit, et apud eos, quibus erant profutura,
non fecerit."

Both of these *dicta* use the words associated with the concept of
calumny in the same general, non-technical, sense they had in the
first millennium of Christian discourse.

That is not the case in the second recension *dictum* C.23 q.3
d.p.c.8. Here we see a series of quotations from book 48 of the
*Digest*, containing <!-- 7 words, 5 of them unique --> 7 occurrences
of 5 words, corresponding to all 4 of the expected lemmas related
to the concept of calumny. It is of obvious interest that the
quotations in this *dictum* are from Justinianic Roman law rather
than from scriptural or patristic sources. And most interesting of
all is the fact that the *dictum* contains two first-person sayings
by the author of the second-recension *dicta* (or at least of this
*dictum*), in effect glossing the terms *calumniator* and *calumnia*.
While Gratian's own intervention is relatively modest, the *dictum*
shows progress toward greater legal sophistication in the sense
that the discussion draws on resources from Justinianic Roman Law.

### Conclusions

The long-term goal of this  project has has been to find a way to
use computationally-enabled distant reading---"reading machines"
in the words of Stephen Ramsay---to efficiently direct the attention
of scholars to specific sites in the text of Gratian's *Decretum*
where new topics added between the first and second recensions are
likely to be found by close reading.

I think this effort was successful as a proof of concept. Using the
PIE lemmatizer in conjunction with the LASLA Latin large language
model (LLM) to systematically lemmatize every word in the first-
and second-recension *dicta* and then to list all of the lemmas
that *do* appear in the second-recension *dicta* but *not* in the
first-recension *dicta* drew attention to a family of lemmas
(*calumnia*, *calumniator*, and *calumniatus*) that indicated the
treatment of a canonically significant concept, calumny. On close
reading, the sites in the text of the *dicta* identified by the
results did indeed show a meaningful development over time in the
vocabulary of Gratian's *dicta* and to that extent in the teaching
or doctrine of the *Decretum* on this topic. The detection of
calumny as a topic that the authors of the *Decretum* developed in
a significant way in the second recension demonstrates the usefulness
of lemmatization as a technique for investigating this type of
question.

Calumny was the most obvious topic (at least to me), and I was
surprised that there were no other such immediately obvious
conceptually related families of lemmas in the results, although I
strongly encourage interested readers to examine the complete list
of lemmas unique to the second-recension *dicta* for themselves.[^10]
As previously indicated, there is limited value in the results of
machine reading by itself. The real value of the results of machine
reading lies in the patterns that trained researchers see in them.

Is it enough? No.

I have tried to emphasize that the project I have discussed in this
paper is very much a work in progress and that the results, although
interesting, are limited to the *dicta*, and therefore should not
be taken as anything more than a proof of concept.

An unsystematic search through the MGH e-text of the Friedberg
edition that was created for the *Wortkonkordanz zum Decretum
Gratiani* edited by Reuter and Silagi indicates that there are
occurrences of forms of the words I have been focusing on---*calumnia*,
*calumnior*, and *calumniator*---in the rubrics and canons.[^11] A
thorough approach to the problem of systematically identifying new
topics added to the *Decretum* between the first and second recensions
will therefore require a data set that includes the rubrics and
canons with their inscriptions as well as the *dicta* and case
statements.

Ideally, such a data set would be in the form of a new e-text in
TEI-P5 XML format incorporating texts from both the old Friedberg
edition and the new Winroth edition-in-progress of the first
recension. This is where the scale of the undertaking becomes really
challenging. Even without the overhead of structuring the data set
as a TEI-P5 document, I spent approximately 12 person-weeks on
corpus preparation for the *dicta* and the case statements as part
of my dissertation project. Since the word count of the canons is
roughly five times that of the *dicta*, one person-year is not an
unreasonable initial estimate for corpus preparation for a comparable
data set for the canons.

The work I have discussed in this paper is based on a highly
customized version of a twentieth century e-text of a nineteenth
century print edition of the *Decretum*. The MGH e-text of the
Friedberg edition is the indispensable free resource without which
none of my work, and I suspect the work of many others, would be
possible. But like so many free things in life, someone paid a great
deal of money to make it free, in this case, the taxpayers of the
State of Bavaria and the Federal Republic of Germany in the 1980s
and 1990s. However, the MGH e-text is a resource that because of
its archaic format is approaching the end of it useful life. If we
want to continue to advance in our understanding of Gratian's
*Decretum* with the help of electronic resources, we need to invest
time, effort, and grant funding into a twenty-first century electronic
text, or better still an electronic edition, of Gratian's *Decretum*
that meets 21st century research needs.

![Table](Table.png)

<!--
[ICMCL XVII – Congress Programme](https://sites.google.com/view/icmcl2024/academic-programme/congress-programme)
Tuesday (9 July): Cathedral Conference Suite
15.30-17.00: Sessions VI
Session 18: Texts and Manuscripts in the Age of Gratian and Beyond
Room: Clagett Auditorium Balcony.
Moderator: Anders Winroth, University of Oslo, Norway.
Speaker 18b: Paul Evans, University of San Diego, USA.
'The Vocabulary of Gratian's Decretum: Change Over Time'
The maximum duration of each presentation (not inclusive of questions) is:
Speakers in sessions lasting 90 minutes and comprising three presentations:
20 minutes.
-->

[^3]: This research could usefully be expanded to include the rubrics
and canons, and I have made preparations to do so. The work required
to expand the corpus to include the canons themselves would
realistically require grant funding.

[^4]: MAchine Learning for LanguagE Toolkit  
@McCallumMALLET

[^5]: @pennington_laws_2013; and @pennington_gratian_2014.

[^6]: Python is a widely-used general-purpose programming language.
According to one frequently-cited industry metric, the [TIOBE
Index](https://www.tiobe.com/tiobe-index/), Python is the most
popular programming language worldwide as of June 2025. Python
provides powerful features for performing operations on textual
data.

[^7]: I would like to acknowledge Jake Bayon, an undergraduate
Computer Science student at the University of San Diego, who set
up the PIE lemmatization environment as an independent study project
with me during the Spring 2024 semester and who learned something
about Gratian in the process. PIE can only be installed with the
2019 Python 3.8 release---the current release is Python 3.13.

[^8]: The 728 lines of program output included 3 numbers, which I
discarded. The complete list is available at
[https://github.com/decretist/ICMCL17/blob/main/results/lemmas.txt](https://github.com/decretist/ICMCL17/blob/main/results/lemmas.txt).

[^10]: The complete list of 725 lemmas unique to the second recension *dicta*
is available from my GitHub repository for the Seventeenth International Congress of Medieval Canon Law at
[https://github.com/decretist/ICMCL17/blob/main/results/lemmas.txt](https://github.com/decretist/ICMCL17/blob/main/results/lemmas.txt).

[^11]: See, for example, the rubrics for D.9 c.9 (R1), D.87 c.9 (R2),
C.3 q.1 c.6 (R1), and C.5 q.5 c.8 (R2)
