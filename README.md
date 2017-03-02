<div align="center" style="margin-bottom: 30px;">
<img src="https://cloud.githubusercontent.com/assets/1416436/23387281/9a628ec4-fd29-11e6-9a1a-09f755c21a14.png" width="224"/>
</div>

# react-tiny-virtual-list
> A tiny but mighty 3kb list virtualization component, with zero dependencies 💪

[![npm version](https://img.shields.io/npm/v/react-tiny-virtual-list.svg)](https://www.npmjs.com/package/react-tiny-virtual-list)
[![license](https://img.shields.io/github/license/mashape/apistatus.svg?maxAge=2592000)](https://github.com/clauderic/react-tiny-virtual-list/blob/master/LICENSE)
[![Gitter](https://badges.gitter.im/clauderic/react-tiny-virtual-list.svg)](https://gitter.im/clauderic/react-tiny-virtual-list)

* **Tiny & dependency free** – Only 3kb gzipped
* **Render millions of items**, without breaking a sweat
* **Scroll to index** or **set the initial scroll offset**
* **Supports fixed** or **variable** heights/widths
* **Vertical** or **Horizontal** lists

Getting Started
---------------

Using [npm](https://www.npmjs.com/):
```
npm install react-tiny-virtual-list --save
```

ES6, CommonJS, and UMD builds are available with each distribution. For example:
```js
import VirtualList from 'react-tiny-virtual-list';
```

You can also use a global-friendly UMD build:
```html
<script src="react-tiny-virtual-list/umd/react-tiny-virtual-list.js"></script>
<script>
var VirtualList = window.VirtualList.default;
...
</script>
```

Example usage
-------------

```js
import React from 'react';
import {render} from 'react-dom';
import VirtualList from 'react-tiny-virtual-list';

const data = ['A', 'B', 'C', 'D', 'E', 'F', ...];

render(
  <VirtualList
    width='100%'
    height={600}
    itemCount={data.length}
    itemSize={50} // Also supports variable heights (array or function getter)
    renderItem={({index, style}) =>
      <div key={index} style={style}> // The style property contains the item's absolute position
        Letter: {data[index]}, Row: #{index}
      </div>
    }
  />,
  document.getElementById('root')
);
```

### Prop Types
| Property          | Type              | Required? | Description                                                                                                                                                                                                                |
|:------------------|:------------------|:----------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| width             | Number or String* | ✓         | Width of List. This property will determine the number of rendered items when scrollDirection is `'horizontal'`.                                                                                                           |
| height            | Number or String* | ✓         | Height of List; This property will determine the number of rendered items when scrollDirection is `'vertical'`.                                                                                                            |
| itemCount         | Number            | ✓         | The number of items you want to render                                                                                                                                                                                     |
| renderItem        | Function          | ✓         | Responsible for rendering an item given it's index: `({index: number, style: Object}): React.PropTypes.node`. The returned element must handle key and style.                                                              |
| itemSize          |                   | ✓         | Either a fixed height/width (depending on the scrollDirection), an array containing the heights of all the items in your list, or a function that returns the height of an item given its index: `(index: number): number` |
| scrollDirection   | String            |           | Whether the list should scroll vertically or horizontally. One of `'vertical'` or `'horizontal'`. Defaults to `'vertical'`                                                                                                 |
| scrollOffset      | Number            |           | Can be used to control the scroll offset; Also useful for setting an initial scroll offset                                                                                                                                 |
| scrollToIndex     | Number            |           | Item index to scroll to (by forcefully scrolling if necessary)                                                                                                                                                             |
| scrollToAlignment |                   |           | Used in combination with `scrollToIndex`, this prop controls the alignment of the scrolled to item. One of: 'start', 'center' or 'end'                                                                                     |
| overscanCount     | Number            |           | Number of extra buffer items to render above/below the visible items. Tweaking this can help reduce scroll flickering on certain browsers/devices.                                                                         |
| estimatedItemSize | Number            |           | Used to estimate the total size of the list before all of its items have actually been measured. The estimated total height is progressively adjusted as items are rendered.                                               |
*\* Width may only be a string when `scrollDirection` is `'vertical'`. Similarly, Height may only be a string if `scrollDirection` is `'horizontal'`*

### Public Methods

#### recomputeSizes (index: number)
This method force recomputes the item sizes after the specificed index (these are normally cached).

`VirtualList` has no way of knowing when its underlying data has changed, since it only receives a rowHeight property. If the rowHeight is a `number`, this isn't an issue, as it can compare before and after values and automatically call `recomputeSizes` internally.
 However, if you're passing a function to `itemSize`, that type of comparison is error prone. In that event, you'll need to call `recomputeSizes` manually to inform the `VirtualList` that the size of it's items has changed.

## Reporting Issues
Found an issue? Please [report it](https://github.com/clauderic/react-tiny-virtual-list/issues) along with any relevant details to reproduce it.

## Contributions
Feature requests / pull requests are welcome, though please take a moment to make sure your contributions fits within the scope of the project. [Learn how to contribute](https://github.com/clauderic/react-tiny-virtual-list/blob/master/CONTRIBUTING.md)

## Acknowledgments
This library draws inspiration from [react-virtualized](https://github.com/bvaughn/react-virtualized), and is meant as a bare-minimum replacement for the [List](https://github.com/bvaughn/react-virtualized/blob/master/docs/List.md) component. If you're looking for a tiny, lightweight and dependency-free list virtualization library that supports variable heights, you're in the right place! If you're looking for something that supports more use-cases, I highly encourage you to check out [react-virtualized](https://github.com/bvaughn/react-virtualized) instead, it's a fantastic library ❤️

## License
react-tiny-virtual-list is available under the MIT License.