---
order: 0
title:
  zh-CN: 侧边栏
  en-US: With Sidebar
---

## zh-CN

使用 `renderSidebar` 在面板中添加额外的侧边栏

## en-US

We can customize the rendering of sidebar in the calendar by providing a `renderSidebar` function to `DatePicker`.

```jsx
import { DatePicker, Tag } from 'antd';
import moment from 'moment';

const { RangePicker } = DatePicker;

class DatePickerWithCustomRange extends React.PureComponent {
  state = {
    value: null,
  };

  handleRangePickerChange = value => {
    this.setState({ value });
  };

  renderSidebar = () => (
    <div style={{ padding: 8 }}>
      <Tag
        color="blue"
        onClick={() => {
          this.setState({ value: moment().subtract(1, 'day') });
        }}
      >
        Yesterday
      </Tag>
      <Tag
        color="blue"
        onClick={() => {
          this.setState({ value: moment() });
        }}
      >
        Today
      </Tag>
      <Tag
        color="blue"
        onClick={() => {
          this.setState({ value: moment().add(1, 'day') });
        }}
      >
        Tomorrow
      </Tag>
    </div>
  );

  render() {
    const { value } = this.state;
    return (
      <DatePicker
        value={value}
        onChange={this.handleRangePickerChange}
        renderSidebar={this.renderSidebar}
      />
    );
  }
}

function getLastMomentRange(range, rangeType = 'days') {
  const now = moment();
  return [
    moment(now)
      .subtract(range, rangeType)
      .startOf('day'),
    now,
  ];
}

function getStartOfMomentRange(startOfType = 'day') {
  const now = moment();
  return [moment(now).startOf(startOfType), now];
}

class RangPickerWithCustomRange extends React.PureComponent {
  state = {
    value: [],
  };

  handleRangePickerChange = value => {
    this.setState({ value });
  };

  getLastMomentTagOnClickHandler = (range, rangeType) => {
    return () => {
      this.setState({ value: getLastMomentRange(range, rangeType) });
    };
  };

  getStartOfMomentTagOnClickHandler = startOfType => {
    return () => {
      this.setState({ value: getStartOfMomentRange(startOfType) });
    };
  };

  renderSidebar = () => (
    <div style={{ padding: 8 }}>
      <Tag color="blue" onClick={this.getLastMomentTagOnClickHandler(7, 'day')}>
        Last 7 days
      </Tag>
      <Tag color="blue" onClick={this.getLastMomentTagOnClickHandler(15, 'day')}>
        Last 15 days
      </Tag>
      <Tag color="blue" onClick={this.getLastMomentTagOnClickHandler(30, 'day')}>
        Last 30 days
      </Tag>
      <Tag color="blue" onClick={this.getLastMomentTagOnClickHandler(60, 'day')}>
        Last 60 days
      </Tag>
      <Tag color="blue" onClick={this.getStartOfMomentTagOnClickHandler('week')}>
        This Week
      </Tag>
      <Tag color="blue" onClick={this.getStartOfMomentTagOnClickHandler('month')}>
        This Month
      </Tag>
      <Tag color="blue" onClick={this.getStartOfMomentTagOnClickHandler('year')}>
        This Year
      </Tag>
    </div>
  );

  render() {
    const { value } = this.state;
    return (
      <RangePicker
        value={value}
        onChange={this.handleRangePickerChange}
        renderSidebar={this.renderSidebar}
      />
    );
  }
}

ReactDOM.render(
  <div>
    <DatePickerWithCustomRange />
    <br />
    <RangPickerWithCustomRange />
  </div>,
  mountNode,
);
```
