# Chatterbot Tricks

[![print-small](https://cloud.githubusercontent.com/assets/13664257/21971242/bd4ca508-dbd4-11e6-846e-2eef4a211135.png)](https://gitprint.com/vkosuri/chatterbot-tricks/blob/master/README.md)

Most commonly used [chatterbot](https://github.com/gunthercox/ChatterBot) tips and tricks

# Table of Contents

1. [Chatterbot test into events](#chatbot-text-into-events)
2. [Combination of both voice and chat](#combination-of-both-voice-and-chat)
3. [Prioritizing some response over others](#prioritizing-some-responses-over-others)
4. [Integrating Jinja2 templates into corpus](#integrating-jinja2-templates-into-corpus)


## Chatbot text into events

Ref: [#482](https://github.com/gunthercox/ChatterBot/issues/482)

Creating efficient scheduling operations can often be a challenging problem to solve. What about offloading the task to the user's calendar? Most calendar apps already display notifications when a scheduled event is coming up, and it would also make it possible synchronize the events across the user's devices if they were all connected to the same calendar.

    https://msdn.microsoft.com/en-us/office/office365/api/calendar-rest-operations
    https://developers.google.com/google-apps/calendar/v3/reference/

## Combination of both voice and chat

Ref: [#416](https://github.com/gunthercox/ChatterBot/issues/416)

I think it's definitely possible, but because it's a web app the audio will have to be processed on the client's side. This might make things easier because there is likely several javascript libraries available that handle speech recognition and speech synthesis. It looks like Google Chrome has built in support for both speech recognition and speech synthesis: https://developers.google.com/web/updates/2014/01/Web-apps-that-talk-Introduction-to-the-Speech-Synthesis-API

To implement this, you would have to add some javascript to listen to the user's speech, then it could send that to the Django ChatterBot

## Prioritizing some response over others

Ref : [#518](https://github.com/gunthercox/ChatterBot/issues/518)

If you have a way to train your bot with the desired responses you could use
the [get_most_frequent_response](http://chatterbot.readthedocs.io/en/latest/logic/response_selection.html#chatterbot.response_selection.get_most_frequent_response) response selection method. Training multiple
times with the desired data would increment occurrence counts for those responses and it would ensure that they get selected. Using [training](http://chatterbot.readthedocs.io/en/latest/training.html#training-via-list-data) to increment the occurrence counts is probably the most efficient way to do this.

## Integrating jinja2 templates into corpus

Ref : [#518](https://github.com/gunthercox/ChatterBot/issues/518)

With reference [#469](https://github.com/gunthercox/ChatterBot/issues/469) I felt introducing jinja2 template into corpus, A more useful to users and developers.

```Json
{
    "conversations": [
        [
            "What's you name",
            "{{bot.name}}"
        ],
        [
            "How many years",
            "{{bot.years}}"
        ]   
    ]
}
```

```Python
from chatterbot import ChatBot
from chatterbot.trainers import ListTrainer
from jinja2 import Environment, FileSystemLoader
import json
import os

# Jinja2 corpus template
THIS_DIR = os.path.dirname(os.path.abspath(__file__))
env = Environment(loader=FileSystemLoader(THIS_DIR), trim_blocks=True)
properties = {"name":"Chatterbot" , "years":2}
corpus_template = env.get_template('example.corpus.json').render(bot=properties)
print(corpus_template)
corpus_data = json.loads(corpus_template)

# Train chatterbot
chatterbot = ChatBot("Template Training Example")
chatterbot.set_trainer(ListTrainer)
for pair in corpus_data['conversations']:
    chatterbot.train(pair)
```




## Pull Requests are most welcome!!

