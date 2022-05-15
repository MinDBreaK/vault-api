Hello 👋, fellow programmer. Welcome the big brain part 🧠. This page of the documentation describes some internal functioning of the library, how to extend library functionality.

## Request Process

```flowchart
             vault(config)
             function call
                   │
                   │
        ┌──────────▼──────────┐
        │ Merge defaultConfig │
        │         and         │
        │   config parameter  │
        └──────────┬──────────┘
                   │
                   │
┌──────────────────▼──────────────────┐
│ call all configs of type`function`  │
│       and validate the values       │
└──────────────────┬──────────────────┘
                   │
                   │
       ┌───────────▼───────────┐
       │ if`engine` paramater  │
       │ is not explicitly set │
       │ call  `getEngineName` │
       └───────────┬───────────┘
                   │
                   │
 ┌─────────────────▼─────────────────┐
 │ call `Engine.preRequest` function │
 │       to get requestConfigs       │
 └─────────────────┬─────────────────┘
                   │
                   │             
      ┌────────────▼────────────┐
      │ validate requestConfigs │
      └────────────┬────────────┘
                   │
                   │
     ┌─────────────▼─────────────┐
     │ send `axios` httprequest  │
     └─────────────┬─────────────┘
                   │
                   │
┌──────────────────▼──────────────────┐
│ call  `Engine.postRequest` function │
│   to  transform `config.response`   │
└──────────────────┬──────────────────┘
                   │
                   │
                   ▼
       return  `config.response`
```
