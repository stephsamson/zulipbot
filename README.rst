zulipbot
=========

The unofficial Python API for Zulip bots. A Zulip email and API key are needed to use this.

To get your bot's Zulip email and API key, go to
your Settings page and scroll down to the Your Bots section.

Usage
-----
To install: ``pip install zulipbot``

Initialization
^^^^^^^^^^^^^^
Identify your Zulip bot's email and API key, and make a new Bot object.

.. code-block :: python

    >>> import zulipbot
    >>> email = 'foo@bar.baz'
    >>> key = 'spammyeggs'
    >>> my_bot = zulipbot.Bot(email, key)

Bot Methods
^^^^^^^^^^^
Note: The Bot class inherits from the ``zulip.Client`` class.

For an example on how the below methods work together in a program, check out `example.py`_.

.. _example.py: https://github.com/stephsamson/zulipbot/blob/master/example.py


``subscribe_to_all_streams`` - Subscribes to all Zulip streams.


``send_private_message`` and ``send_stream_message`` both have the same parameters: ``message_info`` and ``content``, i.e. the function signature for the two aforementioned methods is ``send_[[private||stream]]_message(message_info, content)``. 


``message_info`` is the message meta-info dictionary that you acquire from the function callback that processes messages. ``content`` is the response that you want your bot to make.


Another method of note is ``send_message`` (a ``zulip.Client`` method) which I abstracted away in ``send_private_message`` and ``send_stream_message``. It takes a dictionary with the keys ``type``, ``to``, ``content``, and ``subject`` (optional, ``subject`` is only needed for the ``type`` stream).


.. code-block :: python

    >>> my_bot = zulipbot.Bot(email, key)
    >>> my_bot.send_message({
          'type': 'stream',
          'to': 'bot playground', # this is the stream name or user name
          'subject': 'Hello!',
          'content': 'I\'m the newest bot!' 
        })
