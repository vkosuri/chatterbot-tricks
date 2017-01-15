Prioritizing some responses over others
=======================================

Ref : [#518](https://github.com/gunthercox/ChatterBot/issues/518)

If you have a way to train your bot with the desired responses you could use
the [get_most_frequent_response](http://chatterbot.readthedocs.io/en/latest/logic/response_selection.html#chatterbot.response_selection.get_most_frequent_response) response selection method. Training multiple
times with the desired data would increment occurrence counts for those responses and it would ensure that they get selected. Using [training](http://chatterbot.readthedocs.io/en/latest/training.html#training-via-list-data) to increment the occurrence counts is probably the most efficient way to do this.
