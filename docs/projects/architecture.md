# Architecture

Keep this page current — replace the diagram and component list as the design evolves.
Prefer simple, explainable architecture over cleverness; you will need to defend this
verbally in interviews.

## Current Architecture (v1)

```
[Source Docs] -> [Chunking] -> [Embedding Model] -> [Vector Store]
                                                          |
[User Query] -> [Embed Query] -> [Retrieve top-k] -------+
                                        |
                                        v
                              [Gemini Generation] -> [Answer]
```

## Component Notes

| Component | Choice | Why |
|---|---|---|
| Chunking strategy | | |
| Embedding model | | |
| Vector store | | |
| Generation model | | |

## Known Limitations (current version)

-
