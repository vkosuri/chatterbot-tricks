
Combination of both voice and chat
==================================

Ref: [#416](https://github.com/gunthercox/ChatterBot/issues/416)

I think it's definitely possible, but because it's a web app the audio will have to be processed on the client's side. This might make things easier because there is likely several javascript libraries available that handle speech recognition and speech synthesis. It looks like Google Chrome has built in support for both speech recognition and speech synthesis: https://developers.google.com/web/updates/2014/01/Web-apps-that-talk-Introduction-to-the-Speech-Synthesis-API

To implement this, you would have to add some javascript to listen to the user's speech, then it could send that to the Django ChatterBot API to get the response. Once the response was returned, it could be spoken aloud to the user.