---
layout: post
title: Do legends still matter for today's on-line maps?
---
// On the role of legends in today's web map applications.

Are legends first class citizens in today's on-line mapping applications?
My opinion is no, they are not. If this is always a bad thing is open to discussion.

At university I studied Geography. Printed maps, especially topographic maps, were my bread and butter in those days, long before GIS tools and programming. A topographic map usually comes with everything needed for its correct interpretation: legend, projection, datum, scale, survey year, accuracy, sources and more. When out in the field, with the correct experience, one relies on those textual elements for understanding everything about the map. It is clear how this design originated in a pre globally connected world: the map had to its job and be autonomous, self sufficient.

As an example of how rich these explanatory elements can be, have a look at [this USGS map](http://upload.wikimedia.org/wikipedia/commons/c/c7/Mount_Marcy_New_York_USGS_topo_map_1979.JPG) and at [this excerpt](http://www.dic.unipi.it/s.lombardo/materiali%20I%20eser/Legenda_25k.jpg) from an Italian IGM map.

I grew to love the rich legends and all the other explanatory elements on a topographic map. Biased from this first encounter, afterwards I tended to value maps by the presence or absence of these elements. For example, I started to look with suspicion upon thematic maps that did not give any indication of the underlying projection, even if this was not relevant to understand the message. Let's face it, thematic maps serve a different purpose and are usually more essential, more focused and more specific than topographic maps. Sometimes too much information can be distracting, nevertheless, due to my background, I like the approach where a map and all its elements are explained and the interpretation is not left to guess and convention.

Few years after university I remember the words of a very competent GIS professional I used to work for: "The ideal Web GIS map is without a legend". What he meant is that a Web map should be simple, intuitive, immediately understandable. One flies on the Web and you should not expect people to waste time in map projection information or in making sense of obscure map symbols. My first reaction to this position, unsurprisingly, was to disagree, but nowadays I do admit he had some good points.

Today's mainstream map applications somehow prove his point. Legends and other map textual elements are not very present on the Web. Screen space and user attention are indeed limited resources and designing good, compelling legends for interactive maps is not an easy task. Google maps is a good example. It does equip you with a minimal legend for its thematic layers but nothing more. Even the fact that the used projection is a variant of Mercator is something you would not normally know unless you are a google maps developer. But again, this is not necessarily a bad choice, rather a pragmatic one.

To create a minimal, non comprehensive, legend is not a bad thing to do, in absolute terms. A good Web design is often about compromise. Instead, to completely forget about a legend or not to give enough though about it in the design process is bad. And in my experience of Web Developer I saw this happening again and again.