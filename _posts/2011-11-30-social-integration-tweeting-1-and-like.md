---
layout: post
title: Social Integration Tweeting, +1 and Like

tags: Facebook,Google,Google Plus,Integration,Internet,Like,Plus,Programming,Twitter,Website
---
<p>You may have noticed that there are several websites now that included integration with social networking websites such as <a href="http://facebook.com">Facebook</a>, <a href="http://plus.google.com">Google Plus</a> and <a href="http://twitter.com">Twitter</a>. These small buttons allow your user's to share content instantly with their friends. Depending on which you're including on your site it'll show up differently, and each has a separate process to include them on your blog's pages. Since I am using <a href="http://wordpress.com">Wordpress</a> I will explain how to do this, but if you follow the example it should work in the broad case as well.</p>
<p>This functionality is provided by using meta information that is stored on the user's browser. Unless you decide to do something nefarious, you do not have to their data by merely adding these buttons, but it does expose your user's to a potential security risk. There are browser plugins that allow them to turn off this functionality if they have it enabled. If you're comfortable with all this, then go on ahead and follow the instructions.</p>
<p><a href="https://developers.facebook.com/docs/reference/plugins/like/">A useful wizard</a> is available that provides you with both the <a href="">XHTML</a> and Javascript necessary to make this functionality work correctly on your site. The Javascript code snippet provides the bridge between the user's browser and the Facebook social graph that this is using in the background. There are a few routes regarding how to implement it, I chose the HTML5 approach which asked me to add a schema namespace to the <em>HTML element</em>, and then used the custom <em>like button</em> element that is provided to display it.</p>
<p><strong>Javascript snippet</strong>&nbsp;<em>Place this after your BODY element</em><pre lang="javascript"><script src="//connect.facebook.net/en_US/all.js"></script>
        <div id="fb-root"></div>
        <script>(function(d, s, id) {
        var js, fjs = d.getElementsByTagName(s)[0];
        if (d.getElementById(id)) {return;}
        js = d.createElement(s); js.id = id;
        js.src = "//connect.facebook.net/en_US/all.js#xfbml=1&appId=309698452382243";
        fjs.parentNode.insertBefore(js, fjs);
        }(document, 'script', 'facebook-jssdk'));</script>
</pre>
<p><strong>HTML element</strong>&nbsp;<em>Place this where you want the button to appear.</em><pre lang="html"><fb:like href="http://example.com" send="true" layout="button_count" show_faces="true" action="recommend" font="lucida grande" display="inline"></fb:like></pre></p>
<p>You will be given the exact HTML element tag that you should use based upon your wizard settings. If you want to use this dynamically in the <a href="http://codex.wordpress.org/The_Loop">Wordpress Loop</a> to display under each post you'll have to use a PHP function <code>the_permalink();</code> which will return the URI to the page in question. This can also be done on the single pages if you so desire. One last step is to include meta information at the top of each page to let Facebook know how the post should be described in the user's activity feed. This is very straight forward and simple. An optional <em>title</em> element should be used on individual pages. Categories can be selected through the wizard.</p>
<p><strong>Meta information</strong>&nbsp;<em>Place this in the HEAD element</em><pre lang="html"><meta property="og:type" content="blog" />
<meta property="og:site_name" content="Thoughtless Banter" />
<meta property="fb:admins" content="199800257" /></pre></p>
<p>The <a href="http://plus.google.com">Google Plus</a> approach is very similar, and doesn't require any meta information tags. When a user decides to "+1" any of your posts they will in a special location on that user's profile, and in any the subscriber's feeds as well. You'll need to include a Javascript snippet, like above, and a special HTML tag element. You can add all of this below the Facebook directives if you desire.</p>
<p><strong>Javascript snippet</strong>&nbsp;<em>Place this after the BODY element.</em><pre lang="javascript"><script type="text/javascript">
  (function() {
    var po = document.createElement('script'); po.type = 'text/javascript'; po.async = true;
    po.src = 'https://apis.google.com/js/plusone.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(po, s);
  })();
</script></pre></p>
<p><strong>HTML element tag</strong>&nbsp;<em>Place this where you wish the button to appear.</em><pre lang="html"><g:plusone href="http://example.com" size="medium" annotation="inline"></g:plusone></pre></p>
<p>Finally, the Twitter button is the easiest to place, and they once again provide a wizard for you to change the colors of the background, design, and number of tweets you wish to show (if you do not just want a button, but rather the feed itself). This one-liner can be placed anywhere you want the button to appear.</p>
<p><pre lang="html"><a href="https://twitter.com/share" class="twitter-share-button" data-url="http://thoughtlessbanter.com/2011/11/23/furniture-for-men/" data-text="Furniture For Men" data-count="horizontal" data-via="johnbellone">Tweet</a><script type="text/javascript" src="//platform.twitter.com/widgets.js"></pre></p>
<p>That should basically the gist of how to get this functionality working on your website. Facebook offers more comprehensive widgets that take advantage of the social graph to display photos, and even information about user's actions on your page. There is beta examples of how to post directly to the new <a href="">Facebook Timeline</a> feature that will be rolling out to your profile shortly. As more and more of these snippets become available you should consider both the advantages and the disadvantages of using them. I know that many user's are worried about privacy and tracking that all the social sites are beginning to do. It is quite possible in the future that this type of functionality will be <em>opt-in</em> rather than <em>opt-out</em> and it may not work with the breadth of your user's without their explicit consent. So be wary designing your website around these widgets specifically.</p>


