
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
상태값을 여러개 사용하는 또다른 방법은 reselect를 이용하는 방법이 있다.


```
import { createSelector } from 'reselect'

const getFriends = state => state.friend.friends;
const getAgeLimit = state => state.friend.ageLimit;
const getAgeShowLimit = state => state.friend.showLimit;
export const getFriendWithAgeLimit  = createSelector(
  [ getFriends, getAgeLimit ],
  (friends, ageLimit) => friends.filter(item => item.age <= ageLimit),
)

export const getFriendWithAgeShowLimit  = createSelector(
  [ getFriendWithAgeLimit , geShowtAgeLimit ],
  ( friendsWithAgeLimit, showLimit ) => friendsWithAgeLimit.slice(0, showLimit),
)

### 렌더링 부분

const [ 
  ageLimit,
  showLimit,
  friendsWithAgeLimit,
  friendsWithAgeShowLimit
] = useSelector(
  state => [
    getAgeLimit(state),
    getShowLimit(state),
    getFriendsWithAgeLimit(state),
    getFriendsWithAgeShowLimit(state)
  ],
  shallowEqual,
)

```

이렇게 작성을하면 값으로 넘어오는 변수들이 변경되었을때만 실행을 하기때문에 메모이제이션 기능을 쓴다.
