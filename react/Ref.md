> [스파르타 코딩클럽] '임민영' 멘토님의 강의자료를 기반으로 정리하였습니다.

<br/>

## Ref
리액트 요소를 가지고 오는 방법이다.

### React 요소를 가지고 오는 방법 1. React.createRef()

  ```javascript
  
    class App extends React.Component {
      constructor(props){
        super(props);
        // App 컴포넌트의 state를 정의한다.
        this.state = {
          list: ["음악 듣기", "드라마 보기", "밥 먹기"],
        };
        // ref 선언하기
        this.text = React.createRef();
      }
      
      render(
        <div className="App">
          <input type="text" ref={this.text}/>
        </div>
      );
    }
  
  ```
  
### React 요소를 가지고 오는 방법 2. React.useRef()

  ```javascript
  
    const BucketList = ({list}) => {
      const my_lists = list;
      const my_wrap = React.useRef(null);
      
      return(
        <div ref={my_wrap}>
          {my_list.map((list, index) => {
            return <div key={index}>{list}</div>
          })}
        </div>
      );
    }
  
  ```
  
  
<br/><br/><br/>
