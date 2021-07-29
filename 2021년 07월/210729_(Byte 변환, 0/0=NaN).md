### 1. JavaScript로 Byte 변환하기

```typescript
function formatBytes(bytes, decimals = 2) {
    if (bytes === 0) return '0 Bytes';

    const k = 1024;
    const dm = decimals < 0 ? 0 : decimals;
    const sizes = ['Bytes', 'KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB'];

    const i = Math.floor(Math.log(bytes) / Math.log(k));

    return parseFloat((bytes / Math.pow(k, i)).toFixed(dm)) + ' ' + sizes[i];
}
```

log로 변환하는 이유는 여러 가지가 있을 수 있지만 여기서 쓰이는 이유는
지수를 얻기 위함이다.

바이트를 1024로 한 번 나누면 KB가 되고,
두 번 나누면 MB가 되는 것을 알 수 있다.

예)
참고로 Math.log10() 함수를 쓰면 밑이 10인 로그를 취하여 값을 반환한다.

1024->1000이라 치고
10KB가 입력되었다고 가정하면
`Math.log10(10000)/Math.log10(1000) = 4/3 = 1.333333...`이고 소수점 버리면 `1`이다.

10MB가 입력되었다고 가정하면
`Math.log10(10000000)/Math.log10(1000) = 7/3 = 2.333333...`이고 소수점 버리면 `2`이다.

즉,
i에는 입력된 Byte의 크기가 KB 면 1, MB 면 2, GB 면 3이 저장된다.   
Math.log() 함수는 자연로그를 취한 값을 반환하며 이 함수를 써도 결과는 똑같다.   
결과적으로 1024를 i 만큼 제곱한 값을 나눠주고 소수점 자른 다음 단위 값이 출력되는 것을 확인할 수 있다.



***

https://stackoverflow.com/questions/15900485/correct-way-to-convert-size-in-bytes-to-kb-mb-gb-in-javascript

<br/>


***
***

### 2. `0 / 0 = NaN` (JavaScript)

- https://stackoverflow.com/questions/18838301/in-javascript-why-does-zero-divided-by-zero-return-nan-but-any-other-divided-b
- https://bekusib.tistory.com/70


