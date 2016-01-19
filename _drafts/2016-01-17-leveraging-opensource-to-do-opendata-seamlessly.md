---
layout: post
title:  "Leveraging opensource and existing infrastructure to do opendata seamlessly"
date:   2016-01-17 21:36:00
categories: blog
---

Opendata initiatives are becoming the norm for all government agencies worldwide.
Major cities are offering datasets to help foster innovation, create new markets.

As Tim Berners-Lee said:

> Data is a precious thing and will last longer than the systems themselves.

Accessibility is a real concern here: We want our data to be used, crunched, mashed-up and more,
so we should not expose proprietary/internal formats to the public.

To get data out quickly, we could:

1. ask our in-house developers to program extensions to proprietary software
2. buy ETL tools and schedule scripts, workbenches, etc.
3. leverage opensource tools and existing infrastructure to liberate any data as a service.

They are all good or bad depending on your situation and what your agenda is.  I'm a proponent of
*anything as a service*, so the third option is the most appropriate for my use cases.

What you should note before choosing a path to your success
-----------------------------------------------------------
Any in-house source code out of your main expertise or market differentiator is a
[liability](http://www.jamesshore.com/Blog/An-Approximate-Measure-of-Technical-Debt.html).
Think twice before implementing some nice add-on to a proprietary software.  Usually, what you seek
to achieve has already been done and is available (to buy). Since the purpose is to free data,
I find it particularly funny to spend time or dimes here.  After all, some form of import/export
functionality should be present in all "good" software. Even with limited functionality,
it is usually enough to free your data at close to no cost.

Most ETL tools are dead simple to use and you can click-program your way to success.
But beware: going that route is still a tedious process.  All steps (linking schemas, columns, conditions,
transformations) are usually done one entity at a time in a GUI. You may have hundreds of entity to distribute.
It does not scale. It is error prone and more often than not, it is also nearly impossible to discover what
really changed between 2 versions of an ETL model (if you use SCM softwares like *git* or *svn*).

Leveraging opensource and existing infrastructure
-------------------------------------------------



*[ETL]: Extract, Transform, Load
*[Tim Berners-Lee]: Inventor of the World-Wide-Web
*[SCM]: Source Configuration Management
