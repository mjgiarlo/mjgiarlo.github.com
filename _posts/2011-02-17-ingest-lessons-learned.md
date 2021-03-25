---
title: "Ingest: Lessons learned"
date: 2011-02-17 05:13:51 -07:00
---
Now that we have a by-no-means-complete-but-still-useful [list of common barriers to ingest](https://mike.giarlo.name/blog/2011/02/ingest-is-a-barrier-to-ingest/), I thought I'd share the lessons learned.  We hope to apply these lessons in building [CAPS](https://github.com/DanCoughlin/caps), our prototype curation services platform.

* **Create a namespace, or namespaces, for identifiers that far exceeds foreseeable needs** -- Our first namespace can accommodate 7,072,810,000 identifiers.  We're using the [Archival Resource Key specification](https://wiki.ucop.edu/display/Curation/ARK) for identifiers (each of which will be mapped to HTTP URIs), and the Python-based [arkpy](http://github.com/mjgiarlo/arkpy) library for minting.
*   **Decouple the ingest process from the publication process** -- We plan to build a small suite of applications and tools upon our curation services platform, the first of which is for what we've been unimaginatively calling "generic ingest & management."  The application is for authenticated, authorized users only -- it's a tool for curatorial operations not for end-user display.  The ingest application will never automatically publish objects and it makes the assumption that all objects are private to the curator until the curator decides otherwise.
*   **Plan for scale and test performance from the outset** -- The current phase of development on CAPS was given a very ambitious deadline so we have not had the time to focus on performance and scale as much as we would have liked.  We have a list of areas to address in the next phase, however, and a laundry list of technologies to vet and test for our scaling needs.  We've also lined up a small team of folks to help out with system testing & QA.
*   **Make metadata input optional** -- We believe that curators, not systems, curate, and thus allow them to decide how richly objects ought to be described.  We intend to provide curators with tools that allow (and perhaps encourage) rich metadata to be attached to objects but as far as the "generic" ingest application (and the curation services platform underneath) is concerned, all elements in the data dictionary are repeatable and none are required.  We will be building similar "profiled" ingest applications for specific purposes in the near future, such as an ingest application for electronic business records, which will, however, be more stringent about metadata (and also about file formats, which the generic ingest app couldn't care less about).
*   **Allow stakeholders to drive decisions and, above all, communicate with users** -- This may be a meta-lesson, and it feels like the most important of them all.  Our development team for CAPS consists of our lead developer, a digital curator, an archivist, a metadata librarian, a project manager, and an architect.  Our project team is made up of our development team plus stakeholders from across the University Libraries including representation from our Digitization & Preservation department, the Arts & Architecture library, and University Archives.  Our project team meets for one hour a week -- a Herculean task to find a mutually convenient slot, let me tell you -- and our development team meets for fifteen minutes every morning.  The point here is that our stakeholders -- the primary eventual users of the ingest application -- are invested in the project, and they get a chance to see, criticize, and drive what we've developed every week as it evolves. Because we're in the same room so often, we get to communicate certain points regularly, e.g., what you ingest is only as permanent as you wish; identifiers are not precious at all; the curation platform is there for you to use in ways useful to you, so the typical "don't put that into the repo yet" mindset doesn't apply; your stuff is as findable as the richness of your metadata, but we can provide other ways to find your stuff (full-text search, etc.); and so forth.