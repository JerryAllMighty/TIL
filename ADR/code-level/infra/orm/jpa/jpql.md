[@Query]
- 객체 지향 쿼리.
- SARGable(Search ARGumentable)
> DB가 인덱스를 사용할 수 있는 형태의 쿼리인지 판단. 
> 가급적 쿼리문 안에서 함수로 객체를 감싸는 것은 금지.
> 인덱스 여부와 상관없이 함수 사용하면 풀스캔 가능성.


[쿼리 객체 생성시, Type Query vs Query]
- 반환 타입 명확하게 지정 가능하면 TypeQuery, 아니면 Query
- 