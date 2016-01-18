---
layout: post
title:  "Leveraging opensource and existing infrastructure to do opendata seamlessly"
date:   2016-01-17 21:36:00
categories: blog
---

Opendata initiatives are becoming the norm for all government agencies worldwide.  Major cities are selecting datasets to help foster innovation and create new markets. As Tim Berners-Lee said:

> Data is a precious thing and will last longer than the systems themselves.

Accessibility is a real concern here, so we should not expose proprietary/internal formats to the masses. We want our data to be used, crunched, mashed-up and more !

So to get that data out quickly, we could:

1. ask our in-house developers to program extensions to proprietary software
2. buy ETL tools and schedule scripts, workbenches, etc.
3. leverage opensource tools and our existing infrastructure to liberate any data as a service.

They are all good and bad depending on your situation and what your agenda is.

Extensions to proprietary software
----------------------------------
Any in-house code out of your main expertise or market differentiator is a [liability](http://www.jamesshore.com/Blog/An-Approximate-Measure-of-Technical-Debt.html). Think twice before implementing some nice add-on to a proprietary software.  Usually, what you seek to achieve is already done and available (to buy). Since the purpose is to free data, I find it particularly funny to spend time or dimes here.  After all, some form of import/export functionality should be present in all major software, sometimes with limited functionality, but usually, it's enough to free your data at close to no cost.

ETL tools
---------
If you don't have programmers, creating extensions was out of the question, so you looked at the market to see what it had to offer. Most ETL tools are simple to use and you can click-program your way to success.  But beware, going that route is a tedious process: linking schemas, columns, conditions, are usually done one entity at a time. You have hundreds of entity to distribute. It does not scale well. It is error prone and more often than not, it is also nearly impossible to discover what really changed between 2 versions of an ETL script (if you use SCM softwares like *git* or *svn* and I hope you do).

Leveraging opensource and existing infrastructure
-------------------------------------------------



*[ETL]: Extract, Transform, Load
*[Tim Berners-Lee]: Inventor of the World-Wide-Web
*[SCM]: Source Configuration Management
