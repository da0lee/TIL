# 💻 InputOperateHours component

<br/>

> src > components > form > InputOperateHours.js

<br/>

- Q ) 영업시간 선택 selectInput
- A ) 


<br/>

```js
import React, { useState, useEffect, useMemo } from 'react';
import styled from 'styled-components';

import { timeSelect } from '../../utils/helper';
import { InputSelect } from '.';

const initialValue = {
  day: '월요일',
  start: '0시 00분',
  end: '0시 00분',
};

const InputOperateHours = ({ value, setInputs, error, setErrors }) => {
  const [time, setTime] = useState(initialValue);
  const dayOptions = useMemo(() => ['월요일', '화요일', '수요일', '목요일', '금요일', '토요일', '일요일'], []);
  const startTimeOptions = useMemo(() => timeSelect(), []);
  const endTimeOptions = useMemo(() => timeSelect(time.start), [time.start]);

  const handleChange = (e) => {
    const { name, value } = e.target;
    setTime({
      ...time,
      [name]: value,
    });
  };

  const handleClick = () => {
    const { day, start, end } = time;

    // indexOf : 
    // 0, 1, 2, 3 ... : 배열에서 찾은 지정된 요소의 index
    // -1 :  배열에서 지정된 요소를 찾을 수 없다.
    const checkDay = value.filter((item) => item.indexOf(day) > -1);

    // value.length <= 6 : 토요일 일 때까지만 click event가 일어나는 조건. (value.length가 7일때는 이미 일요일이 추가되었기 때문에 더이상 click이 발생하면 안된다.
    // checkDay.length === 0 : 월요일이 이미 추가되어있으면 또 추가되지 않는다.
    if (value.length <= 6 && checkDay.length === 0) {
      const result = `${day} ${start} - ${end}`;
      setInputs((state) => ({
        ...state,
        operatingHours: [...state.operatingHours, result],
      }));

      setErrors((state) => ({ ...state, operatingHours: '' }));

      setTime({
        ...initialValue,
        day: dayOptions[value.length + 1] ? dayOptions[value.length + 1] : '일요일',
      });
    }
  };

  const handleClickDelete = (deleteItem) => {
    setInputs((state) => {
      return {
        ...state,
        operatingHours: state.operatingHours.filter((item) => item !== deleteItem),
      };
    });
  };

  useEffect(() => {
    setTime({
      ...initialValue,
      day: dayOptions[value.length] ? dayOptions[value.length] : '일요일',
    });
  }, [setTime, value, dayOptions]);

  return (
    <Wrap className="wrap">
      <label>운영시간</label>
      <FormRow>
        <div className="col">
          <InputSelect name="day" value={time.day} onChange={handleChange} options={dayOptions} />
        </div>
        <div className="col">
          <InputSelect name="start" value={time.start} onChange={handleChange} options={startTimeOptions} />
        </div>
        <div className="col">
          <InputSelect name="end" value={time.end} onChange={handleChange} options={endTimeOptions} />
        </div>
        <button type="button" className="btn-add" onClick={handleClick} />
      </FormRow>
      <p className={error ? 'err on' : 'err'}>{error}</p>
      {value.map((operatingHour, idx) => (
        <Card key={idx}>
          {operatingHour}
          <button type="button" className="btn-delete" onClick={() => handleClickDelete(operatingHour)} />
        </Card>
      ))}
    </Wrap>
  );
};

export default InputOperateHours;

```