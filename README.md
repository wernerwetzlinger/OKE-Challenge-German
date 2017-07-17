# Improving Language-Dependent Named Entity Detection 

This directory contains the dataset used for writing the paper "Improving Language-Dependent Named Entity Detection ", if you use this dataset for your experiments or mention the dataset in your study, please cite our paper using the following citation:

> Petz Gerald, Wetzlinger Werner and Nedbal Dietmar: Improving Language-Dependent Named Entity Detection. In Proceedings of the Cross Domain Conference for Machine Learning and Knowledge Extraction 2017 (CD-MAKE 2017) (pp. TBD). DOI: TBD


BibTex format:

	@inproceedings{TBD,
	      title={Improving Language-Dependent Named Entity Detection},
	      author={Petz Gerald, Wetzlinger Werner and Nedbal Dietmar},
	      booktitle={Proceedings of the Cross Domain Conference for Machine Learning and Knowledge Extraction 2017},
	      pages={85--94},
	      year={2017},
	      organization={TBD}
	}

## Motivation for building this dataset

It has been acknowledged that linguistically motivated and thus language aware spotting methods are more accurate than language independent methods. The German language has a lot of differences for example in the use of upper and/or lowercase, compound nouns or hyphens to concatenate nouns. However, improvements in a certain language usually come at the expense of ease of adaptation to new languages.

Established NER/NEL challenges and tasks of the scientific community like the OKE challenges, the NEEL challenge series, or the ERD challenges are in the English language and therefore language-dependent improvements are often not in the focus of the research.

Moreover, the results from different tools need to be comparable against certain quality measures based on the same dataset. Frameworks addressing the continuous evaluation of annotation tools such as GERBIL can be used for comparison, but evaluation datasets provided by GERBIL as “gold standards” are only available for the English language as well.

Thus we developed a dataset to test language-dependent Named Entity Detection.

We decided to build a dataset in the German language that is coded in NIF-format to able to use it in GERBIL. The content of the dataset should be comprised of natural language in encyclopedia entries or news (not tweets or queries), should include multiple documents with multiple spots, cover a wide range of topics and include co-references.

## How the dataset has been generated

We chose to develop a new German dataset based on the evaluation dataset of the OKE challenge 2016 (“OKE 2016 Task 1 evaluation dataset”) because it best fulfilled the above mentioned requirements.

To develop the new dataset based on the dataset, we conducted a multi-step approach that consisted of the following tasks:
1.	Identify all documents and included spots in the NIF file of the OKE 2016 Task 1 evaluation dataset.
2.	Translate all documents in this dataset using Google Translate (translate.google.com)
3.	Adjust the initial Google translation by improving German grammar, word order, etc. by native speakers.
4.	Identify all English spots of the initial dataset in the German translation.
5.	Identify the corresponding entities in the German knowledge base (de.wikipedia.org).
6.	Link the spots to the identified knowledge base entities using links in a HTML file.
7.	Transform the HTML file to NIF using a converter.


## Content

We additionally created a second version of the dataset that includes no coreferences.

### oke2016 - evaluation dataset - german - with coref

This file contains the result of the above mentioned process. Due to the focus of our work, this dataset does not include types. Consequently in contrast to the original OKE 2016 dataset, entities in this dataset do not have assigned types (person, place, organization, role).

The following example illustrates the translation:

Original sentence in OKE 2016 Task 1 evaluation dataset (bold words are part of spots): 
> From 1976 to 1980 **Brown** was employed as a **lecturer** in politics at **Glasgow College of Technology**. **He** also worked as a **tutor** for the **Open University**.

Translation in the developed German version:
> Von 1976 bis 1980 war **Brown** als **Dozent** für Politik am **Glasgow College of Technology** tätig. Er arbeitete auch als **Tutor** für die **Open University**.

The sentence and the spots of this translated sentence are represented in NIF the following way:

