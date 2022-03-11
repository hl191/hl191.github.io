---
layout: page
title: Python
permalink: /python/
---

# NgxTranslate to CSV and back

[@ngx-translate](https://www.npmjs.com/package/@ngx-translate/core) is a NPM dependency, which uses a json to provide internationalization possibilities in e.g. Angular applications.

The json may be structured and contain nested translation keys:
```json
{
    "HOME": {
        "HELLO": "hello {{value}}"
    }
}
```

For external translation services I needed to extract the values into a CSV and then load the translated CSV back to our application. You may check out the python script [here](https://github.com/hl191/python-playground/tree/main/ngxtranslation).
