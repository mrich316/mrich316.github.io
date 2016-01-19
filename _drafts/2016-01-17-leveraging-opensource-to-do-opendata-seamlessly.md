---
layout: post
title:  "Leveraging open-source to do open-data seamlessly"
date:   2016-01-17 21:36:00
categories: blog
---

Open-data initiatives are becoming the norm for all government agencies worldwide.
Major cities are offering datasets to help foster innovation, create new markets,
increasing transparency and citizen engagement.

> Data is a precious thing and will last longer than the systems themselves.
>
> --Tim Berners-Lee

Accessibility is a real concern here: We want our data to be used, crunched and mashed-up in ways
never imagined by our marketing dept. For this to happen at large scale, we must not expose
proprietary/internal formats to the public.

To get data out quickly, we can:

- ask our in-house developers to create extensions in proprietary software (to export data)
- deploy free (or buy) ETL tools and schedule scripts, workbenches, etc.
- create a [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) api to liberate any data as a service using open-source tools.

All solutions are good. It all depends on what your agenda is and where you want to go.
I'm a proponent of *anything as a service*, so the third option is the most appropriate
for my use cases.

Things to consider before choosing a solution
---------------------------------------------
Any in-house source code out of your main expertise or market differentiator is a
[liability](http://www.jamesshore.com/Blog/An-Approximate-Measure-of-Technical-Debt.html).
Think twice before implementing some nice add-on to a proprietary software.  Usually, what you seek
to achieve has already been done and is available (to buy). Since the purpose is to free data,
I find it particularly funny to spend time and dimes here.  After all, some form of import/export
functionality should be present in all "good" software. Even with limited functionality,
it is usually enough to free your data at close to no cost, albeit, in a single format like CSV.

Most ETL tools are dead simple to use and you can click-program your way to success.
But beware: going that route is still a tedious process.  All steps (linking schemas, columns, conditions,
transformations) are usually done one entity at a time through a GUI. You may have hundreds of entity to distribute.
It does not scale. It is error prone, difficult to unit test and more often than not, it is nearly
impossible to discover what really changed between 2 versions of an ETL model (if you are using SCM software
like *git* or *svn*).

Open-source can become legacy just like regular software.  The web evolves faster than the government.
Resist the temptation to mix and match many open-source projects to liberate your data if they are not
backed by respected individuals.

With that in mind, I chose to explicitly declare a contract that I "own" to hide implementation details
like the software used to have a solution that can resist the ages of time and be used almost everywhere.

In a next post, I'll show how we can encapsulate [GDAL ogr2ogr](http://www.gdal.org/ogr2ogr.html) in a
rest api coded in C# [ASP.NET Web API](http://www.asp.net/web-api).  As readers may have found out, similar
[solutions](http://ogre.adc4gis.com/) can already be found on the net.  I chose to explicitly declare a contract that I "own" to hide implementation details and protect the API from "forced" evolution (like vendor upgrades containing [breaking changes](https://en.wiktionary.org/wiki/breaking_change)).

*[ETL]: Extract, Transform, Load
*[CSV]: Comma Separated Values
*[Tim Berners-Lee]: Inventor of the World-Wide-Web
*[SCM]: Source Configuration Management
*[REST]: REpresentational State Transfer
