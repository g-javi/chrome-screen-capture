# chrome-screen-capture

> This chrome extension simply captures content of your screen. It returns `source-id` to callee; and that `source-id` can be used as `chromeMediaSourceId` in WebRTC applications to capture screen's MediaStream.


## Usage

```javascript
// add event listener for the sourceId
window.addEventListener('message', (event) => {
	if (event.data.sourceId) {
    
    const mediaConstrains = {
      audio: false,
      video: {
          mandatory: {
              chromeMediaSourceId: event.data.sourceId
              chromeMediaSource: 'screen',
              maxWidth: window.screen.width > 1920 ? window.screen.width : 1920,
              maxHeight: window.screen.height > 1080 ? window.screen.height : 1080
          },
          optional: []
      }
    };
    
    navigator.mediaDevices.getUserMedia(mediaConstrains)
      .then( stream => {
        // do something with the stream
      });
	}
});

// trigger sourceId request
window.postMessage('get-sourceId', '*');

```

## How to publish?

Learn more about how to publish a chrome extension in Google App Store:

* https://developer.chrome.com/webstore/publish
