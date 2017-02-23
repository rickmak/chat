[![Build Status](https://travis-ci.org/SkygearIO/chat.svg)](https://travis-ci.org/SkygearIO/chat)
# Chat Plugin for Skygear

## Related SDK

You can find the SDK code in following repos on github. You can also directly
install at the package manager. 

- JS - [chat-SDK-JS](https://www.npmjs.com/package/skygear-chat) on npm

    Source: https://github.com/SkygearIO/chat-SDK-JS
- iOS - [SKYKitChat](https://cocoapods.org/pods/SKYKitChat) on cocoapods

    Source: https://github.com/SkygearIO/chat-SDK-iOS
- Android - [chat-SDK-Android] io.skygear.chat on jscentre

    Source: https://github.com/SkygearIO/chat-SDK-Android

### Get the demo running at Skygear cloud 

__First__

Assumed you go registered at `https://portal.skygeario.com`

__Second__ 

git submodule to import the source code.

```
git submodule add https://github.com/SkygearIO/chat.git chat
```

In your cloud code, import the chat plugin. Skygear will load and lambda and
database hook will be ready for use.
```python

from skygear.settings import settings

from .chat import includeme

includeme(settings)
```

__Third__

Tell Skygear cloud to serve the asset from chat-SDK-JS demo folder

git submodule to import the JS SDK source code.

```
git submodule add https://github.com/SkygearIO/chat-SDK-JS.git chat-SDK-JS
```

```python
from skygear import static_assets
from skygear.utils.assets import relative_assets

@static_assets(prefix='demo')
def chat_demo():
    return relative_assets('chat-SDK-JS/demo')
```

`https://<your_app_name>.skygeario.com/static/demo/index.html`

### Quick Start

We provide Quick Start tutorial in different language.

- [Javascript][js-quick-start]
- [Android][android-quick-start]
- [iOS][ios-quick-start]

We also have basic guide go through feature by feature.

- [Javascript][js-basic]
- [Android][android-basic]
- [iOS][ios-basic]

### Understanding the model

In this chat plugin, we have various model represent different data in
application. Understanding the model relation make you able to use the plugin
efficiently. It also enable developer to store application specific data in
the correct model.

Following is the model relation diagram.

![Entity Relation][er]

#### Overview of models responsibility are as follow.

- User - Skygear provided user. Storing user attributes.
- Conversation - represent a conversation, it store conversation information
  like title, last message, no. of participant.
- Message - actual message display on screen, it store message text,
  related asset and metadata.
- UserConversation - represent a user is participating a conversation. It
  stores user specific information to a conversation, like last
  read time and unread count.
- Receipt - Store the user receipt on a message.

### Details attributes on models

Following is the table of attributes ensured by this plugin.

Note that `User` is Skygear provided User profile model.

__User__

| Attributes  | Type                | Description  |
| ------ | ------------------- | ------------ |
| name  | <code>String</code> | |

__Conversation__

| Attributes  | Type                | Description  |
| ------ | ------------------- | ------------ |
| title  | <code>String</code> | |
| admin_ids | <code>JSON Array</code> | |
| participant_ids | <code>JSON Array</code> | |
| participant_count | <code>Number</code> | |
| distinct_by_participants | <code>Boolean</code> | |
| metadata | <code>JSON Object</code> | |
| last_message | <code>Reference</code> | |

__Message__

| Attributes  | Type                | Description  |
| ------ | ------------------- | ------------ |
| body  | <code>String</code> | |
| conversation_status | <code>String</code> | Summary of receipt status |
| attachment | <code>Asset</code> | |
| metadata | <code>JSON Object</code> | |
| conversation_id | <code>Reference</code> | |

__UserConversation__

| Attributes  | Type                | Description  |
| ------ | ------------------- | ------------ |
| unread_count  | <code>Number</code> | |
| last_read_message | <code>Reference</code> | |
| user | <code>Reference</code> | |
| conversation | <code>Reference</code> | |

__Recript__

| Attributes  | Type                | Description  |
| ------ | ------------------- | ------------ |
| read_at  | <code>Datetime</code> | |
| delivered_at | <code>Datetime</code> | |
| user_id | <code>Reference</code> | |
| message_id | <code>Reference</code> | |

## Detail API

For API detail, please visit the platform specific API filie:

- [JS SDK](https://doc.esdoc.org/github.com/skygeario/chat-SDK-JS/)
- [iOS SDK](http://cocoadocs.org/docsets/SKYKitChat/)
- [Android SDK](https://docs.skygear.io/android/plugins/chat/reference/) 

[er]: https://github.com/rickmak/chat/raw/master/doc/er.png "ER diagram"
[js-quick-start]: https://docs.skygear.io/guides/chat-quick-start/js/
[android-quick-start]: https://docs.skygear.io/guides/chat-quick-start/android/
[ios-quick-start]: https://docs.skygear.io/guides/chat-quick-start/ios/
[js-basic]: https://docs.skygear.io/guides/chat/basics/js/
[android-basic]: https://docs.skygear.io/guides/chat/basics/android/
[ios-basic]: https://docs.skygear.io/guides/chat/basics/ios/
