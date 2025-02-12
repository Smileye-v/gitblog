# [React.FC详细解说](https://github.com/Smileye-v/gitblog/issues/25)

1. `React.FC`是一个函数式组件，是在TypeScript使用一个泛型，FC就是`FunctionComponent`的缩写，事实上`React.FC`可以写成`React.FunctionComponent`

   ```react
   const App: React.FunctionComponent<{ message: string }> = ({ message }) => (
       <div>{ message }</div>
   );
    
   //简写
   interface PropsType{
     message : string;
   }
   const App: React.FC<PropsType> = ({ message }) => ( //{ message }相当于解构赋值，从props中解构
       <div>{ message }</div>
   );
    
   //声明了一个函数组件App   泛型为{message: string}  
   //我能不能这么理解  泛型就是给组件里面使用的参数指定类型 
   ```

2. `React.FC` 包含了 `PropsWithChildren` 的[泛型](https://so.csdn.net/so/search?q=泛型&spm=1001.2101.3001.7020)，不用显式的声明 `props.children` 的类型。`React.FC<>` 对于返回类型是显式的，而普通函数版本是隐式的（否则需要附加注释）。

3. `React.FC`提供了类型检查和自动完成的静态属性：`displayName`，`propTypes`和`defaultProps`（注意：`defaultProps`与`React.FC`结合使用会存在一些[问题](https://github.com/typescript-cheatsheets/react/issues/87)）

4. 我们使用`React.FC`来写 React 组件的时候，是不能用setState的，取而代之的是`useState()`、`useEffect`等 Hook API。

   ```react
   //组件实现实时时间刷新显示
   import React, {useState, useEffect} from 'react'; //引入依赖
   export App: React.FC<{}> = (props) => { //泛型里面有对象{ 属性名 }(解构)  泛型为空对象就直接写props
       const [date, setDate] = useState(new Date());  //useState()括号里面的值给date
       useEffect(() => {
           const timer = setInterval(() => {
               setDate(new Date()); //setDate() 括号里面的值给date   date的值只能通过setDate()设置
           }, 1000)
       }, []);
       return (
           <div>
               <h3>现在时间是</h3>
               <p>{ date.toLocaleTimeString }</p>
           </div>
       )
   }  
   ```

   （1）`const [date, setDate] = useState(new Date());`

   （2）useState很简单，就相当于class函数式组件中的state，useState(值)，其中的值表示初始化值，date表示接收值，setDate表示设置值

   （3）可以把 useEffect Hook 看做componentDidMount(组件挂载完成) componentDidUpdate(组件更新完成) 和 componentWillUnmount(组件销毁调用) 这三个函数的组合

   （4）useEffect最后[]中括号中的参数表示当此参数更新时，其中的方法再次执行一遍，如果没有参数，则是空。

   （5）useEffect里的return表示组件卸载的时候执行的动作

   （6）useEffect会在组件加载完成以后，执行一次，所以有第一条中，其可以控制三个生命周期

   （7）如果没有后面的参数，甚至没有[]，即useEffect(()=>{}),这种情况下，每当页面中useState值发生变化，useEffect中的代码就会执行一次，这是不可取的！
