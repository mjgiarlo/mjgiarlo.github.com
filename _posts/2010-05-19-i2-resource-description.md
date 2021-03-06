---

title: "I2: Resource Description"
wordpress_id: 568
wordpress_url: https://mike.giarlo.name/blog/?p=568
date: 2010-05-19 09:38:18 -04:00
---
I can hardly believe it's been eight months since I last wrote about the <a href="https://mike.giarlo.name/blog/category/projects/niso-i2/">NISO I2</a> project.  A lot has changed since then[^1].  I continue to work on I2 however; they won't get rid of me that easily.

In the <a href="https://mike.giarlo.name/blog/2009/09/15/i2-survey-results/">last post</a>, I wrote:<blockquote>The next step is to build upon the report to draw yet more conclusions from the data â€” there's an awful lot there â€” and flesh out some repository use cases for institutional identifiers. The I2 core group is moving quickly towards finalizing identifier metadata elements so that a standard may be drafted, and I think having some use cases documented will help drive the standard in a direction the community can get behind.</blockquote> Since that time, the three scenario groups -- Electronic Resources; Institutional Repositories and Learning Management Systems; and Library Resource Management -- have concluded their work.  The work of the scenario groups included surveys of over 300 people working in these fields.  The survey results have been analyzed and reports were posted on the NISO website.  These reports have been used to flesh out use cases for an institutional identifier.  Upon completion of this work, the scenario groups were disbanded and work continued in a broader I2 working group.

The I2 working group has concentrated its work on analysis of similar standards and, as I alluded to earlier, significant effort has gone into defining core metadata to identify institutions, such as institution name, institution type, location information, variant identifiers, domain name(s), URL(s), and (optionally-typed) relationships to other institutions.  During these discussions it was difficult for me to hear the issues and needs around I2's metadata and identifiers without <a href="https://mike.giarlo.name/blog/2009/06/13/i2-strawman/">linked data springing to mind</a>.

While we are designing a standard and not a system or a service <em>per se</em>, it seems useful to include in the standard an informative section about implementation and architecture[^2]; I find that reading standards is much easier on the brain when you get not only the standard itself but some examples of implementation, and that will be true as well, one hopes, of I2 standard implementers.  To that end, the group will be producing an XML schema of the I2 metadata elements and also an RDF schema.

I have been working on the RDF for I2 on and off for the past month or two.  Below are my impressions, as someone who is new to modeling in RDF, and the procedures I used to produce the draft RDF schema.
<!--more-->
Despite their names, RDF schema and XML schema are quite different[^3].  The XML schema is a tool for validating an XML-based document or record, and it's a common tool for modeling metadata in libraryland.  Not so with RDF schema, where the notion of document or record is replaced by the notion of a set of triples.  The focus in RDF is on the triple not on the document, and so validation of documents or records is not the point of RDF schema.  This took some effort to wrap my mind around.

Before I modeled I2 in RDF, I sketched out a domain model of I2 by copying relevant bits of information from I2 documents and pasting them into a text editor.  Then I put them into classes.  In I2's case, the domain model contained three classes of things: metadata elements about an institution, relationships between institutions, and types of institution.

I gathered some examples of relatively simple RDF schemas and transformed them into the <a href="http://www.w3.org/TeamSubmission/turtle/">Turtle</a> serialization format[^4] for ease of reading, using them as a template for the I2 schema.

In the <a href="http://www.w3.org/TR/rdf-schema/">RDF schema (RDFS)</a> specification, there are two classes of things in the domain model: classes and properties.  If you are familiar with object-oriented programming, chances are you already grok this way of modeling, but otherwise, generally: a class is like a type and a property is an attribute.  If I were to model myself in RDF schema, then, I might say I am in the class of human beings, and one of my many properties is having a particular birth date, and another is having been born in a particular city.  The next step was to take the I2 domain model (metadata elements about an institution, relationships between institutions, and types of institution) and decide whether each thing was a class or a property.  I decided that the former two were sets of properties and that type of institution could be modeled as a set of classes.

Having a conceptual model of I2 and how it fit into the RDF schema way of thinking about things, I wrote a simple ontology defining one RDFS class per type of institution, and one RDFS property per metadata element and one per relationship type.  This would have sufficed as an ontology.

Exposing RDF-based resources on the web as linked data, however, represents an opportunity for metadata element-level interoperability at global scale.  In order to interoperate with the existing corpus of linked data available on the web, I went through the new I2 ontology and looked for areas where I could re-use, or subclass or otherwise link to, classes and properties already defined in more widely-used ontologies.  I realized at this point just how different coming up with a new XML document format was from writing an RDF ontology; whereas I might have wanted the former to be comprehensive and inclusive of every single aspect within the I2 domain model, my goal with the latter became to eliminate it (by trimming it down to only those bits which are not defined elsewhere).

Since the RDF ontology for I2 is not inclusive of the entire domain model, it seemed necessary to produce another reference document: a set of instances of I2 resources showing the mingling of new I2-specific classes and properties with well-defined classes and properties from other ontologies.

I shared rough first drafts of these documents and received very helpful feedback from some folks who are better-versed in this than myself.  I've now incorporated their feedback into the latest I2 ontology and instance document.  I hope to include both of these into a draft of the I2 specification which will go out for comment in the coming months.  Here's the latest <a href="http://gist.github.com/358857">ontology</a> and the latest <a href="http://gist.github.com/358858">set of instances</a>.

[^1]: I've moved and <a href="https://mike.giarlo.name/blog/2009/12/22/forking/">changed jobs</a>, in fact
[^2]: This practice seems more or less common in my (admittedly limited) experience, cf. <a href="http://unapi.info/specs/">the unAPI specification</a>.
[^3]: This reflection should come as little surprise since RDF and XML are different kinds of things: RDF is a data model and XML is a serialization format.
[^4]: Using <a href="http://librdf.org/raptor/rapper.html">rapper</a>, a nifty little tool.
