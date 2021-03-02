
---
title: "Redux selector 관련"
date: 2021-03-02
categories:
  - blog
tags:
  - redux
  - selector
---


```
const [friends, frends2] = useSelector(state => [state.friend.friends, state.friend.friends2], shallowEqual)

```
friends, friends2의 레퍼런스만 비교하는 것이 아니고 각각을 비교하기 때문에 friends 만 렌더링이 된다.


