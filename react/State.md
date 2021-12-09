> [스파르타 코딩클럽] '임민영' 멘토님의 강의자료를 기반으로 정리하였습니다.

<br/><br/>

## State 관리
### 단방향 데이터 흐름
: 데이터는 위에서 아래로, 부모에서 자식으로 넘겨줘야 한다.
- 단뱡향으로 써야하는 이유 <br/>
  : 부모 컴포넌트의 state가 업데이트 되면 자식 컴포넌트도 리렌더링이 된다.<br/>
    만약 자식 컴포넌트의 state가 바뀐 걸 부모 컴포넌트가 props로 받는다고 한다면 자식 컴포넌트가 업데이트 될 때
    부모 컴포넌트도 업데이트 된다. !!그러면 부모 컴포넌트가 업데이트 되니까 또 자식 컴포넌트가 리렌더링 될 것이다...
<br/><br/>

### 함수형 컴포넌트에서 state 관리: useState()
: 함수형 컴포넌트는 클래스형처럼 자체적으로 state를 가지고 있지 않지만, react hooks를 사용하면 state를 가질 수 있다.

  ```javascript
    
    import React from 'react';
    
    const Memo = (props) =>{
      
      // count에는 state 값이, setCount는 count라는 state 값을 수정하는 함수이다.
      // useState(초기값): () 안에 초기값을 넣어준다.
      const [count, setCount] = React.useState(3);
      
      const addCount = () => {
        // setCount를 통해서 count에 저장된 값을 +1 해준다.
        setCount(count + 1);
      }
      
      const removeCount = () => {
        setCount(count>0 ? count-1 : 0);
      }
    
      return(
        <div>
          <div>{count}</div>
          <button onClick={addCount}>하나 추가</button>
          <button onClick={removeCount}>하나 빼기</button>
        </div>
      );
    }
  
  ```

    
<br/><br/><br/>
