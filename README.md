node-spotify-webhelper
======================

Node.js interface for the Spotify WebHelper API, based on this great article: http://cgbystrom.com/articles/deconstructing-spotifys-builtin-http-server/

The API interacts with the SpotifyWebHelper process via HTTP. For windows, the module checks whether SpotifyWebHelper.exe is running, and try to run it if not.

API:

This module exposes the SpotifyWebHelper object, which exposes  the following methods:

 - **getStatus (cb : function(err, res))** -  get current status information (name of song/artist which is currently playing, etc..)
 - **pause (cb : function(err, res))** - pause currently playing song
 - **unpause (cb : function(err, res))** - unpause currently playing song
 - **play (spotifyurl : string, cb : function(err, res))** - play the given spotify url
 - **Constructor ({port : number (optional), protocol : string (optional)})** - Creates a new SpotifyWebHelper object, 
    The default port is set to 4381 as well as a default protocol of http, in some cases, you might want to use 4370 and https instead.

Example:
```javascript
var nodeSpotifyWebHelper = require('node-spotify-webhelper');
var spotify = new nodeSpotifyWebHelper.SpotifyWebHelper();

// get the name of the song which is currently playing
spotify.getStatus(function (err, res) {
  if (err) {
    return console.error(err);
  }

  console.info('currently playing:', 
    res.track.artist_resource.name, '-',  
    res.track.track_resource.name);
});
```