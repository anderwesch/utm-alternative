Below are some suggestions on how to use the plugin:

<h2>Adwords</h2>
With the new Upgraded URLs of Adwords (July 2015), it is very easy to implement utm-alternative. What you should do is add to the src value to the "URL options". For example, if you want the new cookie to have the keyword that triggered the ad from which the converted user arrived, then I suggest the following: 
<pre>{lpurl}?src=aw-{keyword}</pre> The aw tells you this lead came from an Adwords campaign, followed by the keyword that is generated automatically.
If you want to add to the campaign id of Adwords, you can use: <pre>{lpurl}?src={campaignid}</pre> If using remarketing and want this data directly in the lead source, then you can use: <pre>{lpurl}?src={campaignid}-remarketing</pre>You can theoretically add any value you want (and remember to adhere to your privacy statement).

You can find all the parameters of adwords here: https://support.google.com/adwords/answer/2375447?hl=en

<h3>Adwords Auto-tagging</h3>
If you use the utm_alternative (version 2.0) using the utm_campaign as the tracking parameter, you might encounter difficulties with adwords autotagging, which omits the utm_campaign and does everything for you very conventiently. If you want to keep on using utm_alternative, while keep using Adwords' autotagging, the best way is to can adjust utm-alternative in such a way that it will always take the utm_campaign, unless there is a custom parameter in the url as well. 

To do so, replace the following line: 

<pre>var urlParamSRC = getURLParameter(tracking_parameter); //get value of the query string parameter (if any)</pre>

With:
<pre>
if  (isNotNullOrEmpty(getURLParameter(tracking_parameter))) {
			var urlParamSRC = getURLParameter(tracking_parameter); //get value of traffic source query string parameter
		} else {
			var urlParamSRC = getURLParameter("utm_campaign"); //get value of utm_campaign query string parameter (if any)
		}
</pre>

Now, just add to your adwords campaign the "src" query string parameter (or any other parameter based on your settings). Again, with Upgraded URLs and Adwords Editor, this job is very easy to do. 

<h2>Linkedin and others</h2>
With linkedin and other platform, you will have to tag your target URLs manually, therefore you can easily add the src parameter in the following way:<pre>www.example.com/?utm_source=Linkedin&utm_medium=cpc&utm_content=XXX&utm_campaign=YOURCAMPAIGN&src=YOURCAMPAIGN</pre>

What you can also do, that will add value to your tracking, is to add ad creative to the src (the utm_campaign stays intact):<pre>www.example.com/?utm_source=Linkedin&utm_medium=cpc&utm_content=XXX&utm_campaign=YOURCAMPAIGN&src=YOURCAMPAIGN<b>-01</b></pre>
You can always see which ads generated conversions on google analytics, but in simple implementations og Analytics you cannot associate it with specific users, since GA data is anonymous. This approach will help you to do that. But note that it is hard to manage when you have a lot of ads - you have to keep track on creatives and their numbers. You can also add the whole ad content to the src if you would like. 

<h2>Navigation inside the site</h2>
The plugin can be also used to track navigation inside the site. What you have to do is to add src parameter to your own internal links. Important note: if you do that, remember to tell search engines that this parameter does not affect page content. Otherwise, search engines will show your website urls with the src in it - this will mess up your tracking completely. In Google Webmstertools, go to Crawl-->URL Parameters-->Add parameter. (From my experience, google doesn't always follow this directive, and the tracking parameter still appeared on search results. Make your own tests to be sure). 
