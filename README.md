Author: Jiajun Zhang

### gapy: A concise wrapper for Google Analytics Reporting API V4.

If you want to get pageviews and other statistics with Google Analytics and you really don't 
want to do it in frontend. Guess what, getting it at backend is pretty simple.

Please refer following steps:

#### 1. Get an account

https://support.google.com/analytics/answer/1008015?hl=en

#### 2. Add your webpage domain to your GA account

https://support.google.com/analytics/answer/1042508

#### 3. Add analytics.js to your webpage source code

https://developers.google.com/analytics/devguides/collection/analyticsjs/
Remember to replace the track ID of your own webpage created in step2. After this, you can 
relaunch your webpage to the server.
Now if you go to https://analytics.google.com/ and login with your account, you can get
every statistic about your webpage, including number of pageviews and visitors.

#### 4. Get statistics from backend(Python)
If you are using Flask or Django, you can look at gapy.py code and try to do the same thing
at your own backend. This is very common if you building your own admin page for a database
management system. Based on Google Analytics Reporting API v4, it also offers JAVA and PHP API. 

Please follow this guide to enable and install this API:
https://developers.google.com/analytics/devguides/reporting/core/v4/quickstart/service-py
Basically, you need to enable API, get your key, generate a JSON key file, and refer to the 
tracking ID in previous steps.

You can also see the exact helloAnalytics.py sample there. However in gapy, you can use one
function to obtain useful pageviews data. Have a try:

		analytics = initialize_analyticsreporting()

		print get_pageviews_array(analytics, '6daysAgo', 'today', 'day')
		print get_pageviews_array(analytics, '27daysAgo', 'today', 'week')
		print get_pageviews_array(analytics, '2017-05-01', 'today', 'month')
		print get_pageviews_array(analytics, '2017-01-01', 'today', 'year')
		print get_pageviews_array(analytics, '2017-01-01', 'today', 'total')
		
Output is something like this:
		# per day
		[['2017-07-04', '2017-07-05', '2017-07-06', '2017-07-07', '2017-07-08', '2017-07-09', '2017-07-10'], [1, 0, 1, 1, 0, 6, 4]]
		# per week
		[['2017-24', '2017-25', '2017-26', '2017-27', '2017-28'], [0, 11, 45, 4, 10]]
		# per month
		[['2017-05', '2017-06', '2017-07'], [0, 46, 24]]
		# per year
		[['2017'], [70]]
		# in total
		[[''], [70]]
		
Pretty simple right? Then you can send the result to your application admin page.



