.. _how_to_read.rst:

******************************
How to read this documentation
******************************

This document explains everything you need to know to understand the rest of the documentation as well as its general structure and the phrases used throughout it. While we tried our very best to make the documentation as clear and concise as possible, you may encounter a few rough edges here and there or things that aren't entirely clear. If you do so, please tell us about them so that we can update the offending parts.

General structure
=================

When reading a class reference, you will often encounter an overview block at the beginning, which you are encouraged to read as it usually explains the general use of the class, as well as various other useful information that you should know before working with the class. Individual method references will assume that you've read these overviews and not repeat information already present there.

.. note:: 
	Sometimes references include additional information in the form of various info boxes, like this one. You should read the information presented in there to get additional insight or warnings about the documented topic. Sometimes you will also find "See Also" links, which you are encouraged to look at as well, since they contain additional documentation about the topic.
.. seealso:: :doc:`naming`


Terms & Notions
===============

While reading this documentation, you will find various terms and notions used to describe various things. These terms can be ambiguous and up to interpretation much like the previous sentence, which is why they are listed here along with their intended interpretation.

* **Receiver** The receiver always refers to the `this` pointer. Eg, if a method is documented as "Does X to the receiver", it means that X will happen to the object the method was invoked on.
* **Must not** Don't do what you were told not to. If things break because you did something you were explicitly told not to, it's your fault.
* **Must** The opposite of must not; These are things you must do in order to not break things.
* **Strongly encouraged** If the documentation strongly encourages you to do something, you should have a really good reason and knowledge of what you are doing in order to not do it. Usually this wording is used when various things depend on the thing you are doing. 
* **Strongly discouraged** These are the things that you should not do unless you are well aware of what it is you are actually doing and what kind of effect it has.
* **Encouraged** These are things that you should do, for instance because it allows Rayne to perform certain actions faster, but you won't break things if you don't do them. Still, you should have good reasons to not do these things, as they usually result in better performance.
* **Discouraged** The opposite of encouraged; Try to avoid doing these things.
