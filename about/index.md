---
layout: default
title: "The man, the beard, the mystery"
---

{% capture my_age %}{{ site.time | date: %Y | minus: 1980.44 }}{% endcapture %}

<img src="http://static.tonyarnold.com/photobooth.png" alt="Photo Booth shenanigans" align="right" />

# About Tony

Hi! I’m Tony Arnold, a {{ my_age | truncate: 2, '' }} year old chap from [Newcastle, Australia][NewcastleMapLink]. Professionally, I run a small business — [The CocoaBots][TCB] — building apps for Apple's Mac, iPhone and iPad devices.

If you’d like to get in contact with me, please feel free to [send me an e-mail][Email].

 [TCB]: http://thecocoabots.com/
 [Email]: mailto:Tony%20Arnold%20%3Ctony@tonyarnold.com%3E
 [NewcastleMapLink]: http://www.google.com/maps?f=q&source=s_q&hl=en&geocode=&q=Newcastle,+Australia&sll=-32.893409,151.735743&sspn=0.014324,0.016651&ie=UTF8&hq=&hnear=Newcastle+New+South+Wales,+Australia&t=h&z=15&iwloc=A
