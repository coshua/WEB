### Transition
Transition 은 요소가 최종 목적지를 갖고 변화하는 것을 지칭한다.

기본적인 규칙은 transition은 초기 상태 속성에 지정해준다. button:hover 에 transition 효과를 보여주고 싶다면 button에 지정한다.

transition 의 속성에는 property, duration, timing-function, delay 가 있다.
* property: 화면 이동에 영향을 받는 속성으로 이 값을 지정하면 특정 사항에 대해서만 이동 효과가 나타난다. 
* duration: 트랜지션이 일어나는 지속 시간
* timing-function: 변화율에 대한 함수이다 (점점 빠르게 변화, 점점 느리게 변화).
* delay: 이 시간만큼 지연시킨다.

#### property
기본적으로 all, 모든 속성을 가르킨다. font-size 처럼 특정한 속성을 지정할 수 있다.

#### duration
기본값이 0이기 때문에 지정해주지 않으면 트랜지션이 일어나지 않는다.

#### timing-function
바로 쓸 수 있는 키워드는 대표적으로
* linear: 등속도, 처음부터 끝까지 흐름이 일정하게 유지된다.
* ease: 점진적인 가속, 기본값은 ease 로서 느리게 시작한 후 빠르게 가속되다가 다시 느리게 끝난다.
* ease-in: 가속, 애니메이션이 느리게 시작된 후 빠름 흐름으로 끝난다.
* ease-out: 감속, 애니메이션이 빠르게 시작된 후 느리게 끝난다.
* ease-in-out: 점진적인 가속 후에 감속, 느리게 시작한 후 중간 지점에서 빨라지다가 다시 느려지면서 끝나므로 ease 와 비슷하지만, 
그 변화가 더 부드럽다.

#### delay
기본값은 0으로, 별도 지정하지 않으면 바로 트랜지션이 일어난다.
