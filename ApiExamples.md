
```
<html>
<head>
    <title>Tweet Bitly Link Example</title>
</head>
<body>
    
<a href="http://twitter.com/home?status=I+am+reading+documentation+of+http://test.example/webpage" class="tweetlink">tweet this link</a>

<!-- REPLACE WITH YOUR login AND apiKey -->
<script type="text/javascript" charset="utf-8" src="http://bit.ly/javascript-api.js?version=latest&login=bitlyapidemo&apiKey=R_0da49e0a9118ff35f52f629d2d71bf07"></script>
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.3.2/jquery.js"></script>

<script>
var TweetThisLink = {
    shorten : function(e) {
        // this stops the click, which will later be handled in the  response method
        e.preventDefault();
        // find the link starting at the second 'http://'
        var url = this.href.substr(this.href.indexOf('http:',5));
        BitlyClient.shorten(url, 'TweetThisLink.response');
    },
    
    response : function(data) {
        var bitly_link = null;
        for (var r in data.results) {
            bitly_link = data.results[r]['shortUrl']; 
            break;
        }
        var tweet_text = "I am reading documentation of"
        document.location = "http://twitter.com/home?status=" + encodeURIComponent(tweet_text + ' ' + bitly_link);
    }
}


jQuery('.tweetlink').bind('click', TweetThisLink.shorten);

// this is cool if you are adding links to dom on the fly
//jQuery('.tweetlink').live('click', TweetThisLink.shorten);
</script>
</body>
</html>
```