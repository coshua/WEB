Consider the following codes.
```javascript
class Table extends React.Component {
  render() {
    return (
      <table>
        <tr>
          <Columns />
        </tr>
      </table>
    );
  }
}

class Columns extends React.Component {
  render() {
    return (
      <div>
        <td>Hello</td>
        <td>World</td>
      </div>
    );
  }
}
```
Results
```html
<table>
  <tr>
    <div>
      <td>Hello</td>
      <td>World</td>
    </div>
  </tr>
</table>
```
In `<tr>` tags, `<td>` should be places in order for the rendered HTML to be valid. 
However, we also know the returned result from one component should be wrapped into the parent element, like `<div>`.

Fragments solve this problem.

### Fragments
Fragments let you group a list of children without adding extra nodes to the DOM.
```javascript
class Columns extends React.Component {
  render() {
    return (
      <React.Fragment>
        <td>Hello</td>
        <td>World</td>
      </React.Fragment>
    );
  }
}
```

### Short Syntax
Sometimes it feels tedious to import or type fragments. So you use `<></>` instead of those. It looks like empty tags and neither makes extra node.

The only difference is that <React.Fragment> could have keys. It is the only attribute it could have. It is useful when mapping a collection to an array of fragments.
