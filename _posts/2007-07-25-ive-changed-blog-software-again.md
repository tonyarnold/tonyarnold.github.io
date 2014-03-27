---
layout: post
title: I’ve changed blog software again
tags:
  - Programming
  - Web
date: 25 July 2007 16:41:00
---

In what appears to be a biannual ‘thing’ for me over the last few years, I’ve thrown out my old blog software and replaced it with something that suits my needs and skills better. I’m now running [Symphony][1], by [21 Degrees][2], which is:

1.  **Not a Rails app (it’s PHP)**. Whilst not entirely happy with this (as I am a huge advocate of the “Rails Way™”), both Typo and Mephisto were generally a little unreliable for me over my time using them. There’s also the fact that neither are receiving serious attention anymore - and let’s be honest, everyone loves new features once in a while;
2.  **[Symphony][1] is run entirely off a combination of XML and XSLTs**. If you’ve not worked with this combination for web sites before, you’re missing out. XSLT is the language god would present his structured data with;
3.  **It’s faster**. No idea why, but my Rails sites on Dreamhost always ran slowly.
4.  **It’s more configurable** - check out the “Projects” section of my site - that’s all generated using a custom page type I set-up once and forget about.
5.  I like shiny things. **Obey my blog** - and its shiny updated design.
6.  **The search pages currently suck**. I’m working on them.
7.  **My RSS feed has moved**, and I haven’t rewritten the old URL yet (I’ll get to it).

#### Code splurge

Here’s some naff XSL I wrote (with some assistance from [members and their examples at Overture][4]) to scan through my XML structure and append the location of the installed [Symphony][1] application to the front of all absolute URLs. This means I can move my blog where-ever I like, and all of my links within pages will continue working. It’s also a good example of advanced XSL usage.

{% highlight xslt %}
<xsl:template match="p | ul | ol | li | h1 | h2 | h3 | h4 | h5 | h6 | blockquote | em | strong | code | pre | acronym | span">
    <xsl:element name="{name(.)}">
        <xsl:apply-templates select="@*"/>
        <xsl:apply-templates/>
    </xsl:element>
</xsl:template>

<xsl:template match="a | img">
  <xsl:element name="{name(.)}">
    <xsl:apply-templates select="@*"/>
    <xsl:if test="substring(@src,1,1)='/'">
      <xsl:attribute name="src"><xsl:value-of select="$root"/><xsl:value-of select="@src"/></xsl:attribute>
    </xsl:if>
    <xsl:if test="substring(@href,1,1)='/'">
      <xsl:attribute name="href"><xsl:value-of select="$root"/><xsl:value-of select="@href"/></xsl:attribute>
    </xsl:if>
    <xsl:apply-templates/>
  </xsl:element>
</xsl:template>

<xsl:template match="@*">
    <xsl:attribute name="{name(.)}"><xsl:value-of select="."/></xsl:attribute>
</xsl:template>

<xsl:template match="text()">
    <xsl:value-of select="."/>
</xsl:template>
{% endhighlight %}


 [1]: http://symphony21.com/
 [2]: http://21degrees.com.au/
 [4]: http://overture21.com/forum/comments.php?DiscussionID=1352
