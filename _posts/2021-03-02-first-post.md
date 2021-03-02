
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

매번 shallowEqual을 쓰는 것은 불편하여 커스텀 훅을 만들어서 사용하길 권장

```
function useMyselector(selector) {
  return useSelector(selector, shallowEqual);
}

const [value, value2] = useMyselector(state => [state.value1, state.value2]);
```
이렇게 커스텀 훅을 사용할때는 모든 값을 비교하기 때문에 배열로 반환해주는 것이 좋다.
```
const [value4] = useMyselector(state => [state.value4])

```
