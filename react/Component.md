## Component 
- 컴포넌트는 한 가지의 기능을 수행하는 UI 단위이다.<br/>
- 웹 사이트를 컴포넌트로 잘 나누는 사람이 리액트를 잘 사용하는 사람이다.<br/>
- 리액트는 컴포넌트를 잘 조립해서 어플리케이션을 만든다.
<br/><br/>

### state
component가 가지고 있는 데이터이다. component에 들어있는 데이터를 나타내는 오브젝트이다.

### props
component가 부모 component로부터 받아온 데이터이다. 자식 component는 부모로부터 받은 props를 수정할 수 없다.

<br/><br/>

## 함수형 Component

  ```javascript
  
    // 리액트 패키지를 불러온다.
    import React from 'react';
    
    // props는 부모 컴포넌트에게 받아온 데이터이다.
    const BucketList = (props) => {
    
      // 컴포넌트가 뿌려줄 UI 요소( 리액트 엘리먼트 )를 반환한다.
      return(
          <div>
            버킷 리스트
          </div>
      );
    }
    
    // 만든 함수형 컴포넌트를 export 해준다.
    // export해주면 다른 컴포넌트에서도 BucketList 컴포넌트를 불러와서 사용할 수 있다.
    export default BucketList;
    
  ```
  <br/><br/>
  
## 클래스형 Component
  
 #### state의 데이터가 변경되면 자동으로 render 함수가 호출된다.
  
  ```javascript
      
     import React from 'react';
     // BucketList 컴포넌트를 import 해온다.
     // import [컴포넌트명] from [컴포넌트가 있는 파일경로];
     import BucketList from './BucketList';
    
     class App extends React.Component {
        
       constructor(props){
         super(props);
          
         // App 컴포넌트의 state를 정의한다.
         this.state ={
           list: ['음악 듣기', '드라마 보기', '코딩 하기'],
         };
       }
        
       // 렌더 함수 안에 리액트 엘리먼트를 넣어준다.
       render(){
         return(
           <div className='App'>
             <h1>내 버킷리스트</h1>
             {/* BucketList 컴포넌트를 넣어준다. */}
             {/* 컴포넌트에 props를 넘겨준다. */}
             {/* <컴포넌트 명  [props 명]={넘겨줄 것(리스트, 문자열, 숫자, ...)} */}
             <BucketList list={this.state.list}/>
           </div>
         );
       }
     }
    
     export default App;

  ```
 
 <br/><br/>
 
  
  
  
  
  
  
  
  
