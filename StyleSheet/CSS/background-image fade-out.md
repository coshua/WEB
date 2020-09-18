background 를 천천히 fade-out, fade-in 으로 바꿔주고 싶었으나 background image 는 애니메이션 불가능한 속성이다. 따라서 transition 과 같은 속성으로 건드릴 수가 없다.

background-blend-mode 를 이용해서 꼼수를 쓸 수 있다. background-color 와 image 를 블랜드 하고 color 의 transparent 를 조절해서 원하는 효과를 얻어낸다.

background-color 를 rgba 값으로 정해주면 transparent 를 조절할 수 있다.

적용해보자.

fade-out 했을때 남는 배경색이 하얀색이고 싶다면 하얀색과, 검정이고 싶다면 검정과 blend 한다. `transition: background-color 2s` `background-color: rgba(255, 255, 255, 1)`
이런식으로 color에 transition 값을 준다. blend 모드에 따라 결과물이 다른데, 이는 이미지마다 효과가 상이하므로 직접 적용해보도록 하자.

live demo 에서 실시간으로 수정사항을 확인 가능하다.
https://tympanus.net/codrops-playground/SaraSoueidan/lc3XhUii/editor

image 마다 내용물이 다르지만 하양 또는 검정의 transparent 값이 1일때 blend 의 결과물이 완전히 하양 또는 검정으로 나오는 blend-mode 만 간략하게 정리해봤다.
```css
rgba(0, 0, 0, 1) //검은색
background-blend-mode: hue, saturation, soft-light, color, color-burn, color-dodge, multiply, overlay, darken

rgba(255, 255, 255, 1) //하얀색
background-blend-mode: soft-light, color-burn, color-dodge, lighten, overlay, screen
```
이미지마다 color 를 하양 또는 검정으로 써서 필요한 색을 만들 수도 있지만, 여기서 공통되는 mode 를 이용하면 하양이든 검정이든 상관없이 원하는 효과를 얻을 수 있다

soft-light, color-burn, color-dodge, overlay 네 가지 mode가 그렇다.
