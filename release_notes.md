OpenTok 2.0 iOS Client SDK release notes
========================================

Revision history
----------------

August 30, 2013 - Version 2.1.5

* New signaling API -- This version adds support for the new OpenTok signaling API. 
  You can now send messages with data to other clients connected to the OpenTok session you are connected to. 
  See the [OTSession signalWithType:data:completionHandler:],
  [OTSession signalWithType:data:connections:completionHandler:], 
  and [OTSession receiveSignalType:withHandler:] methods.
* Dynamic traffic shaping -- [OTSubscriberDelegate subscriberVideoDisabled:] 
  is invoked when the OpenTok media server stops sending video to a subscriber. 
  This feature of the OpenTok media server has a subscriber drop the video stream when
   connectivity degrades. The subscriber continues to receive the audio stream, if there is one.
* New connection events -- [OTSessionDelegate session:didCreateConnection:] and
  [OTSessionDelegate session:didDropConnection:] are invoked when clients connect to and disconnect from a session.
* iOS 7 Support -- This version resolves several iOS 7 compatability issues. Note that iOS 7 introduces a system-level
  end-user prompt for microphone access.

August 7, 2013 - Version 2.1.4

* Dynamic traffic shaping -- In non-peer-to peer sessions, OpenTok now dynamically
shapes audio and video to maximize the experience for every participant in a multi-point conversation. For more information,
see our [blog](http://www.tokbox.com/blog/quality-of-experience-and-traffic-shaping-the-next-step-with-mantis/).
In a non-peer-to peer session, setting `[OTSubscriber subscribeToAudio]` or `[OTSubscriber subscribeToAudio]` to `NO`
reduces the bandwidth consumed by the app. (The app does only receives audio and video streams that it subscribes to.)
* The `[OTSubscriber subscribeToAudio]` and `[OTSubscriber subscribeToVideo]` messages are now supported. 
* Background support improvements -- This version fixes some issues related to apps running in the background
* Other improvements -- This version includes other fixes for performance and stability.

July 3, 2013 - Version 2.1.3

* Fixed an issue preventing [OTVideoView getImageWithBlock:] from working correctly
* Added support for peer-to-peer sessions connecting with Firefox 22
* Fixed some reported crashes
* Fixed an issue with subscriber video quality introduced in 2.1.2

May 16, 2013 - Version 2.1.2

* Support for non-peer-to-peer sessions, using the OpenTok media server for WebRTC.
* Fixed some issues that were occurring when the OpenTok library ran in the background.
* Added native support for armv7s architecture.
* Fixed a bug that causes inconsistent UI when manipulating media track functions (e.g. publishVideo, subscribeToAudio, etc.)

April 24, 2013

*  OpenTok on WebRTC now provides increased connectivity. WebRTC is a peer-to-peer protocol that does not work on some
restricted networks. Many environments, especially cellular and corporate networks, have strict network policies that
prevent WebRTC apps from working. OpenTok on WebRTC now overcomes these restrictions to connect clients, even in
environments that have NAT-style firewalls. However, an app cannot use WebRTC if UDP is completely blocked on the
network.

April 9, 2013

* This is version 2.1.1 of the OpenTok iOS SDK.
* We have corrected the name of the `[OTPublisherDelegate publisher:didChangeCameraPosition:]` message. (See the notes for
April 5, 2013.)

April 5, 2013

* This is version 2.1 of the OpenTok on WebRTC iOS SDK.
* You can now specify the camera a publisher uses by setting the `[OTPublisher cameraPosition]` property. The OTPublisherDelegate sends
the `[OTPublisherDelegate publisherDidChange:cameraPosition:]` message in response to a camera change.
* Publishers and subscribers now continue to publish and subscribe to streams when running in the background.
* This release improves connectivity between WebRTC clients.
* This release includes bug fixes to improve performance and stability.


Known issues
------------

* Some features available in the OpenTok SDK for other platforms (such as JavaScript) are not supported in the OpenTok iOS SDK. These unsupported features include peer-to-peer streaming and archiving.

* The OpenTok iOS SDK supports iOS 5 and later only.

* Our graphics rendering pipeline causes this error to be logged when debugging: "CGContextDrawImage: invalid context 0x0." This should not affect the performance of your app. If you experience video quality issues, please let us know.

* You cannot target the iOS Simulator. Build and deploy to a supported iOS device.

* The OpenTok iOS SDK includes echo suppression for subscriber and publisher streams in the same app. However, you
may experience echoes when testing an app on two iOS devices *in the same room or in close proximity* (or on one
iOS device and in a nearby web browser using the OpenTok JavaScript client library). In this test scenario, mute
the audio in one of the devices (or the web browser) or use headphones.


Peer-to-peer streaming Limitations
----------------------------------

* If you use a peer-to-peer session that already has two connected clients, calling `[OTSession connectWithApiKey:token:]`
results in the `[OTSessionDelegate session:didFailWithError:]` message. The error message is defined by the
`OTP2PSessionMaxParticipants` enum in the OTError.h file.

* In a a peer-to-peer session, you cannot subscribe to a stream published by your own app. If you call
`[OTSubscriber initWithStream:delegate:]` passing in a stream you publish, the OTSubscriberDelegate sends
the `[OTSubscriberDelegate subscriber:didFailWithError:]` message. The error message is defined by the
`OTSelfSubscribeFailure` enum in the OTError.h file.
