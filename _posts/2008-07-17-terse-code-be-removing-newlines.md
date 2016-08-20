---
id: 1592
title: Terse code be removing newlines
date: 2008-07-17T23:01:12+00:00
author: Niklas
layout: post
guid: http://protocol7.com/?p=1592
permalink: /archives/2008/07/17/terse-code-be-removing-newlines/
categories:
  - Uncategorized
tags:
  - Java
  - scala
---
<div class='microid-62d01fa48b2fac01c2282e99966ce6aa4dae88d4'>
  <p>
    While I&#8217;m a big fan of Scala, and in general like to write more stuff in less code, I&#8217;ve seen a few cases of people showing examples of how terse the code gets once its in Scala (or Ruby or what ever) compared to Java. However, in many of those examples, the effect is solely due to using one liner code rather than those, actually readable constructs that code conventions has taught us to use. Not to pick <a href="http://www.gracelessfailures.com/2008/07/compacting-java-code-and-style.html">on this post</a> in particular (it does in fact mention that they are not satisfied with the result), but it does show my problem. Of course, that Java code could be written like this:
  </p>
  
  <pre><code>
        Vector&lt;string> v = new Vector&lt;/string>&lt;string>();
        for(String s : map.keySet()) if(s.startsWith(prefix) && !s.equals(prefix)) v.add(s);
        return v.size() > 0 ? v.toArray(new String[0]) : null;
&lt;/string></code></pre>
  
  <p>
    Is that generics beautiful? Not exactly. Do we have to do a lot of stuff the compile could do for us? Yeah. But I would argue that this code is as readable as the Scala code in the post.
  </p>
  
  <pre><code>
(for (val key &lt; - map.keys if key.startsWith(prefix) &#038;&#038; (key != prefix)) yield key).toList match {
    case Nil => null
    case list => list.toArray
}
</code></pre>
  
  <p>
    Which is to say, not a lot. And it&#8217;s not significantly more verbose. Now, as <a href="http://www.gracelessfailures.com/2008/07/compacting-java-code-and-style.html?showComment=1216274160000#c2987683146900549428">the comment on the post show</a>, there are better ways of doing this which really does make Scala shine. That&#8217;s the examples we need.
  </p>
</div>