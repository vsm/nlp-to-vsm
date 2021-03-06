# nlp-to-vsm
**Converting NLP dependency trees, to semantic structures in VSM.**

This is a project for the 7th Biomedical Linked Annotation Hackathon ([BLAH7](https://blah7.linkedannotation.org)), with a focus on **Covid-19 literature**.

Demo of work-in-progress: [vsm.github.io/nlp-to-vsm](https://vsm.github.io/nlp-to-vsm).

Overview:

<img src="img/nlp-vsm-etc.svg">

Presentation video:

[![](http://img.youtube.com/vi/0kHWBZIL04E/0.jpg)](http://www.youtube.com/watch?v=0kHWBZIL04E "Animation: From a natural language sentence to a VSM semantic structure.")


## Goal
We want to map the dependency trees of NLP, onto the intuitive semantic structures of [VSM](https://vsm.github.io) (Visual Syntax Method).

"Covid-19" is the theme of the hackathon, so we would like to:  
• focus on **Covid-19 literature**,  
• design how Covid-19-related **syntax trees** can be **converted to VSM semantics**,  
• discuss how this can facilitate **semantic queries** over multidisciplinary Covid-19 knowledge, in a form that **biomedical end-users can grasp**.

### About VSM
VSM is an intuitive way to represent any contextualized knowledge on any topic, in a form that is semantically precise and also easy to understand. Biologists and others often tell they find VSM intuitive because it shows computable knowledge in a form close to _"how they think"_.

VSM is both a **knowledge representation** and an **interface** for entering, editing, or simply displaying knowledge in this form – the latter is the use-case for this project.  
All info on VSM is on [**vsm.github.io**](https://vsm.github.io), &nbsp;see esp. the [vsm-box](https://vsm.github.io/demo) demo and the [causalBuilder](https://mi2cast.github.io/causalBuilder) use case.

When context-rich knowledge is represented in VSM,  
• it can be placed in a [**vsm-box**](https://github.com/vsm/vsm-box) user-interface, where it becomes easy to read, **edit**, or correct by biologists – which may serve as feedback for NLP;  
• the knowledge is then **formalized and queryable** – via [**vsm-to-rdf**](https://github.com/vsm/vsm-to-rdf).


<br>

## Concrete project

### Project option 1:&nbsp; Enju –> VSM

We could use the output of the [Enju](https://mynlp.is.s.u-tokyo.ac.jp/enju) deep parser (Covid-19 corpus [coming soon](http://pubannotation.org/projects/LitCovid-sample-docs)), and design rules (or apply ML) to convert this to VSM-structures.  
This means that:
- all relevant entities should ideally be mapped onto a readable string + an identifier (e.g. URIs, see also [vsm-PubDictionaries](https://github.com/UniBioDicts/vsm-pubdictionaries) and  [paper](https://doi.org/10.37044/osf.io/gzfa8)),
- these term+ID units should be meaningfully connected with ‘VSM-connectors’ – which express an elementary semantics with: • triples (always `relation-entity has-subject subject-entity; has-object object-entity`), • couples, • lists, and • coreferences – as described in the [VSM paper](https://www.preprints.org/manuscript/202007.0486).

**Covid-19 literature** spans across **multiple** biological scales, and covers multiple research areas. Nevertheless, knowledge from any of these areas can be represented in the same, quick-to-understand semantic form of VSM (second image below).

For example this Enju output (from [PubAnnotation.org](http://www.pubannotation.org), bottom image), on a subject within molecular biology :

<img src="img/enju.svg">

could be transformed into a VSM-sentence like this:

<img src="img/vsm.svg">


<br>

This VSM-sentence corresponds to the JSON below: &nbsp;(or [go here](https://vsm.github.io/demo/?vsm=%7B+terms%3A+%5B%0A++++%7B+str%3A+%27production+of%27%2C++classID%3A+null%2C+instID%3A+null%2C+style%3A+%27i11-13%27+%7D%2C%0A++++%7B+str%3A+%27ROI%27%2C++++++++++++classID%3A+null%2C+instID%3A+null+%7D%2C%0A++++%7B+str%3A+%27and%27%2C++++++++++++classID%3A+null%2C+instID%3A+null%2C+descr%3A+%27a+set+of+items%27+%7D%2C%0A++++%7B+str%3A+%27activation+of%27%2C++classID%3A+null%2C+instID%3A+null%2C+style%3A+%27i10-13%27+%7D%2C%0A++++%7B+str%3A+%27NF-kappaB%27%2C++++++classID%3A+null%2C+instID%3A+null+%7D%2C%0A++++%7B+str%3A+%27could%27%2C++++++++++classID%3A+null%2C+instID%3A+null+%7D%2C%0A++++%7B+str%3A+%27be+blocked+by%27%2C++classID%3A+null%2C+instID%3A+null%2C%0A+++++++++++++++++++++++++++++descr%3A+%27%3D%5C%27is+blocked+by%5C%27%2C+%3Dinverse+of+%5C%27blocks%5C%27+or+%5C%27blocking+activity%5C%27%27+%7D%2C%0A++++%7B+str%3A+%27antioxidant%27%2C++++classID%3A+null%2C+instID%3A+null+%7D%2C%0A++++%7B+str%3A+%27or%27%2C+++++++++++++classID%3A+null%2C+instID%3A+null+%7D%2C%0A++++%7B+str%3A+%27FLAP+Inhibitor%27%2C+classID%3A+null%2C+instID%3A+null+%7D%0A++%5D%2C%0A++conns%3A+%5B%0A++++%7B+type%3A+%27T%27%2C+pos%3A+%5B+-1%2C++0%2C+1+%5D+%7D%2C%0A++++%7B+type%3A+%27T%27%2C+pos%3A+%5B+-1%2C++3%2C+4+%5D+%7D%2C%0A++++%7B+type%3A+%27L%27%2C+pos%3A+%5B++2%2C++0%2C+3+%5D+%7D%2C%0A++++%7B+type%3A+%27T%27%2C+pos%3A+%5B++6%2C+-1%2C+5+%5D+%7D%2C%0A++++%7B+type%3A+%27L%27%2C+pos%3A+%5B++8%2C++7%2C+9+%5D+%7D%2C%0A++++%7B+type%3A+%27T%27%2C+pos%3A+%5B++2%2C++6%2C+8+%5D+%7D%0A++%5D%0A%7D) to see it as an interactive, editable VSM-sentence):
```javascript
{ terms: [
    { str: 'production of', classID: 'http://purl.obolibrary.org/obo/GO_1903409', style: 'i11-13', instID: null },
    { str: 'ROI', classID: 'http://purl.obolibrary.org/obo/CHEBI_26523', instID: null },
    { str: 'and', classID: null, instID: null },
    { str: 'activation of', classID: 'http://purl.obolibrary.org/obo/MI_2235', style: 'i10-13', instID: null },
    { str: 'NF-kappaB', classID: 'https://www.alliancegenome.org/gene/HGNC:7794', instID: null },
    { str: 'could', classID: null, instID: null },
    { str: 'be blocked by', classID: null, instID: null, descr: '=inverse of \'blocks\' or \'blocking activity\'' },
    { str: 'antioxidant', classID: null, instID: null },
    { str: 'or', classID: null, instID: null },
    { str: 'FLAP Inhibitor', classID: null, instID: null }
  ],
  conns: [
    { type: 'T', pos: [ -1, 0, 1 ] },
    { type: 'T', pos: [ -1, 3, 4 ] },
    { type: 'L', pos: [ 2, 0, 3 ] },
    { type: 'T', pos: [ 6, -1, 5 ] },
    { type: 'L', pos: [ 8, 7, 9 ] },
    { type: 'T', pos: [ 2, 6, 8 ] }
  ]
}
```

<br>

### Project option 2:&nbsp; UD –> VSM

We could also start from dependency structures in the [UD form](https://universaldependencies.org/introduction.html) (Universal Dependencies), and design rules to convert this to VSM.

For example the [Stanza](https://stanfordnlp.github.io/stanza) parser can produce UD [output](https://stanfordnlp.github.io/stanza/depparse.html#accessing-syntactic-dependency-information), also for biomedical and clinical text.  
This can be tested live on [stanza.run/bio](http://stanza.run/bio) : press Submit, and see the UD output and other useful information visualized at the bottom of the page.  
The Stanza UD output for the earlier example is:

<img src="img/ud.svg">


<br>

## This project is particularly looking for:

- People with diverse expertise in NLP – (as this project owner's expertise is with biocurators, semantic tech, etc).
- It would be great to **have discussions** about dependency types and semantics, and to come up with ideas for:
  - how to **map dependency relations onto VSM semantics**, structurally (i.e. VSM-connectors),
  - how to **map certain terms onto IDs**, where possible (e.g. relation IDs, and prepositions as relations),
  - which **parts of a sentence to select** for conversion (e.g. discard filler text),
  - how to **simplify some parts** (e.g. the structure "production-of &rarr; ROI" could become one GO-term like "ROS biosynthesis").


### Further ideas

Once we can translate NLP output to VSM, we can automatically convert the [VSM to RDF](https://github.com/vsm/vsm-to-rdf) (among others), and store it in a triplestore.

- Then we could discuss how to **represent SPARQL queries in VSM** form as well.  
Making it easier to **formulate semantic queries** like this, could give our biomedical experts a more independent power to wield semantic technologies against Covid-19. It would give them a practical tool to query deep semantic knowledge structures, extracted from literature.


### A necessary ambition

This project is quite ambitious and may eventually become the topic of an X-people-year project. Therefore we want to emphasize that our main goal – apart from some preliminary coding – is to **initiate discussions and intellectual cross-pollinations** towards achieving these goals.


### Q&amp;A

Questions &amp; answers and **further thoughts** are collected in GitHub [**Discussions**](https://github.com/vsm/nlp-to-vsm/discussions).
