Page-Requested Reader Mode (PRRM)
=================================

.. image:: https://licensebuttons.net/l/by-nc-sa/3.0/80x15.png
   :target: https://creativecommons.org/licenses/by-nc-sa/4.0/
   :alt: License: Creative Commons BY-NC-SA 4.0


Status
------

- Author: Josh Bronson <jabronson@gmail.com>
- Last updated: 2018-04-01

This is currently a first draft in need of comments.
Please share with anyone you know who would be interested.
Critical feedback gratefully received.
[#fn-evidence]_


What is Reader Mode?
--------------------

Reader Mode is an accessibility-enhancing feature
that users of popular browsers
(e.g.
[#fn-reader-mode-firefox]_
[#fn-reader-mode-edge]_
[#fn-reader-mode-safari]_
[#fn-reader-mode-chrome]_
[#fn-reader-mode-opera-mini]_
[#fn-reader-mode-ucbrowser]_
[#fn-reader-mode-vivaldi]_
)
can use to improve the reading experience
of a page they're viewing.


Proposal: Page-Requested Reader Mode (PRRM)
-------------------------------------------

There should be a standard [#fn-standard]_ API for web pages
to proactively request that Reader Mode be used by default
(for users with a supporting browser or browser extension),
rather than requiring each user to enable Reader Mode manually.


Target Users
------------

The target users of this API
are publishers (and publishing platforms)
that prioritize their readers
having a fast-loading and high-quality reading experience
over a highly-customized or heavily-branded one,
at least in some cases
(e.g. users with bad internet connections,
low-end devices, etc.).

Target users benefiting from this API include
everyone who reads low-reading-quality and/or slow-loading pages
who would prefer (consciously or otherwise)
that Reader Mode be used instead.


(Straw-man) API Proposal
------------------------

One possible API for PRRM could be
an HTTP response header such as:

.. code::

   Reader-Mode: true

or equivalently:

.. code:: html

   <meta http-equiv="Reader-Mode" content="true">

(See [#fn-api-prior-art]_ for prior art.)

The possible values could be limited to only ``true``
to signify
"please automatically activate Reader Mode for this page by default".
This would provide a great deal of value
in and of itself,
without need for any additional API surface.

However, for more flexibility,
a value of ``auto`` could also be available
to indicate that browser[ extension]s should decide
whether to proactively activate Reader Mode
based on inputs that they are free to choose
(e.g. quality of the internet connection,
availability of system resources, etc.).

(See [#fn-api-bikeshed]_ for other ideas.)


Problem
-------

This proposal addresses a two-sided problem:

#. Publishers want to provide a good reading experience for their audience
   but cannot currently do so without adding nontrivial page weight.

   Adding page weight can often make the reading experience worse,
   especially for users with bad connections or low-end devices,
   due to longer times-to-first-contentful-paint,
   longer times-to-interactive, etc.

#. Readers want a fast-loading, high-quality reading experience,
   but regularly find that pages fail on one or both counts.


Impact
------

#. The negative impact of heavy pages is large and well-understood.
   Publishers and readers alike pay additional costs in
   bandwidth, time, frustration, and missed opportunity.

   Users who consume more bandwidth than they can afford
   suffer when they run out of quota or when the bill comes.

   Users who wait longer than they can afford give up and close pages early.
   Content goes unread, unappreciated, and unshared. Calls to action go unseen.

   Publishers and readers both lose.

   As usual,
   **less-privileged users are disproportionately affected**
   (e.g. those with bad connections or low-end devices).

#. When pages offer a bad reading experience,
   **which is the default when no dedicated styling code is added**,
   sighted users may strain their eyes,
   struggle to read and therefore absorb less,
   and/or become frustrated having to make extra effort to compensate.

   Again, users may give up and close pages early.

   And again,
   **less-privileged users are disproportionately affected**
   (e.g. users in older age groups,
   with lower vision,
   other accessibility issues,
   users without assistive technology).


Status Quo
----------

#. Some publishers have decided that adding styles that improve readability
   either isn't worth the additional effort
   or isn't worth the additional page weight,
   letting readability suffer instead.

   Others end up including code in their pages
   for uncustomized, off-the-shelf themes
   that succeed in improving readability,
   but that increase page weight prohibitively
   for some of their audience.

   Still others decide to spend some effort trying to improve readability,
   but lack the knowledge and expertise to succeed.
   The result may be (still-) hard to read, slow to load, or both.

   In all of these cases,
   a significant number of publishers
   would prefer to use PRRM
   if it were available rather than what they're currently doing.

#. Users who are able and inclined
   may install a special browser extension that improves poor readability.
   A quick look through the results of e.g.
   [#fn-gws-chrome-reader-mode]_,
   [#fn-cws-reader-mode]_,
   [#fn-quora-auto-reader-mode]_,
   etc.
   shows the high demand for this feature among such users.

   Users may also use a built-in Reader Mode feature
   if offered by their browser.

#. Browsers such as
   Firefox [#fn-reader-mode-firefox]_,
   Edge [#fn-reader-mode-edge]_,
   Safari [#fn-reader-mode-safari]_,
   Chrome [#fn-reader-mode-chrome]_,
   and others
   (
   [#fn-reader-mode-opera-mini]_
   [#fn-reader-mode-ucbrowser]_
   [#fn-reader-mode-vivaldi]_
   )
   provide a built-in Reader Mode feature.

   Because it's implemented in browsers already,
   native Reader Mode costs nothing extra
   in terms of page load time or publisher effort.

   But it has serious costs on the part of users.
   To benefit from native Reader Mode,
   each user must:

   #. know/remember that the feature exists, and

   #. go to the trouble of manually activating it
      (and then only after waiting long enough
      for enough of the page to load
      for manual activation to become possible).
      [#fn-manual-activation]_

   However,

   #. Many users don't actually know that native Reader Mode exists,
      or think to use it when they would prefer to.
      [#fn-native-awareness]_

   #. Among users who do activate Reader Mode manually,
      many say they wish it were activated automatically more often,
      because either the small icon button
      is a pain to repeatedly have to click,
      the browser already has sufficient context to know
      when Reader Mode should be used,
      or both.


Benefits of PRRM
----------------

#. Between (a) the set of publishers who would prefer
   that Reader Mode be used on their pages,
   and (b) their readers who would also prefer that it be used,
   the publishers are structurally in a better position to enable it.

   By definition, publishers as a set think more consciously
   about providing a reading experience on the web,
   have more to gain from improving the reading experience of their content,
   and – most impactfully – could use PRRM
   to improve the experience for all their readers at once
   with as little as a one-line code change.

   On the other hand, to achieve the same effect,
   for each site that would benefit from Reader Mode that does not use PRRM,
   all *N* of its readers would have to first know about Reader Mode
   and then go to the trouble to activate it manually.

#. Publishers who have already invested in improved reading experiences
   (at the likely cost of page load time)
   could still use PRRM to signal that
   Reader Mode is preferred.

   Since a PRRM-supporting browser[ extension]
   could discover the use of PRRM early in the page load
   (the PRRM can be placed within the first few bytes of the response),
   **it could optimize the remainder of the page loading process**,
   ignoring content it can predict will have no impact on the end result
   (e.g. a background image that would not be shown anyway).

#. PRRM would result in publishers and readers incurring less
   bandwidth, time, and missed-opportunity costs
   while benefiting from providing and enjoying
   a better reading experience.


Risks
-----

#. Technical risk of implementing basic support,
   i.e. just ``true`` or ``true|false|auto)``,
   is expected to be low.

   Implementation appears to be doable in a handful of lines of code
   whose maintenance burden is in turn expected to be low.

   Browsers and extensions should ignore HTTP headers
   (and corresponding ``<meta http-equiv>`` tags)
   they don't recognize,
   so there is low risk of breaking clients that predate this feature.

#. There is a risk that readers will prefer to deactivate Reader Mode
   for a page where it is enabled automatically.

   This should be rare,
   but in cases where it happens,
   the user could toggle off Reader Mode manually
   using the existing UI as usual.

   As an additional hedge,
   the first time a user overrides a PRRM
   that the browser[ extension] had honored,
   the browser[ extension] could offer to ignore PRRM
   for the page (or even for all pages) in the future.

#. The biggest risk is low adoption.

   Since people can only adopt something they know about,
   uptake depends first on publicizing PRRM to interested parties.
   [#fn-please-share]_

   There is a chicken-and-egg effect
   between publishers and browser[ extension] software providers.
   Each side may wait for the other to adopt first.

   Like any two-sided adoption problem,
   the more you chip away at one side,
   the more incentive there is for the other side to adopt.

   On the software side,
   patches could be submitted to
   open source Reader Mode browser extensions
   [#fn-open-source-reader-mode-extensions]_
   that add support for PRRM.

   On the publisher side,
   several authors of popular, independent blogs
   have said they would use the PRRM API already,
   given that it's a simple and low-cost change
   with the potential for outsized benefits.

   Patches could also be submitted to some of
   the many open source readability themes
   [#fn-open-source-readability-themes]_
   that add the PRRM tag.
   This would accelerate adoption as PRRM use
   flowed to their many downstream users.

   Thinking bigger,
   large publishing platforms
   such as Medium, Blogger, Wordpress, etc.,
   that control the reading experience for diverse sets of readers
   of content generated by the many authors publishing on their platforms,
   and that have already invested in more complex technologies
   to improve the experience for their readers,
   are especially incentivized to adopt PRRM
   to increase the usage and usability of their platforms,
   especially by readers with bad connections or low-end devices.

   Getting PRRM support contemporaneously landed
   in both Blogger and Chrome
   (or some Chrome extension with significant usage)
   could alone make a significant impact
   to accessibility on the web.


Conclusion
----------

The low risks/costs of implementation,
potential for outsized benefits,
and emergence of interested early adopters already
suggest that further discusion
of standardization and potential adoption
would be worthwhile.


Inspiration
-----------

#. Experiencing firsthand
   the uncountable number of bytes, hours, dollars, and opportunities
   that this problem has cost,
   as a reader with both impaired vision and a 2G internet connection,
   and also as a software engineer
   with expertise in web optimization.

#. The many popular bloggers who have struggled with slow-loading pages
   they inherited from their blogging software,
   many of whom ultimately dropped technologies
   that provided a better reading experience
   in preference to shipping lighter pages
   (see e.g.
   [#fn-danluu-web-bloat]_
   [#fn-danluu-octopress]_
   [#fn-meownica-web-fonts]_
   and many others).


References
----------

.. [#fn-evidence] The claims in this proposal
   are based on common and collective professional experience,
   as well as wider polling of affected users.
   In many cases, rigorous research has already been done
   that supports these conclusions.
   Please help provide citations of any relevant research you know about.

.. [#fn-reader-mode-firefox] https://support.mozilla.org/en-US/kb/firefox-reader-view-clutter-free-web-pages
.. [#fn-reader-mode-edge] https://docs.microsoft.com/en-us/microsoft-edge/dev-guide/browser-features/reading-view
.. [#fn-reader-mode-safari] https://support.apple.com/en-gb/guide/safari/read-articles-clutter-free-sfri32632/mac 
.. [#fn-reader-mode-chrome] https://github.com/chromium/dom-distiller (work in progress)
.. [#fn-reader-mode-opera-mini] https://blogs.opera.com/mobile/2016/09/opera-android-gets-new-look/
.. [#fn-reader-mode-ucbrowser] http://www.ucweb.com/wor/prd/prd/android-phone-bbtrn-15263.html
.. [#fn-reader-mode-vivaldi] https://help.vivaldi.com/article/reader-view/

.. [#fn-standard] as in *de facto* standard.
   Reader Mode itself is not currently an official standard.
   (Though some official guidelines or standardization
   of Reader Mode itself could also benefit users.)

.. [#fn-api-prior-art] https://docs.microsoft.com/en-us/microsoft-edge/dev-guide/browser-features/reading-view#opting-out-of-reading-view

.. [#fn-api-bikeshed] For compatibility with the possibility
   that browser[ extension]s
   automatically activate Reader Mode
   in the absence of an explicit Reader Mode request,
   an explicit value of ``false`` could also be available,
   to request that Reader Mode not be activated automatically.

   For still more flexibility,
   a DSL could allow for making the PRRM request conditional.
   For example,
   "only activate Reader Mode if the effective connection is worse than 3g"
   could look something like this:

   .. code::

      Reader-Mode: connection.effectiveType < 3g

   (Inspired by the
   `navigator.connection API
   <https://developer.mozilla.org/en-US/docs/Web/API/Navigator/connection>`__.)

   Pending evidence to the contrary,
   this proposal recommends only implementing support for ``(true|auto|false)``
   as the best balance between flexibility and complexity.


.. [#fn-gws-chrome-reader-mode] https://www.google.com/search?q=chrome+reader+mode
.. [#fn-cws-reader-mode] https://chrome.google.com/webstore/search/reader%20mode?_category=extensions
.. [#fn-quora-auto-reader-mode] https://www.quora.com/Is-there-any-Android-web-browser-that-will-load-a-webpage-directly-in-reading-mode-like-Pocket-app

.. [#fn-manual-activation] At least one browser (Safari) allows
   activating Reader Mode for an entire site,
   so users don't have to activate it manually as often,
   but this feature is even less discoverable
   than the basic Reader Mode feature:
   Safari buries per-site Reader Mode in a hidden menu
   that is only revealed after long-pressing on the
   "activate Reader Mode" button.
   So even fewer users know about per-site Reader Mode.

.. [#fn-native-awareness] Its availability is only indicated
   by a small, unlabeled icon in the address bar
   that users often never notice in the first place.

   Those users who do notice the icon there are often uninclined to click it.
   For these users,
   the icon is unfamiliar and insufficiently self-explanatory,
   does not look obviously like something clickable,
   or is placed in a context where they're not expecting
   to find buttons that can change the page (inside the address bar).

   When users who don't know about Reader Mode are shown the feature,
   many say they would have used it if they had known about it,
   and would like to use it in the future.

.. [#fn-please-share] If you like this idea,
   please star this repo
   and provide any additional feedback you may have.
   If you know others who would like the idea,
   please spread the word!

.. [#fn-open-source-reader-mode-extensions] https://www.google.com/search?q=chrome+reader+mode+github
.. [#fn-open-source-readability-themes] https://www.google.com/search?q=readability+theme+github

.. [#fn-danluu-web-bloat] http://danluu.com/web-bloat/
.. [#fn-danluu-octopress] http://danluu.com/octopress-speedup/
.. [#fn-meownica-web-fonts] https://meowni.ca/posts/web-fonts/