```
<http://demo.org/document41#char=0,143>
a nif:RFC5147String , nif:String , nif:Context ;
nif:beginIndex "0"^^xsd:nonNegativeInteger ;
nif:endIndex "143"^^xsd:nonNegativeInteger ;
nif:isString "Von 1976 bis 1980 war Brown als Dozent für Politik am Glasgow College of Technology tätig. Er arbeitete auch als Tutor für die Open University."^^xsd:string .


<http://demo.org/document41#char=22,27>
a nif:RFC5147String , nif:String , nif:Phrase ;
nif:anchorOf "Brown"^^xsd:string ;
nif:beginIndex "22"^^xsd:nonNegativeInteger ;
nif:endIndex "27"^^xsd:nonNegativeInteger ;
nif:referenceContext <http://demo.org/document41#char=0,143> ;
itsrdf:taIdentRef <https://de.wikipedia.org/wiki/Gordon_Brown> .


<http://demo.org/document41#char=32,38>
a nif:RFC5147String , nif:String , nif:Phrase ;
nif:anchorOf "Dozent"^^xsd:string ;
nif:beginIndex "32"^^xsd:nonNegativeInteger ;
nif:endIndex "38"^^xsd:nonNegativeInteger ;
nif:referenceContext <http://demo.org/document41#char=0,143> ;
itsrdf:taIdentRef <https://de.wikipedia.org/wiki/Dozent> .

<http://demo.org/document41#char=54,83>
a nif:RFC5147String , nif:String , nif:Phrase ;
nif:anchorOf "Glasgow College of Technology"^^xsd:string ;
nif:beginIndex "54"^^xsd:nonNegativeInteger ;
nif:endIndex "83"^^xsd:nonNegativeInteger ;
nif:referenceContext <http://demo.org/document41#char=0,143> ;
itsrdf:taIdentRef <https://de.wikipedia.org/wiki/Glasgow_Caledonian_University> .

<http://demo.org/document41#char=91,93>
a nif:RFC5147String , nif:String , nif:Phrase ;
nif:anchorOf "Er"^^xsd:string ;
nif:beginIndex "91"^^xsd:nonNegativeInteger ;
nif:endIndex "93"^^xsd:nonNegativeInteger ;
nif:referenceContext <http://demo.org/document41#char=0,143> ;
itsrdf:taIdentRef <https://de.wikipedia.org/wiki/Gordon_Brown> .

<http://demo.org/document41#char=113,118>
a nif:RFC5147String , nif:String , nif:Phrase ;
nif:anchorOf "Tutor"^^xsd:string ;
nif:beginIndex "113"^^xsd:nonNegativeInteger ;
nif:endIndex "118"^^xsd:nonNegativeInteger ;
nif:referenceContext <http://demo.org/document41#char=0,143> ;
itsrdf:taIdentRef <https://de.wikipedia.org/wiki/Tutor> .

<http://demo.org/document41#char=127,142>
a nif:RFC5147String , nif:String , nif:Phrase ;
nif:anchorOf "Open University"^^xsd:string ;
nif:beginIndex "127"^^xsd:nonNegativeInteger ;
nif:endIndex "142"^^xsd:nonNegativeInteger ;
nif:referenceContext <http://demo.org/document41#char=0,143> ;
itsrdf:taIdentRef <https://de.wikipedia.org/wiki/The_Open_University> .
```

### oke2016 - evaluation dataset - german - without coref

This file has exactly the same content and structure as the file “oke2016 - evaluation dataset - german - with coref”, except that all coreferences are deleted.

Consequently, in the developed German version of the above mentioned sentence there is one spot less (“Er”):
> Von 1976 bis 1980 war **Brown** als **Dozent** für Politik am **Glasgow College of Technology** tätig. Er arbeitete auch als **Tutor** für die **Open University**.



## Original (English) OKE2016 Challenge dataset

The original (English) OKE2016 Challenge dataset can be found [here](https://github.com/anuzzolese/oke-challenge-2016).
