## 2018 Week 35

### One world, one web, one team

In the absence of [Dan](https://twitter.com/dasbarrett) (and his [yo-yo](https://ukparliament.github.io/weeknotes.data-search/2018/34/#get-yer-yo-yos-out)) [Matthieu took on data strategy duties](https://twitter.com/cognithive/status/1035152530358067200). An open session was run. Models and measurement were discussed.

[Alison](https://twitter.com/oliala), [Samu](https://twitter.com/langsamu), [Matt](https://twitter.com/mattrayner) and [Jamie](https://twitter.com/oddtype) (and assorted other computational experts) reviewed the initial work on the Committee Information System API. It's being built by our colleagues in the Business Systems Development team with the Data Service (and therefore the new website) being the main client. It's all part of a major refresh of end-to-end Committees digital stuff planned for delivery in early 2019. The computational experts had some thoughts and suggestions about the underlying model, the technical implementation of the API and how we might collaborate. Jamie's planning to catch up with Head of Business Systems, Matt Stutely next week to turn thoughts into plans.

Alison grabbed Samu and Jamie to talk about the modelling work for [Visiting](https://www.parliament.uk/visit/). Parliament puts on lots of events that the public can book and attend but these are managed by an array of departments and systems. One of the main systems is due to be refreshed, so we're looking at how we can improve and unify the online experience for people wanting to visit [our palace](https://en.wikipedia.org/wiki/Palace_of_Westminster). They came up with a few options that acknowledged the various systems and the existing administration workflows. The conclusion, at least for now, is to continue aggregating and refining the information on current events in the context of the models. Which, roughly translated, means make a really nice spreadsheet. With a view to this information evolving into a new data source.

Martin Casey, the Business Partner for [Strategic Estates](https://www.parliament.uk/mps-lords-and-offices/offices/commons/teams/#jump-link-7), got in touch with our Liz to chat dashboards. They've been working with an external consultancy to design one and now want to bring it in house. The source data is from the internal training system and [Microsoft Project](https://en.wikipedia.org/wiki/Microsoft_Project). So far it's all been built on spreadsheets. Liz thinks it should be possible to change the source but that depends on whether we can get access to the file. She explained that they could build their own dashboard with support from the [Parliamentary Computational Section](https://pds.blog.parliament.uk/) but that access to the the training system will be the limiting factor. We haven't yet seen the reporting data available but we seem to think we can't connect directly. It does look like there's a content pack for Microsoft Project and if they move online we should be able to query via [OData](https://www.odata.org/).

We're told that the back and front end teams released a new [search](https://beta.parliament.uk/search) architecture today. Or that that's happening right now. As I type. So far Slack is not exploding so we can only assume it's going well.

### Domain modelling

We entered our second week without a working copy of [LODE](http://www.essepuntato.it/lode). Which means we're still unable to generate HTML to match our [turtle](https://en.wikipedia.org/wiki/Turtle_(syntax)) files. [Published models](https://ukparliament.github.io/ontologies/) remain unchanged. At least in HTML form. Elsewhere Robert is attempting to write a turtle parser to fix this problem. Which would be splendid.

[Anya](https://twitter.com/bitten_), Jayne, [James](https://twitter.com/thevinternet), [Silver](https://twitter.com/silveroliver) and [Michael](https://twitter.com/fantasticlife) got together to chat about potential improvements to the [procedure model](https://ukparliament.github.io/ontologies/procedure/procedure-ontology.html). It was all very early on bank holiday Tuesday but brains fed on nicotine and caffeine ground sluggishly into gear. Three things got covered:

* Given we only have dates for [business items](https://ukparliament.github.io/ontologies/procedure/procedure-ontology.html#d4e193) and given that multiple business items can and do happen on the same day, ordering them on [work package](https://ukparliament.github.io/ontologies/procedure/procedure-ontology.html#d4e284) pages can be tricky. So far we've tried ordering by distance from the starting [step](https://ukparliament.github.io/ontologies/procedure/procedure-ontology.html#d4e272) in the procedural graph but there are often many paths to the same thing. And paths through the House of Lords tend to involve more steps than those through the House of Commons. We had wondered if introducing a level of inheritance across steps would help solve this by bridging between similar steps in different Houses. So an 'approval motion tabled' step would have 'approval motion tabled in House of Commons' and 'approval motion tabled in House of Lords' as child steps. Which would at least help with some sense of symmetry. But we're not yet sure if the step ordering on work package pages takes into account requires routes. If it does we may be able to add more requires routes to help order things. And if that fails, possibly add step inheritance.

* To differentiate between things that could happen only once (e.g. an [EVEL](https://en.wikipedia.org/wiki/English_votes_for_English_laws) decision) and things that could happen multiple times in parallel (e.g. the tabling of non-fatal approval motion amendments) we introduced the concept of self-preclusion. A step would be related to itself by a precludes route if it could only be [actualised](https://ukparliament.github.io/ontologies/procedure/procedure-ontology.html#d4e22) once. Which meant, having happened, that step would no longer show up in the space of future possibilities. But some things like debate scheduling can happen many times in series but only if you cycle through a debate not reached step. You can't make debate scheduled self-precluding if it can happen again but if you don't make it self-precluding it will always show up on the list of possible future things. The only way we can think this might be made to work would mean introducing route level [logic gates](https://en.wikipedia.org/wiki/Logic_gate). But even then we're not quite sure what that would look like. And it would complicate things enormously. And it's not strictly untrue to say that a debate having been scheduled, one possible future event is for the debate to scheduled. So for now we've decided to leave well alone. Cos it's hard and, at least for now, not too much breaks.

* We don't currently have a mechanism for matching the results of [tabling](https://ukparliament.github.io/ontologies/tabling/tabling-ontology.html#d4e231) motions and motion amendments to any withdrawal of those motions and motion amendments. At least solely within procedural data. So multiple Members might table non-fatal amendments to an approval motion and all of those will be debated and decided upon. But if one motion amendment is withdrawn we're currently saying that debates and decisions are precluded. Which isn't true if one or more non-fatal amendments are still tabled. So we need to remove the precludes arrows between amendment withdrawal and decisions. And take into account business data when calculating any future possibility space.

Which is all a lot of words to describe not much action. Much like the meeting then.

Most of the rest of Anya, Silver and Michael's day involved sitting around with Robert practicing a [talk we're due to give at KetIKX in September](http://www.netikx.org/content/ontologies-and-domain-modelling-fun-honest-and-friendly-introduction-20-september-2018). Michael attempted to run though a workshop thing but Robert decided workshopping Michael was more fun than idle participation. Tough crowd this.

Anya, Silver and Michael spent Thursday with [David Beamish](https://en.wikipedia.org/wiki/David_Beamish), idiot checking some of their recent models and dipping into timetabling and [order papers](https://en.wikipedia.org/wiki/Order_Paper). They ran through the procedure model, associated [statutory instrument](https://en.wikipedia.org/wiki/Statutory_instrument_(UK)) [flowcharts](https://ukparliament.github.io/ontologies/procedure/procedure-ontology.html#examples), the [legislation model](https://ukparliament.github.io/ontologies/legislation/legislation-ontology.html), [laying](https://ukparliament.github.io/ontologies/laying/laying-ontology.html) and [tabling](https://ukparliament.github.io/ontologies/tabling/tabling-ontology.html). A few small improvements were suggested and found their usual home on [Trello](https://trello.com/b/Z1nrm0Vr/parliament-ontology). More meetings with [Table Office types to talk timetabling are planned.

Librarian Jayne and our [Alex](https://twitter.com/alexedwardh) spent a delightful couple of hours staring at flowcharts for [draft negative](https://github.com/ukparliament/ontologies/blob/master/procedure/sis/draft-negative.pdf) and [made negative](https://github.com/ukparliament/ontologies/blob/master/procedure/sis/made-negative.pdf) SIs and comparing against [the data](https://procedures.azurewebsites.net/) we've entered. Jayne developed an appreciation for why Michael may have dozed whilst doing the same exercise last week. It is very tiring work. Luckily librarian Emma arrived bearing fudge so sugar carried them through. We're told they talked about dogs but it's not clear from Slack if they like dogs. Or hate them.

### Corporate data

"The car is on fire, and there's no driver at the wheel](https://www.youtube.com/watch?v=XVekJTmtwqM)"

But that was last week. This week Lew's been doing some [BizTalk](https://en.wikipedia.org/wiki/Microsoft_BizTalk_Server) maintenance, fiddling with performance improvements and setting up our test environments. Noel's been looking at outstanding tickets in our incident management system and checking if they're related to the fire.

### Customer service of the week award goes to...

...[librarian Jayne](https://www.youtube.com/watch?v=f3V-7DEAgdc). The nomination arrives from Alex who'd received a request from the [Knesset Archives](https://knesset.gov.il/archive/eng/ArchiveIntro_eng.htm) to provide session level Member activity counts for things like the number of [private bills](https://www.parliament.uk/about/how/laws/bills/private/) sponsored, the number of [written questions](https://www.parliament.uk/business/publications/written-questions-answers-statements/written-questions-answers/) tabled etc. Jayne kindly helped out. For which read did the actual work. Alex tells us *we* were able to provide everything requested out of [Solr](http://lucene.apache.org/solr/). Not all developers, man.

We're still stuck on the number of motions per member as this is a all bit tricky. But we continue to investigate. And feel sure Jayne will come up with the goods.

### Strolls

Not much in the way of strolls this week though Anya and Michael did manage to clock up 22 miles in 2 days. Sore feet resulted.

Anya, Silver and Michael took a short stroll down to Bellamy's, headquarters of the Parliamentary Pudding Section. An institution long famed for its commitment to quality steamed puddings and custard. The bread and butter pudding was slightly less than luke warm. The custard was slightly warmer but lumpy. Standards have slipped. You can certainly tell it's recess.

### Things that caught our eye

* [The Role of Visualisation in Data Analysis](https://www.youtube.com/watch?v=ZdPNBF6GWBw)

* [Shower With Your Dad Simulator 2015: Do You Still Shower With Your Dad on Steam](https://store.steampowered.com/app/359050/Shower_With_Your_Dad_Simulator_2015_Do_You_Still_Shower_With_Your_Dad/)

* [https://beta.layersoflondon.org/map/layers](https://beta.layersoflondon.org/map/layers)

* [Chicken Chicken Chicken: Chicken Chicken](https://isotropic.org/papers/chicken.pdf)