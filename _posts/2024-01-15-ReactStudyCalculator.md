---
layout: post
categories: blog
title: useState를 활용한 계산기 만들기
tags: [React, 프론트엔드]
date: 2024-01-15
---

리액트 스터디 첫날 useState에 대해 설명을 들으며 공부를 하고 과제로 useState를 활용한 계산기 기능 만들기를 과제로 받았다...   
처음 과제를 받고 진행을 했을때 어떻게 구성해야할지랑 어떤식으로 작성해야할지 활용해야할지에 대한 여러 생각들이 들었다   

먼저 상태변수 구성을 어떻게 할지 생각을 하다가 일단 계산기에서 쓸만한게 현재값,이전값,연산값 이 필요한거 같아서 Value,oldValue,operator로 변수를 구성해줬다.   

```js
  const [Value, setValue] = useState(0);
  const [OldValue, setOldValue] = useState(0);
  const [operator, setOperator] = useState(0);
```

그 다음 값을 입력 받기 위해 inputValue의 이름으로 함수를 지정해줬다.   
만약 값이 0이면 현재 입력받은 값을 저장하고 이미 값이 입력되어있으면 그 값 뒤에 저장을 했다.   
```js
  const inputValue = (e) => {
    let input = e.target.value;
    if (Value === 0) {
      setValue(input);
    } else {
      setValue(Value + input);
    }
  }
```

AC 기능을 위해 clear함수로 Value값을 초기화 해주고 퍼센트 함수로 현재 값 나누기 100을 해줬다.   
그리고 +/-기능을 위해 changeSign 함수로 현재 값이 양수면 -을 통해 음수로 바꾸고 만약 음수라면 Math.abs함수를 통해 양수로 변환해줬다.   
```js
  const clear = () => {
    setValue(0);
  }

  const percent = (e) => {
    setValue(Value / 100);
  }

  const changeSign = () => {
    if (Value > 0) {
      setValue(-Value);
    } else {
      setValue(Math.abs(Value));
    }
  }
```

연산자를 입력받기 위해 operatorHandle이름의 함수로 연산자가 입력되면 현재값을 이전값으로 넘겨주고 현재값을 0으로 초기화하는 작업을 해줬다.   
```js
  const operatorHandle = (e) => {
    let operatorInput = e.target.value;
    setOperator(operatorInput);
    setOldValue(Value);
    setValue(0);
  }
```
계산식   
```js
  const calculate = () => {
    if (operator === "/") {
      setValue(parseFloat(OldValue) / parseFloat(Value));
    } else if (operator === "X") {
      setValue(parseFloat(OldValue) * parseFloat(Value));
    } else if (operator === "-") {
      setValue(parseFloat(OldValue) - parseFloat(Value));
    } else if (operator === "+") {
      setValue(parseFloat(OldValue) + parseFloat(Value));
    }
  }
```

html 구성
```js
    <div className="CalculatorArea">
      <div className={styles.container}>
        <div className={styles.wrapper}>
          <div className="Display">
            <h1 className={styles.result}>{Value}</h1>
          </div>
          <div className={styles.btn_container}>
            <button className={styles.gary} onClick={clear}>AC</button>
            <button className={styles.gary} onClick={changeSign}>+/-</button>
            <button className={styles.gary} onClick={percent}>%</button>
            <button className={styles.orange} onClick={operatorHandle} value={'/'}>÷</button>
            <button className={styles.deepgray} onClick={inputValue} value={7}>7</button>
            <button className={styles.deepgray} onClick={inputValue} value={8}>8</button>
            <button className={styles.deepgray} onClick={inputValue} value={9}>9</button>
            <button className={styles.orange} onClick={operatorHandle} value={'X'}>X</button>
            <button className={styles.deepgray} onClick={inputValue} value={4}>4</button>
            <button className={styles.deepgray} onClick={inputValue} value={5}>5</button>
            <button className={styles.deepgray} onClick={inputValue} value={6}>6</button>
            <button className={styles.orange} onClick={operatorHandle} value={'-'}>-</button>
            <button className={styles.deepgray} onClick={inputValue} value={1}>1</button>
            <button className={styles.deepgray} onClick={inputValue} value={2}>2</button>
            <button className={styles.deepgray} onClick={inputValue} value={3}>3</button>
            <button className={styles.orange} onClick={operatorHandle} value={'+'}>+</button>
            <button className={styles.zero} onClick={inputValue} value={0}>0</button>
            <button className={styles.deepgray} onClick={inputValue} value={"."}>.</button>
            <button className={styles.orange} onClick={calculate}>=</button>
          </div>
        </div>
      </div>
    </div>
```

