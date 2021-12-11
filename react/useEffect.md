> [스파르타 코딩클럽] '임민영' 멘토님의 강의자료를 기반으로 정리하였습니다.

<br/>

## ⏲ useEffect()
라이프 사이클 함수 중 componentDidMount와 componentDidUpdate, componentWillUnmount를 합쳐 둔 것이다!
- 첫번째 인자인 화살표 함수 안에 렌더링 시 실행할 함수를 넣는다.
- 두번째 인자인 [] 디펜던시 어레이에 어떤 값을 넣어주면 그 값이 변할 때마다 첫번째 인자인 콜백함수를 실행한다.
- 첫번째 인자의 return()문은 componentWillUnmount 때 동작된다.

<br/>

  ```javascript
    
    const text = React.useRef(null);
    
    const hoverEvent = (e) => {
      // 이벤트가 발생한 요소를 확인할 수 있음.
      console.log(e.target);
      // ref와 같은 요소인지 확인.
      console.log(text.current);
    }
    
  
    // 첫번째 인자는 화살표 함수이다. 렌더링 시 실행할 함수가 들어간다.
    // 두번째 인자는 [] 디펜던시 어레이라고 부른다. 여기 넣어준 값이 변하면 첫번째 인자인 콜백함수를 실행한다.
    React.useEffect(() => {
      // 여기가 rendering 때 실행될 구문이 들어가는 부분이다.
      // componentDidMount, componentDidUpdate일 때 동작하는 부분이다.
      // 이벤트 리스너는 DOM 요소가 있어야 하기 때문에 이곳에 넣어준다.
      text.current.addEventListener("mouseover", hoverEvent);
      
      return () => {
        // componentWillUnmount 때 동작하는 부분이다.
        // clean up: 컴포넌트가 사라지면 등록한 이벤트를 삭제하는 것.
        // - 이벤트는 한번 등록되면 계속 남아있는다. 컴포넌트가 사라지면 이벤트가 실행되지 않겠지만, 남아있을 것이다.
        //   그렇기 때문에 깨끗하게 정리해주는 과정이 필요하다. 
        text.current.removeEventListener("mouseover", hoverEvent);
      };
    }, [text]);
  
  ```
  
  
  
  
  
  <br/><br/><br/>
  
