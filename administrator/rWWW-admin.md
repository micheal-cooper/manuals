# rWWW Administration

<!-- MarkdownTOC  depth=0 autolink=true bracket=round -->

- [Home Page Anatomy](#home-page-anatomy)
	- [Hero Slide Show](#hero-slide-show)
	- [News Carousel](#news-carousel)
	- [OIST for Okinawa](#oist-for-okinawa)
	- [Choose OIST](#choose-oist)
	- [Connect](#connect)
	- [Events](#events)
	- [Subscribe to OIST Newsletters](#subscribe-to-oist-newsletters)
	- [Social Media Buttons](#social-media-buttons)
	- [Footer](#footer)
- [Content Types](#content-types)
	- [News Article and Press Release Nodes](#news-article-and-press-release-nodes)
		- [Home Page Image](#home-page-image)
		- [Related Videos](#related-videos)
		- [Related Images](#related-images)
		- [Related Image](#related-image)
		- [Embed Photos and Video Nodes in the Body](#embed-photos-and-video-nodes-in-the-body)
- [News Center Top Page Anatomy](#news-center-top-page-anatomy)
	- [News Center Hero Featured Story](#news-center-hero-featured-story)
- [Troubleshooting](#troubleshooting)
	- [Content on GROUPS is visible in View but not Edit](#content-on-groups-is-visible-in-view-but-not-edit)

<!-- /MarkdownTOC -->



## Home Page Anatomy

### Hero Slide Show

Each item in the slideshow is either a photo or an Advert (advertisement) for something like a News Article or Press Release, an upcoming event like a concert or Open Campus, a new division or service, or anything else that we want to highlight.

* Defined at `Nodequeue : Home Page Slide Show`:
* Each item is a `Slide` Node, the image of which must be 1140px:380px (w:h).
* Each Advert has a Title and a Teaser:
	-  The Title can be a link to the news article being plugged, a signup form for the event being advertised, etc..
	-  The Teaser should be additional information, like a slogan, the date and time for an event, or the teaser of the research article being featured.

### News Carousel

The latest News Articles and Press Releases.

* Defined at `Nodequeue : Homepage News Items`.
* Comprised of [News Article and Press Release Nodes](#news-article-and-press-release-nodes).
* Custom code makes sure that 9 news items are shown when you view the page. If this nodequeue contains less than 9 items of each language, the system will pull the latest news article items to make the total 9, so always keep 9 stories in here. 
* See the link for details about the [Home Page Image](#home-page-image) and how it is used in the News Carousel.

### OIST for Okinawa

* Defined at `Structure : Mini panels : Okinawa Panel (okinawa_panel)`.
* Don't mess with `Settings`, `Context`, `Layout`, or `Content` here.
* To change the content of this Mini Panel, edit the Blocks that define the content by going to `Structure : Blocks`:
	- `Front Page Okinawa Panel Left`
	- `Front Page Okinawa Panel Right`

### Choose OIST

* The Mini Panel is defined at `Structure : Mini panels : Front Page Bottom Sections` but the content is defined at `Structure : Blocks : Front Page Bottom Left`.

### Connect

* The Mini Panel is defined at `Structure : Mini panels : Front Page Bottom Sections` but the content is defined at `Structure : Blocks : Front Page Bottom Right`.

### Events

* The contents show in `Structure : Mini panels : Front Page Bottom Sections`, but it is populated by code that brings a feed groups.oist.jp - `Calendar - All-OIST Responsive Public Calendar` (https://groups.oist.jp/admin/structure/views/view/responsive_public_calendar/edit/upcoming). The limit of 4 items is in the View on groups.list.jp.

### Subscribe to OIST Newsletters
* The Mini Panel is defined at `Structure : Mini panels : Front Page Bottom Sections`.

### Social Media Buttons
* The Mini Panel is defined at `Structure : Mini panels : Front Page Bottom Sections`, also under the title 'Connect'.

### Footer
* The Header and Footer settings were built into the Theme to make them portable to all/new sites.
* Get there by going straight to '/admin/appearance/settings/oist_master_main' or 
	- Admin Menu > Appearance
	- Click Settings of active theme
	- OIST Master Specific Settings Section
	- Header and Footer Tabs


## Content Types

### News Article and Press Release Nodes

#### Home Page Image

The `Home Page Image` represents the article, giving the reader a way to identify the article as she goes from Home Page to News Center to the article, through search results, and so on.

* Must be 1140px:380px (w:h).
* Is the top Hero image at the top of the article Node view, where readers read the article.
* Is resized and used as the thumbnail for the image in the Home Page [News Carousel](#news-carousel) and in article lists in the News Center and in search results.
* Is used as the `Featured Story Image` in the News Center when its node is at the top of `Nodequeue : Home Page Featured`.
* The same image file can and should be used as the image for the 'Slide' Node when this News Article or Press Release is featured in the [Hero Slide Show](#hero-slide-show).

#### Related Videos

* Type or paste the Title of the Node slowly, allowing the site autocomplete to find the Node for you, then select the Node. You should see the Node ID in parentheses when you are successful.

#### Related Images

* No longer used.


#### Related Image

* As with `Related Videos`, type or paste the Title of the Node slowly, allowing the site autocomplete to find the Node for you, then select the Node.
* Appear as blocks at the bottom of the page.

#### Embed Photos and Video Nodes in the Body

* Embed Photo and Video Nodes in the flow of the text using the syntax `[[nid:11731 view_mode:node_embed]]`, where "11731" is replaced by the Node ID of the Node you want to embed.
* http://oist-responsive.xenostaging.com/news-center/news/2014/8/5/okinawa-summer-safety
* http://oist-responsive.xenostaging.com/news-center/news/2014/4/8/oist-outing-himeyuri-peace-park-and-okinawa-world



## News Center Top Page Anatomy

### News Center Hero Featured Story

* Determined by the top node in `Nodequeue: Homepage News Items`.


















## Troubleshooting

### Content on GROUPS is visible in View but not Edit

This issue is caused by both content translation ( Internationalization module ) and field translation ( Entity translation module) being used on groups.oist.jp on different content types. These two modules are better not to be used simultaneously on a site.

Four content types (Page, Event, FAQ and Webform) are using content translation which creates a separate node for the JA content. All other content types are using field translation which does not create a separate node for the JA content but stores the EN and JA content for each field in the database separately. It is only effecting the body field because that is the only field that is common to all content types and once that field is set to be "translatable", it becomes translatable for all content types. 

When you try to edit the node, the system is looking for the field translation for the body field which does not exist, since that "Page" content type is set to use content translation.

The issue is also described at https://www.drupal.org/node/1885588, and this problem occurred on WWW a couple years ago (https://xenomedia.basecamphq.com/projects/8066016-oist-web/todo_items/166982297/comments).

Senem: It was a quick fix on WWW because there was no content with field translations so disabling entity translation and doing some database adjustments fixed it. In the case of GROUPS, however, it will not be an easy fix since there is a lot of content involved. One thought would be to change those four content types to use field translations and migrate the content but this needs to be carefully tested especially considering the webforms - and all custom code groups site has. Considering the number of dev hours required, I would advice leaving it as is if it is not a major issue - or schedule for future.

