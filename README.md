# Google Analytics

It's a wrapper for Node [googleanalytics](https://github.com/ncb000gt/node-googleanalytics) package.


# Description

Pull data from Google Analytics for use in projects.

The library maintains tracking of the token so that you don't have to and will push the token around with your requests.
Should you require a different token, just create a new GA instance. However, this is asynchronous through eventing so if you do want the token you can latch onto the event.


# Usage

Add this pacakge to your Meteor project: `meteor add jss:ga`

With a user and password:

```javascript
var ga = new GAnalytics.GA({
  user: 'myusername',
  password: 'mypassword'
});

ga.login(function(err, token) {
  var options = {
    'ids': 'ga:<profileid>',
    'start-date': '2010-09-01',
    'end-date': '2010-09-30',
    'dimensions': 'ga:pagePath',
    'metrics': 'ga:pageviews',
    'sort': '-ga:pagePath'
  };

  ga.get(options, function(err, entries) {
   console.log(JSON.stringify(entries));
  });
});
```

If you have already gotten permission from a user, you can simply use the oAuth access token you have:

```javascript
var ga = new GAnalytics.GA({
  token: 'XXXXXXXXXXXX'
});

var options = {
 'ids': 'ga:<profileid>',
  'start-date': '2010-09-01',
  'end-date': '2010-09-30',
  'dimensions': 'ga:pagePath',
  'metrics': 'ga:pageviews',
  'sort': '-ga:pagePath'
};

 ga.get(options, function(err, entries) {
  console.log.debug(JSON.stringify(entries));
});
```

You can specify the type of token by setting 'tokenType', default is 'Bearer'.

See [node-gapitoken](https://github.com/bsphere/node-gapitoken) for easy service account Server to Server authorization flow.

# Event API

* token(err, token)
* entries(err, entries)


# Entry API

* metrics[]
* dimensions[]

Each array contains objects. These objects contain the following:

* name — The name of the metric or dimension requested
* value — The value associated. If the value is a Number, it is parsed for you. Otherwise, it will be a string.

# License

This project is under MIT license.

--------------------

Made by [![Custom Software Development Company](https://s3-eu-west-1.amazonaws.com/jssolutions/github/jss_xs.png)](http://jssolutionsdev.com/) - [Custom Software Development Company](http://jssolutionsdev.com/)
