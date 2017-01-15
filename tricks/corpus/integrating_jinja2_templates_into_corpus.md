Integrating jinja2 templates into corpus
========================================

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


