# Mark selection text content

使用 javascript 實現對選取的文字加入 html 的 tag

[Try it](https://jsfiddle.net/gr1a6bhw/)

```javascript
const clickEvent = () => {
  let selection = window.getSelection();
  let parent = selection.anchorNode.parentElement;
  let parentNode = selection.anchorNode.parentNode;
  let selectionText = selection.toString();
  let containMark = false;
  if (parent.nodeName === "MARK") {
    let grandParent = parent.parentElement;
    parent.replaceWith(document.createTextNode(parent.textContent || ""));
    grandParent.normalize();
    return;
  } else {
    let childNodes = parentNode.childNodes;
    for (let i = 0; i < childNodes.length; i++) {
      if (
        childNodes[i].nodeName === "MARK" &&
        selection.containsNode(childNodes[i], true)
      ) {
        containMark = true;
        childNodes[i].replaceWith(
          document.createTextNode(childNodes[i].textContent || "")
        );
        parentNode.normalize();
        break;
      }
    }
  }
  if (containMark) return;

  let mark = document.createElement("mark");

  mark.textContent = selectionText;

  let range = selection.getRangeAt(0);
  range.deleteContents();
  range.insertNode(mark);
};
```

# 參考

- [Selection - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Selection)
- [javascript - How to check if selected text in html already has a class? - Stack Overflow](https://stackoverflow.com/questions/45909416/how-to-check-if-selected-text-in-html-already-has-a-class)
