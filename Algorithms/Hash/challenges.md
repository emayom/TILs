[2023 KAKAO BLIND RECRUITMENT - 개인정보 수집 유효기간](https://school.programmers.co.kr/learn/courses/30/lessons/150370)

```js
function solution(today, terms, privacies) {
    const tday = new Date(today).getTime();    
    
    const term_table = new Map(terms.map(term => {
        const [type, exp] = term.split(' ');
        return [type, Number(exp)]
    }));
    
    const exp_list = privacies.map((p, idx)=> {
        const [date, type] = p.split(' ');
        const exp = new Date(date);
        
        exp.setMonth(exp.getMonth() + term_table.get(type));
        exp.setDate(exp.getDate() - 1);
 
        return exp.getTime();
    });

    return exp_list.map((exp, idx) => tday - exp > 0 && idx + 1)
                    .filter(Boolean);
}
```

[프로그래머스 - 전화번호 목록](https://school.programmers.co.kr/learn/courses/30/lessons/42577)

```js
function solution(phone_book) {
    const table = new Map(phone_book.map(number => [number, true]));
    
    return !phone_book.find((number)=> 
                // 불필요한 배열 변환 과정 존재 
                number.split('').find((_, idx) => idx && table.has(number.slice(0, idx)))
            );
}
```

```js
function solution(phone_book) {
    const table = new Map(phone_book.map(number => [number, true]));
    
    return !phone_book.find((number)=> {
        for(let i = 1; i < number.length; i++){
            if(table.has(number.slice(0, i))){
                return true;
            }
        }
        return false;
    });
}
```

##### Review 
```
제한 사항
- phone_book의 길이는 1 이상 1,000,000 이하입니다.
    - 각 전화번호의 길이는 1 이상 20 이하입니다.
    - 같은 전화번호가 중복해서 들어있지 않습니다.
```

`정렬 후 탐색`, `해시 테이블 활용 방식` 모두 풀이가 가능하지만 카테고리가 **해시**인 만큼 해시 테이블을 활용하는 접근 방식을 선택했다. 

접두어를 비교하기 위해 키를 기반으로 많은 접근이 요구되는 상황에서 `Map`의 `has` 메서드를 통해 직관적으로 키에 접근하기 위해 `Map` 객체를 활용하여 해시 테이블을 구현했다. (Map의 경우 내부적으로 해시 테이블로 구현되어 키 기반 데이터 접근이 빠르다. 다만 잦은 갱신이 필요할 경우에는 `Object`와 비교하여 효율적이지 않을 수 있지만, 이 문제에서는 정적인 해시 테이블로 활용되어 크게 문제가 되지않을 것이다.)

해시 테이블을 구현 할 경우 메모리의 사용량이 증가하고, 공간 복잡도가 높아진다는 단점이 있다.  
해당 문제의 제한 사항에 따르면 키의 개수는 1 이상 1,000,000 이하이며 개별 키는 1 이상 20 이하의 문자열로 제한되어 있다.  
값(value) 역시 primitive `boolean` 타입으로 고려하였을 때 메모리 측면에서 큰 부담이 없을 것이라고 판단했다.  
