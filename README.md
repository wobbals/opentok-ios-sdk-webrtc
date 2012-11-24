OpenTok WebRTC for iOS SDK
==========================

This SDK lets you use OpenTok on WebRTC video sessions in apps you build for iPad, iPhone, and iPod touch devices.

To get started, [sign up for a Developer Account](https://dashboard.tokbox.com/signups/new) and get your API Key.

You can use OpenTok video sessions across iOS devices AND web clients that use OpenTok on
WebRTC. For details about using this SDK with web clients, see the
[JavaScript documentation](http://www.tokbox.com/opentok/api/documentation/v2) at the TokBox website.

Using the OpenTok WebRTC for iOS SDK
------------------------------------

[Reference Documentation for the OpenTok iOS SDK](http://www.tokbox.com/opentok/ios/docs/index.html)

There are two important differences to keep in mind when working with the OpenTok WebRTC for iOS SDK (compared with
the [non-WebRTC version](https://github.com/opentok/opentok-ios-sdk) of the OpenTok iOS SDK):

*  You must use a [peer-to-peer streaming](http://www.tokbox.com/opentok/api/tools/js/documentation/overview/peer_to_peer.html)
   enabled OpenTok Session. You can enable p2p when creating a session using the Project Tools on your
   [Developer Dashboard](https://dashboard.tokbox.com/projects) or enable it for any Session created with
   our supported [server-side libraries](http://www.tokbox.com/opentok/api/tools/documentation/api/server_side_libraries.html).

   Peer-to-peer streaming helps reduce latency by letting the media stream skip a hop to an external server,
   resulting in better performance. A few limitations introduced by this technique are discussed below.

*  At this time you cannot run your application in the iOS Simulator, just run it on your device for testing. We will
   be addressing this in a future release.

Supported devices
-----------------

The OpenTok WebRTC for iOS SDK is supported on the following devices:

* iPhone 4S / 5
* iPad 2 / 3 / 4 / mini

The OpenTok WebRTC for iOS SDK is supported on wifi connections.

OpenTokHello Sample App
--------------------

You can test the OpenTok WebRTC for iOS SDK using the `webrtc` branch of the
[OpenTokHello Sample App](https://github.com/opentok/OpenTok-iOS-Hello-World/tree/webrtc)

1. Use `git clone --recursive -b webrtc https://github.com/opentok/OpenTok-iOS-Hello-World.git` to obtain the 
   OpenTokHello Sample App project.

2. Generate an OpenTok Session with p2p enabled and a Token for the session. You can use your Project Tools on the 
   [Developer Dashboard](https://dashboard.tokbox.com/projects) or a
   [server-side library](http://www.tokbox.com/opentok/api/tools/documentation/api/server_side_libraries.html).

3. Open the OpenTokHelloWorld project in XCode.

4. Edit the ViewController.m file in the OpenTokHelloWorld project.

   Change the values of the `kApiKey`, `kSessionId`, and `kToken` constants to match your API key, the peer-to-peer session ID
   you generated, and the token you generated.

5. Select an iOS Device to target from the Scheme chooser in Xcode. Run the application (play button).

6. You will test the app using the `browser_demo.html` file, included in the OpenTokHelloWorld project. Edit the 
   `browser_demo.html` file:

   Edit the `apiKey`, `sessionId`, and `token` variables to use your API key, the peer-to-peer session ID you generated,
   and a generated token (for the session).

7. Open the `browser_demo.html` file in a web browser and connect to the session. You should now be subscribing
   in the browser to the stream that is published from the iOS device. You can also publish from the browser and
   the iOS device should automatically subscribe.

   ***Note:*** You will not be able to subscribe properly if opening `browser_demo.html` from the `file:///` URL Scheme.
   One quick way to start an HTTP server from the Terminal is to run
   `open http://localhost:8000/browser_demo.html && python -m SimpleHTTPServer` on command line from the project directory.
   This will start a server on port 8000 and open a new window with the right URL loaded.

   You can also test the app on two iOS devices (instead of an iOS device and a web browser).

Peer-to-peer Streaming Limitations
----------------------------------

If you use a session that does not support peer-to-peer streaming, calling `[OTSession connectWithApiKey:token:]`
results in the `[OTSessionDelegate session:didFailWithError:]` message. The error message is defined by the
`OTP2PSessionRequired` enum in the OTError.h file.

If a session already has two connected clients, calling `[OTSession connectWithApiKey:token:]`
results in the `[OTSessionDelegate session:didFailWithError:]` message. The error message is defined by the
`OTP2PSessionMaxParticipants` enum in the OTError.h file.

You cannot subscribe to a stream published by your own app. If you call `[OTSubscriber initWithStream:delegate:]`
passing in a stream you publish, the OTSubscriberDelegate sends the `[OTSubscriberDelegate subscriber:didFailWithError:]`
message. The error message is defined by the `OTSelfSubscribeFailure` enum in the OTError.h file.

Known Issues
------------

The following features are currently unsupported in this version of the OpenTok WebRTC for iOS SDK:

* The `[OTPublisher publishAudio]` and `[OTPublisher publishVideo]` messages
* The `[OTSubscriber subscribeToAudio]` and `[OTSubscriber subscribeToVideo]` messages
* You cannot target the iOS Simulator. Build and deploy to a supported iOS device.

In XCode, you need to remove armv7s from the Valid Architectures section of the Build Settings for your project.

Support
-------

Support is available at the OpenTok iOS forum: <http://www.tokbox.com/forums/ios>