최종 코드
```js
import react, { useState } from 'react';
import styles from './Calculator.module.css'

const Calculator_hard = () => {
  const [Value, setValue] = useState(0);
  const [OldValue, setOldValue] = useState(0);
  const [operator, setOperator] = useState(0);

  const inputValue = (e) => {
    let input = e.target.value;
    if (Value === 0) {
      setValue(input);
    } else {
      setValue(Value + input);
    }
  }

  const clear = () => {
    setValue(0);
  }

  const percent = (e) => {
    setValue(Value / 100);
  }

  const changeSign = () => {
    if (Value > 0) {
      setValue(-Value);
    } else {
      setValue(Math.abs(Value));
    }
  }

  const operatorHandle = (e) => {
    let operatorInput = e.target.value;
    setOperator(operatorInput);
    setOldValue(Value);
    setValue(0);
  }

  const calculate = () => {
    if (operator === "/") {
      setValue(parseFloat(OldValue) / parseFloat(Value));
    } else if (operator === "X") {
      setValue(parseFloat(OldValue) * parseFloat(Value));
    } else if (operator === "-") {
      setValue(parseFloat(OldValue) - parseFloat(Value));
    } else if (operator === "+") {
      setValue(parseFloat(OldValue) + parseFloat(Value));
    }
  }

  return (
    <div className="CalculatorArea">
      <div className={styles.container}>
        <div className={styles.wrapper}>
          <div className="Display">
            <h1 className={styles.result}>{Value}</h1>
          </div>
          <div className={styles.btn_container}>
            <button className={styles.gary} onClick={clear}>AC</button>
            <button className={styles.gary} onClick={changeSign}>+/-</button>
            <button className={styles.gary} onClick={percent}>%</button>
            <button className={styles.orange} onClick={operatorHandle} value={'/'}>÷</button>
            <button className={styles.deepgray} onClick={inputValue} value={7}>7</button>
            <button className={styles.deepgray} onClick={inputValue} value={8}>8</button>
            <button className={styles.deepgray} onClick={inputValue} value={9}>9</button>
            <button className={styles.orange} onClick={operatorHandle} value={'X'}>X</button>
            <button className={styles.deepgray} onClick={inputValue} value={4}>4</button>
            <button className={styles.deepgray} onClick={inputValue} value={5}>5</button>
            <button className={styles.deepgray} onClick={inputValue} value={6}>6</button>
            <button className={styles.orange} onClick={operatorHandle} value={'-'}>-</button>
            <button className={styles.deepgray} onClick={inputValue} value={1}>1</button>
            <button className={styles.deepgray} onClick={inputValue} value={2}>2</button>
            <button className={styles.deepgray} onClick={inputValue} value={3}>3</button>
            <button className={styles.orange} onClick={operatorHandle} value={'+'}>+</button>
            <button className={styles.zero} onClick={inputValue} value={0}>0</button>
            <button className={styles.deepgray} onClick={inputValue} value={"."}>.</button>
            <button className={styles.orange} onClick={calculate}>=</button>
          </div>
        </div>
      </div>
    </div>
  );
};

export default Calculator_hard;
```

여러 문서를 보면서 만들었지만 지금 돌아보면 그렇게 어렵지 않았는데 처음 시작할때는 어떻게 계산시키고 어떻게 구성할지에 대해서 하나도 모르겠어서 좀 어려웠던 것 같다...   