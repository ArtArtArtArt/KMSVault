---
type: 
 - definition
tags:
---

## Monorepo is 

```
├── lib
|   ├── lib
|   └── lib
├── lib
├── lib
├── lib
├── app
|   ├── lib
|   └── lib
|       ├── lib
|       └── lib
├── app
|   └── lib
└── big-project
|   ├── lib
|   ├── app
|   |   ├── lib
|   |   └── lib
|   └── app
|       └── lib
└── big-project
    ├── lib
    ├── lib
    ├── app
    |   └── lib
    └── app
        ├── lib
        └── lib
```

For monorepo sevices as Bit are common because they help create a component repository which will be easy to reuse. It can be pushed to a repository and added to any project using a package system.

## Polyrepo is 

```
github.com/myorg/app1
├── docs
├── examples
├── src
└── tests

github.com/myorg/app2
├── docs
└── src

github.com/myorg/app3
├── lib
|   └── src
├── lib
|   └── src
└── lib
    └── src

github.com/myorg/lib1
└── src
```


