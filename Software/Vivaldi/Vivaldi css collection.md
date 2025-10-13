# Vivaldi css collection

## Vertical tab open on hover

Original Link : https://gist.github.com/tiwari-shaswat7/87b082ef5bb10b8ef27a959b6ce77c29

```css
/* Expanding Left Tabs */

/* Animate the tabs, set initial width. */
#tabs-tabbar-container.left {
  width: inherit !important;
}

.tabbar-wrapper {
  position: absolute !important;
  z-index: 200 !important;
  height: 100% !important;
  transition: all 250ms ease !important;
  width: 32px;
}

.tabbar-wrapper:hover {
  width: 250px !important;
}

#webview-container {
  margin-left: 32px;
}

@media all and (display-mode: fullscreen) {
  /* For full screen inside element like youtube, facebook videos */
  .inner > #main > .inner > #webview-container {
    margin-left: 0 !important;
  }
}

/* Shunt the status info (text on hover) over to accomodate tabs */
#webview-container ~ .StatusInfo {
  left: 36px !important;
}

.button-popup[aria-label="Workspaces"] {
  z-index: 300 !important;
}

.tabbar-workspace-button {
  width: inherit !important;
}

/* To hide workspace extra text and dropdown chevron */
.tabbar-wrapper > .tabbar-workspace-button > .ToolbarButton-Button {
  justify-content: flex-start !important;
  overflow: hidden;
}
```
