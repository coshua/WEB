## 01. Bootstrap 기본

### badge

badge로 컴포넌트를 꾸며줄 수 있다.

'badge-light' property로 badge를 parent component 안으로 넣을 수 있다.

아래 코드는 'Notification'이라는 버튼 안에 작은 숫자로 몇개의 소식이 있는지 보여준다.
인스타그램이나 페이스북에서 보던 것과 비슷하게 디스플레이 한다.

```
<button type="button" class="btn btn-primary">
  Notification <span class="badge badge-light">12</span>
</button>
```

### pagination

웹페이지 하단에 있는 페이지 탐색 컴포넌트를 만들어 제공한다. 
'active' class 로 현재 있는 페이지 번호를 강조해서 나타낼 수 있다. 특정 페이지 누르는 것을 disabled 시킬 수 있다. 페이지가 맨 처음이거나 맨 마지막일 때 주로 활용한다.

```
<ui class="pagination">
  <li class="page-item">
    <a class="page-link" href="/1">1</a>
  </li>
  <li>
    <a class="page-link" href="/2">2</a>
  </li>
</ui>
