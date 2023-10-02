# Jotai

## Jotai ?
매우 작은 3kb의 번들 사이즈와 타입스크립트 지향적.
recoil에 비해 1/6정도의 번들 사이즈를 가지고 있어 매우 작은 크기로 작동하기에 가볍고 사용하기 부담 없음.
React.js, Next.js, React Native에서 사용 가능.

Context의 리렌더링 문제를 해결하기 위해 등장했으며 recoil에서 영감 받아 atomic한 상태 관리 방식으로 구현됨.

### 사용법

```ts
import { atom, useAtom } from 'jotai';

const textAtom = atom('hello');

const Input = () => {
  const [text, setText] = useAtom(textAtom)
  const handleChange = (e) => setText(e.target.value)
  return (
    <input value={text} onChange={handleChange} />
  )
}
```

## 3가지 파생 atom 만들기
1. Read-only atom
    -------
    get을 사용해서 atom 값을 읽을 수 있고 읽은 값을 아래 예시처럼 원하는 값으로 변환 후 값을 제공

2. Write-only atom
    -------
    수정(쓰기) 기능은 set을 이용하여 제공
3. Read-Write atom
    -------
    읽기 및 쓰기 모두 가능

```ts
import { atom } from 'jotai';

const priceAtom = atom(10);

const readOnlyAtom = atom((get) => get(priceAtom) * 2);
// const [price] = useAtom(readOnlyAtom);

const writeOnlyAtom = atom(
  null,
  (get, set, update) => {
    set(priceAtom, get(priceAtom) - update.discount)
  }
);
// const [, setPrice] = useAtom(writeOnlyAtom);

const readWriteAtom = atom(
  (get) => get(priceAtom) * 2,
  (get, set, newPrice) => {
    set(priceAtom, newPrice / 2)
   }
);
// const [price, setPrice] = useAtom(readWriteAtom);
```

## 출처
https://medium.com/pinkfong/jotai%EB%8A%94-%EC%A1%B0-%ED%83%80%EC%9D%B4-%EB%9D%BC%EA%B3%A0-%EC%9D%BD%EC%8A%B5%EB%8B%88%EB%8B%A4-6498535abe11

