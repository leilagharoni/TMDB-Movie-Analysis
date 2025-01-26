<!DOCTYPE html>

<html lang="en">
<head><meta charset="utf-8"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Investigate_a_Dataset</title><script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<style type="text/css">
    pre { line-height: 125%; }
td.linenos .normal { color: inherit; background-color: transparent; padding-left: 5px; padding-right: 5px; }
span.linenos { color: inherit; background-color: transparent; padding-left: 5px; padding-right: 5px; }
td.linenos .special { color: #000000; background-color: #ffffc0; padding-left: 5px; padding-right: 5px; }
span.linenos.special { color: #000000; background-color: #ffffc0; padding-left: 5px; padding-right: 5px; }
.highlight .hll { background-color: var(--jp-cell-editor-active-background) }
.highlight { background: var(--jp-cell-editor-background); color: var(--jp-mirror-editor-variable-color) }
.highlight .c { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment */
.highlight .err { color: var(--jp-mirror-editor-error-color) } /* Error */
.highlight .k { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword */
.highlight .o { color: var(--jp-mirror-editor-operator-color); font-weight: bold } /* Operator */
.highlight .p { color: var(--jp-mirror-editor-punctuation-color) } /* Punctuation */
.highlight .ch { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Multiline */
.highlight .cp { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Preproc */
.highlight .cpf { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Single */
.highlight .cs { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Special */
.highlight .kc { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Pseudo */
.highlight .kr { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Type */
.highlight .m { color: var(--jp-mirror-editor-number-color) } /* Literal.Number */
.highlight .s { color: var(--jp-mirror-editor-string-color) } /* Literal.String */
.highlight .ow { color: var(--jp-mirror-editor-operator-color); font-weight: bold } /* Operator.Word */
.highlight .pm { color: var(--jp-mirror-editor-punctuation-color) } /* Punctuation.Marker */
.highlight .w { color: var(--jp-mirror-editor-variable-color) } /* Text.Whitespace */
.highlight .mb { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Bin */
.highlight .mf { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Float */
.highlight .mh { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Hex */
.highlight .mi { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Integer */
.highlight .mo { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Oct */
.highlight .sa { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Affix */
.highlight .sb { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Backtick */
.highlight .sc { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Char */
.highlight .dl { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Delimiter */
.highlight .sd { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Doc */
.highlight .s2 { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Double */
.highlight .se { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Escape */
.highlight .sh { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Heredoc */
.highlight .si { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Interpol */
.highlight .sx { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Other */
.highlight .sr { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Regex */
.highlight .s1 { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Single */
.highlight .ss { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Symbol */
.highlight .il { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Integer.Long */
  </style>
<style type="text/css">
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*
 * Mozilla scrollbar styling
 */

/* use standard opaque scrollbars for most nodes */
[data-jp-theme-scrollbars='true'] {
  scrollbar-color: rgb(var(--jp-scrollbar-thumb-color))
    var(--jp-scrollbar-background-color);
}

/* for code nodes, use a transparent style of scrollbar. These selectors
 * will match lower in the tree, and so will override the above */
[data-jp-theme-scrollbars='true'] .CodeMirror-hscrollbar,
[data-jp-theme-scrollbars='true'] .CodeMirror-vscrollbar {
  scrollbar-color: rgba(var(--jp-scrollbar-thumb-color), 0.5) transparent;
}

/* tiny scrollbar */

.jp-scrollbar-tiny {
  scrollbar-color: rgba(var(--jp-scrollbar-thumb-color), 0.5) transparent;
  scrollbar-width: thin;
}

/* tiny scrollbar */

.jp-scrollbar-tiny::-webkit-scrollbar,
.jp-scrollbar-tiny::-webkit-scrollbar-corner {
  background-color: transparent;
  height: 4px;
  width: 4px;
}

.jp-scrollbar-tiny::-webkit-scrollbar-thumb {
  background: rgba(var(--jp-scrollbar-thumb-color), 0.5);
}

.jp-scrollbar-tiny::-webkit-scrollbar-track:horizontal {
  border-left: 0 solid transparent;
  border-right: 0 solid transparent;
}

.jp-scrollbar-tiny::-webkit-scrollbar-track:vertical {
  border-top: 0 solid transparent;
  border-bottom: 0 solid transparent;
}

/*
 * Lumino
 */

.lm-ScrollBar[data-orientation='horizontal'] {
  min-height: 16px;
  max-height: 16px;
  min-width: 45px;
  border-top: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='vertical'] {
  min-width: 16px;
  max-width: 16px;
  min-height: 45px;
  border-left: 1px solid #a0a0a0;
}

.lm-ScrollBar-button {
  background-color: #f0f0f0;
  background-position: center center;
  min-height: 15px;
  max-height: 15px;
  min-width: 15px;
  max-width: 15px;
}

.lm-ScrollBar-button:hover {
  background-color: #dadada;
}

.lm-ScrollBar-button.lm-mod-active {
  background-color: #cdcdcd;
}

.lm-ScrollBar-track {
  background: #f0f0f0;
}

.lm-ScrollBar-thumb {
  background: #cdcdcd;
}

.lm-ScrollBar-thumb:hover {
  background: #bababa;
}

.lm-ScrollBar-thumb.lm-mod-active {
  background: #a0a0a0;
}

.lm-ScrollBar[data-orientation='horizontal'] .lm-ScrollBar-thumb {
  height: 100%;
  min-width: 15px;
  border-left: 1px solid #a0a0a0;
  border-right: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='vertical'] .lm-ScrollBar-thumb {
  width: 100%;
  min-height: 15px;
  border-top: 1px solid #a0a0a0;
  border-bottom: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='horizontal']
  .lm-ScrollBar-button[data-action='decrement'] {
  background-image: var(--jp-icon-caret-left);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='horizontal']
  .lm-ScrollBar-button[data-action='increment'] {
  background-image: var(--jp-icon-caret-right);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='vertical']
  .lm-ScrollBar-button[data-action='decrement'] {
  background-image: var(--jp-icon-caret-up);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='vertical']
  .lm-ScrollBar-button[data-action='increment'] {
  background-image: var(--jp-icon-caret-down);
  background-size: 17px;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-Widget {
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
}

.lm-Widget.lm-mod-hidden {
  display: none !important;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.lm-AccordionPanel[data-orientation='horizontal'] > .lm-AccordionPanel-title {
  /* Title is rotated for horizontal accordion panel using CSS */
  display: block;
  transform-origin: top left;
  transform: rotate(-90deg) translate(-100%);
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-CommandPalette {
  display: flex;
  flex-direction: column;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-CommandPalette-search {
  flex: 0 0 auto;
}

.lm-CommandPalette-content {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  min-height: 0;
  overflow: auto;
  list-style-type: none;
}

.lm-CommandPalette-header {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.lm-CommandPalette-item {
  display: flex;
  flex-direction: row;
}

.lm-CommandPalette-itemIcon {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemContent {
  flex: 1 1 auto;
  overflow: hidden;
}

.lm-CommandPalette-itemShortcut {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemLabel {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.lm-close-icon {
  border: 1px solid transparent;
  background-color: transparent;
  position: absolute;
  z-index: 1;
  right: 3%;
  top: 0;
  bottom: 0;
  margin: auto;
  padding: 7px 0;
  display: none;
  vertical-align: middle;
  outline: 0;
  cursor: pointer;
}
.lm-close-icon:after {
  content: 'X';
  display: block;
  width: 15px;
  height: 15px;
  text-align: center;
  color: #000;
  font-weight: normal;
  font-size: 12px;
  cursor: pointer;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-DockPanel {
  z-index: 0;
}

.lm-DockPanel-widget {
  z-index: 0;
}

.lm-DockPanel-tabBar {
  z-index: 1;
}

.lm-DockPanel-handle {
  z-index: 2;
}

.lm-DockPanel-handle.lm-mod-hidden {
  display: none !important;
}

.lm-DockPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}

.lm-DockPanel-handle[data-orientation='horizontal'] {
  cursor: ew-resize;
}

.lm-DockPanel-handle[data-orientation='vertical'] {
  cursor: ns-resize;
}

.lm-DockPanel-handle[data-orientation='horizontal']:after {
  left: 50%;
  min-width: 8px;
  transform: translateX(-50%);
}

.lm-DockPanel-handle[data-orientation='vertical']:after {
  top: 50%;
  min-height: 8px;
  transform: translateY(-50%);
}

.lm-DockPanel-overlay {
  z-index: 3;
  box-sizing: border-box;
  pointer-events: none;
}

.lm-DockPanel-overlay.lm-mod-hidden {
  display: none !important;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-Menu {
  z-index: 10000;
  position: absolute;
  white-space: nowrap;
  overflow-x: hidden;
  overflow-y: auto;
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-Menu-content {
  margin: 0;
  padding: 0;
  display: table;
  list-style-type: none;
}

.lm-Menu-item {
  display: table-row;
}

.lm-Menu-item.lm-mod-hidden,
.lm-Menu-item.lm-mod-collapsed {
  display: none !important;
}

.lm-Menu-itemIcon,
.lm-Menu-itemSubmenuIcon {
  display: table-cell;
  text-align: center;
}

.lm-Menu-itemLabel {
  display: table-cell;
  text-align: left;
}

.lm-Menu-itemShortcut {
  display: table-cell;
  text-align: right;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-MenuBar {
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-MenuBar-content {
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: row;
  list-style-type: none;
}

.lm-MenuBar-item {
  box-sizing: border-box;
}

.lm-MenuBar-itemIcon,
.lm-MenuBar-itemLabel {
  display: inline-block;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-ScrollBar {
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-ScrollBar[data-orientation='horizontal'] {
  flex-direction: row;
}

.lm-ScrollBar[data-orientation='vertical'] {
  flex-direction: column;
}

.lm-ScrollBar-button {
  box-sizing: border-box;
  flex: 0 0 auto;
}

.lm-ScrollBar-track {
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
  flex: 1 1 auto;
}

.lm-ScrollBar-thumb {
  box-sizing: border-box;
  position: absolute;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-SplitPanel-child {
  z-index: 0;
}

.lm-SplitPanel-handle {
  z-index: 1;
}

.lm-SplitPanel-handle.lm-mod-hidden {
  display: none !important;
}

.lm-SplitPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}

.lm-SplitPanel[data-orientation='horizontal'] > .lm-SplitPanel-handle {
  cursor: ew-resize;
}

.lm-SplitPanel[data-orientation='vertical'] > .lm-SplitPanel-handle {
  cursor: ns-resize;
}

.lm-SplitPanel[data-orientation='horizontal'] > .lm-SplitPanel-handle:after {
  left: 50%;
  min-width: 8px;
  transform: translateX(-50%);
}

.lm-SplitPanel[data-orientation='vertical'] > .lm-SplitPanel-handle:after {
  top: 50%;
  min-height: 8px;
  transform: translateY(-50%);
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-TabBar {
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.lm-TabBar[data-orientation='horizontal'] {
  flex-direction: row;
  align-items: flex-end;
}

.lm-TabBar[data-orientation='vertical'] {
  flex-direction: column;
  align-items: flex-end;
}

.lm-TabBar-content {
  margin: 0;
  padding: 0;
  display: flex;
  flex: 1 1 auto;
  list-style-type: none;
}

.lm-TabBar[data-orientation='horizontal'] > .lm-TabBar-content {
  flex-direction: row;
}

.lm-TabBar[data-orientation='vertical'] > .lm-TabBar-content {
  flex-direction: column;
}

.lm-TabBar-tab {
  display: flex;
  flex-direction: row;
  box-sizing: border-box;
  overflow: hidden;
  touch-action: none; /* Disable native Drag/Drop */
}

.lm-TabBar-tabIcon,
.lm-TabBar-tabCloseIcon {
  flex: 0 0 auto;
}

.lm-TabBar-tabLabel {
  flex: 1 1 auto;
  overflow: hidden;
  white-space: nowrap;
}

.lm-TabBar-tabInput {
  user-select: all;
  width: 100%;
  box-sizing: border-box;
}

.lm-TabBar-tab.lm-mod-hidden {
  display: none !important;
}

.lm-TabBar-addButton.lm-mod-hidden {
  display: none !important;
}

.lm-TabBar.lm-mod-dragging .lm-TabBar-tab {
  position: relative;
}

.lm-TabBar.lm-mod-dragging[data-orientation='horizontal'] .lm-TabBar-tab {
  left: 0;
  transition: left 150ms ease;
}

.lm-TabBar.lm-mod-dragging[data-orientation='vertical'] .lm-TabBar-tab {
  top: 0;
  transition: top 150ms ease;
}

.lm-TabBar.lm-mod-dragging .lm-TabBar-tab.lm-mod-dragging {
  transition: none;
}

.lm-TabBar-tabLabel .lm-TabBar-tabInput {
  user-select: all;
  width: 100%;
  box-sizing: border-box;
  background: inherit;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-TabPanel-tabBar {
  z-index: 1;
}

.lm-TabPanel-stackedPanel {
  z-index: 0;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Collapse {
  display: flex;
  flex-direction: column;
  align-items: stretch;
}

.jp-Collapse-header {
  padding: 1px 12px;
  background-color: var(--jp-layout-color1);
  border-bottom: solid var(--jp-border-width) var(--jp-border-color2);
  color: var(--jp-ui-font-color1);
  cursor: pointer;
  display: flex;
  align-items: center;
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  text-transform: uppercase;
  user-select: none;
}

.jp-Collapser-icon {
  height: 16px;
}

.jp-Collapse-header-collapsed .jp-Collapser-icon {
  transform: rotate(-90deg);
  margin: auto 0;
}

.jp-Collapser-title {
  line-height: 25px;
}

.jp-Collapse-contents {
  padding: 0 12px;
  background-color: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  overflow: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensureUiComponents() in @jupyterlab/buildutils */

/**
 * (DEPRECATED) Support for consuming icons as CSS background images
 */

/* Icons urls */

:root {
  --jp-icon-add-above: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPGcgY2xpcC1wYXRoPSJ1cmwoI2NsaXAwXzEzN18xOTQ5MikiPgo8cGF0aCBjbGFzcz0ianAtaWNvbjMiIGQ9Ik00Ljc1IDQuOTMwNjZINi42MjVWNi44MDU2NkM2LjYyNSA3LjAxMTkxIDYuNzkzNzUgNy4xODA2NiA3IDcuMTgwNjZDNy4yMDYyNSA3LjE4MDY2IDcuMzc1IDcuMDExOTEgNy4zNzUgNi44MDU2NlY0LjkzMDY2SDkuMjVDOS40NTYyNSA0LjkzMDY2IDkuNjI1IDQuNzYxOTEgOS42MjUgNC41NTU2NkM5LjYyNSA0LjM0OTQxIDkuNDU2MjUgNC4xODA2NiA5LjI1IDQuMTgwNjZINy4zNzVWMi4zMDU2NkM3LjM3NSAyLjA5OTQxIDcuMjA2MjUgMS45MzA2NiA3IDEuOTMwNjZDNi43OTM3NSAxLjkzMDY2IDYuNjI1IDIuMDk5NDEgNi42MjUgMi4zMDU2NlY0LjE4MDY2SDQuNzVDNC41NDM3NSA0LjE4MDY2IDQuMzc1IDQuMzQ5NDEgNC4zNzUgNC41NTU2NkM0LjM3NSA0Ljc2MTkxIDQuNTQzNzUgNC45MzA2NiA0Ljc1IDQuOTMwNjZaIiBmaWxsPSIjNjE2MTYxIiBzdHJva2U9IiM2MTYxNjEiIHN0cm9rZS13aWR0aD0iMC43Ii8+CjwvZz4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTExLjUgOS41VjExLjVMMi41IDExLjVWOS41TDExLjUgOS41Wk0xMiA4QzEyLjU1MjMgOCAxMyA4LjQ0NzcyIDEzIDlWMTJDMTMgMTIuNTUyMyAxMi41NTIzIDEzIDEyIDEzTDIgMTNDMS40NDc3MiAxMyAxIDEyLjU1MjMgMSAxMlY5QzEgOC40NDc3MiAxLjQ0NzcxIDggMiA4TDEyIDhaIiBmaWxsPSIjNjE2MTYxIi8+CjxkZWZzPgo8Y2xpcFBhdGggaWQ9ImNsaXAwXzEzN18xOTQ5MiI+CjxyZWN0IGNsYXNzPSJqcC1pY29uMyIgd2lkdGg9IjYiIGhlaWdodD0iNiIgZmlsbD0id2hpdGUiIHRyYW5zZm9ybT0ibWF0cml4KC0xIDAgMCAxIDEwIDEuNTU1NjYpIi8+CjwvY2xpcFBhdGg+CjwvZGVmcz4KPC9zdmc+Cg==);
  --jp-icon-add-below: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPGcgY2xpcC1wYXRoPSJ1cmwoI2NsaXAwXzEzN18xOTQ5OCkiPgo8cGF0aCBjbGFzcz0ianAtaWNvbjMiIGQ9Ik05LjI1IDEwLjA2OTNMNy4zNzUgMTAuMDY5M0w3LjM3NSA4LjE5NDM0QzcuMzc1IDcuOTg4MDkgNy4yMDYyNSA3LjgxOTM0IDcgNy44MTkzNEM2Ljc5Mzc1IDcuODE5MzQgNi42MjUgNy45ODgwOSA2LjYyNSA4LjE5NDM0TDYuNjI1IDEwLjA2OTNMNC43NSAxMC4wNjkzQzQuNTQzNzUgMTAuMDY5MyA0LjM3NSAxMC4yMzgxIDQuMzc1IDEwLjQ0NDNDNC4zNzUgMTAuNjUwNiA0LjU0Mzc1IDEwLjgxOTMgNC43NSAxMC44MTkzTDYuNjI1IDEwLjgxOTNMNi42MjUgMTIuNjk0M0M2LjYyNSAxMi45MDA2IDYuNzkzNzUgMTMuMDY5MyA3IDEzLjA2OTNDNy4yMDYyNSAxMy4wNjkzIDcuMzc1IDEyLjkwMDYgNy4zNzUgMTIuNjk0M0w3LjM3NSAxMC44MTkzTDkuMjUgMTAuODE5M0M5LjQ1NjI1IDEwLjgxOTMgOS42MjUgMTAuNjUwNiA5LjYyNSAxMC40NDQzQzkuNjI1IDEwLjIzODEgOS40NTYyNSAxMC4wNjkzIDkuMjUgMTAuMDY5M1oiIGZpbGw9IiM2MTYxNjEiIHN0cm9rZT0iIzYxNjE2MSIgc3Ryb2tlLXdpZHRoPSIwLjciLz4KPC9nPgo8cGF0aCBjbGFzcz0ianAtaWNvbjMiIGZpbGwtcnVsZT0iZXZlbm9kZCIgY2xpcC1ydWxlPSJldmVub2RkIiBkPSJNMi41IDUuNUwyLjUgMy41TDExLjUgMy41TDExLjUgNS41TDIuNSA1LjVaTTIgN0MxLjQ0NzcyIDcgMSA2LjU1MjI4IDEgNkwxIDNDMSAyLjQ0NzcyIDEuNDQ3NzIgMiAyIDJMMTIgMkMxMi41NTIzIDIgMTMgMi40NDc3MiAxMyAzTDEzIDZDMTMgNi41NTIyOSAxMi41NTIzIDcgMTIgN0wyIDdaIiBmaWxsPSIjNjE2MTYxIi8+CjxkZWZzPgo8Y2xpcFBhdGggaWQ9ImNsaXAwXzEzN18xOTQ5OCI+CjxyZWN0IGNsYXNzPSJqcC1pY29uMyIgd2lkdGg9IjYiIGhlaWdodD0iNiIgZmlsbD0id2hpdGUiIHRyYW5zZm9ybT0ibWF0cml4KDEgMS43NDg0NmUtMDcgMS43NDg0NmUtMDcgLTEgNCAxMy40NDQzKSIvPgo8L2NsaXBQYXRoPgo8L2RlZnM+Cjwvc3ZnPgo=);
  --jp-icon-add: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE5IDEzaC02djZoLTJ2LTZINXYtMmg2VjVoMnY2aDZ2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-bell: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE2IDE2IiB2ZXJzaW9uPSIxLjEiPgogICA8cGF0aCBjbGFzcz0ianAtaWNvbjIganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMzMzMzMzIgogICAgICBkPSJtOCAwLjI5Yy0xLjQgMC0yLjcgMC43My0zLjYgMS44LTEuMiAxLjUtMS40IDMuNC0xLjUgNS4yLTAuMTggMi4yLTAuNDQgNC0yLjMgNS4zbDAuMjggMS4zaDVjMC4wMjYgMC42NiAwLjMyIDEuMSAwLjcxIDEuNSAwLjg0IDAuNjEgMiAwLjYxIDIuOCAwIDAuNTItMC40IDAuNi0xIDAuNzEtMS41aDVsMC4yOC0xLjNjLTEuOS0wLjk3LTIuMi0zLjMtMi4zLTUuMy0wLjEzLTEuOC0wLjI2LTMuNy0xLjUtNS4yLTAuODUtMS0yLjItMS44LTMuNi0xLjh6bTAgMS40YzAuODggMCAxLjkgMC41NSAyLjUgMS4zIDAuODggMS4xIDEuMSAyLjcgMS4yIDQuNCAwLjEzIDEuNyAwLjIzIDMuNiAxLjMgNS4yaC0xMGMxLjEtMS42IDEuMi0zLjQgMS4zLTUuMiAwLjEzLTEuNyAwLjMtMy4zIDEuMi00LjQgMC41OS0wLjcyIDEuNi0xLjMgMi41LTEuM3ptLTAuNzQgMTJoMS41Yy0wLjAwMTUgMC4yOCAwLjAxNSAwLjc5LTAuNzQgMC43OS0wLjczIDAuMDAxNi0wLjcyLTAuNTMtMC43NC0wLjc5eiIgLz4KPC9zdmc+Cg==);
  --jp-icon-bug-dot: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiPgogICAgICAgIDxwYXRoIGZpbGwtcnVsZT0iZXZlbm9kZCIgY2xpcC1ydWxlPSJldmVub2RkIiBkPSJNMTcuMTkgOEgyMFYxMEgxNy45MUMxNy45NiAxMC4zMyAxOCAxMC42NiAxOCAxMVYxMkgyMFYxNEgxOC41SDE4VjE0LjAyNzVDMTUuNzUgMTQuMjc2MiAxNCAxNi4xODM3IDE0IDE4LjVDMTQgMTkuMjA4IDE0LjE2MzUgMTkuODc3OSAxNC40NTQ5IDIwLjQ3MzlDMTMuNzA2MyAyMC44MTE3IDEyLjg3NTcgMjEgMTIgMjFDOS43OCAyMSA3Ljg1IDE5Ljc5IDYuODEgMThINFYxNkg2LjA5QzYuMDQgMTUuNjcgNiAxNS4zNCA2IDE1VjE0SDRWMTJINlYxMUM2IDEwLjY2IDYuMDQgMTAuMzMgNi4wOSAxMEg0VjhINi44MUM3LjI2IDcuMjIgNy44OCA2LjU1IDguNjIgNi4wNEw3IDQuNDFMOC40MSAzTDEwLjU5IDUuMTdDMTEuMDQgNS4wNiAxMS41MSA1IDEyIDVDMTIuNDkgNSAxMi45NiA1LjA2IDEzLjQyIDUuMTdMMTUuNTkgM0wxNyA0LjQxTDE1LjM3IDYuMDRDMTYuMTIgNi41NSAxNi43NCA3LjIyIDE3LjE5IDhaTTEwIDE2SDE0VjE0SDEwVjE2Wk0xMCAxMkgxNFYxMEgxMFYxMloiIGZpbGw9IiM2MTYxNjEiLz4KICAgICAgICA8cGF0aCBkPSJNMjIgMTguNUMyMiAyMC40MzMgMjAuNDMzIDIyIDE4LjUgMjJDMTYuNTY3IDIyIDE1IDIwLjQzMyAxNSAxOC41QzE1IDE2LjU2NyAxNi41NjcgMTUgMTguNSAxNUMyMC40MzMgMTUgMjIgMTYuNTY3IDIyIDE4LjVaIiBmaWxsPSIjNjE2MTYxIi8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-bug: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0yMCA4aC0yLjgxYy0uNDUtLjc4LTEuMDctMS40NS0xLjgyLTEuOTZMMTcgNC40MSAxNS41OSAzbC0yLjE3IDIuMTdDMTIuOTYgNS4wNiAxMi40OSA1IDEyIDVjLS40OSAwLS45Ni4wNi0xLjQxLjE3TDguNDEgMyA3IDQuNDFsMS42MiAxLjYzQzcuODggNi41NSA3LjI2IDcuMjIgNi44MSA4SDR2MmgyLjA5Yy0uMDUuMzMtLjA5LjY2LS4wOSAxdjFINHYyaDJ2MWMwIC4zNC4wNC42Ny4wOSAxSDR2MmgyLjgxYzEuMDQgMS43OSAyLjk3IDMgNS4xOSAzczQuMTUtMS4yMSA1LjE5LTNIMjB2LTJoLTIuMDljLjA1LS4zMy4wOS0uNjYuMDktMXYtMWgydi0yaC0ydi0xYzAtLjM0LS4wNC0uNjctLjA5LTFIMjBWOHptLTYgOGgtNHYtMmg0djJ6bTAtNGgtNHYtMmg0djJ6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-build: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE0LjkgMTcuNDVDMTYuMjUgMTcuNDUgMTcuMzUgMTYuMzUgMTcuMzUgMTVDMTcuMzUgMTMuNjUgMTYuMjUgMTIuNTUgMTQuOSAxMi41NUMxMy41NCAxMi41NSAxMi40NSAxMy42NSAxMi40NSAxNUMxMi40NSAxNi4zNSAxMy41NCAxNy40NSAxNC45IDE3LjQ1Wk0yMC4xIDE1LjY4TDIxLjU4IDE2Ljg0QzIxLjcxIDE2Ljk1IDIxLjc1IDE3LjEzIDIxLjY2IDE3LjI5TDIwLjI2IDE5LjcxQzIwLjE3IDE5Ljg2IDIwIDE5LjkyIDE5LjgzIDE5Ljg2TDE4LjA5IDE5LjE2QzE3LjczIDE5LjQ0IDE3LjMzIDE5LjY3IDE2LjkxIDE5Ljg1TDE2LjY0IDIxLjdDMTYuNjIgMjEuODcgMTYuNDcgMjIgMTYuMyAyMkgxMy41QzEzLjMyIDIyIDEzLjE4IDIxLjg3IDEzLjE1IDIxLjdMMTIuODkgMTkuODVDMTIuNDYgMTkuNjcgMTIuMDcgMTkuNDQgMTEuNzEgMTkuMTZMOS45NjAwMiAxOS44NkM5LjgxMDAyIDE5LjkyIDkuNjIwMDIgMTkuODYgOS41NDAwMiAxOS43MUw4LjE0MDAyIDE3LjI5QzguMDUwMDIgMTcuMTMgOC4wOTAwMiAxNi45NSA4LjIyMDAyIDE2Ljg0TDkuNzAwMDIgMTUuNjhMOS42NTAwMSAxNUw5LjcwMDAyIDE0LjMxTDguMjIwMDIgMTMuMTZDOC4wOTAwMiAxMy4wNSA4LjA1MDAyIDEyLjg2IDguMTQwMDIgMTIuNzFMOS41NDAwMiAxMC4yOUM5LjYyMDAyIDEwLjEzIDkuODEwMDIgMTAuMDcgOS45NjAwMiAxMC4xM0wxMS43MSAxMC44NEMxMi4wNyAxMC41NiAxMi40NiAxMC4zMiAxMi44OSAxMC4xNUwxMy4xNSA4LjI4OTk4QzEzLjE4IDguMTI5OTggMTMuMzIgNy45OTk5OCAxMy41IDcuOTk5OThIMTYuM0MxNi40NyA3Ljk5OTk4IDE2LjYyIDguMTI5OTggMTYuNjQgOC4yODk5OEwxNi45MSAxMC4xNUMxNy4zMyAxMC4zMiAxNy43MyAxMC41NiAxOC4wOSAxMC44NEwxOS44MyAxMC4xM0MyMCAxMC4wNyAyMC4xNyAxMC4xMyAyMC4yNiAxMC4yOUwyMS42NiAxMi43MUMyMS43NSAxMi44NiAyMS43MSAxMy4wNSAyMS41OCAxMy4xNkwyMC4xIDE0LjMxTDIwLjE1IDE1TDIwLjEgMTUuNjhaIi8+CiAgICA8cGF0aCBkPSJNNy4zMjk2NiA3LjQ0NDU0QzguMDgzMSA3LjAwOTU0IDguMzM5MzIgNi4wNTMzMiA3LjkwNDMyIDUuMjk5ODhDNy40NjkzMiA0LjU0NjQzIDYuNTA4MSA0LjI4MTU2IDUuNzU0NjYgNC43MTY1NkM1LjM5MTc2IDQuOTI2MDggNS4xMjY5NSA1LjI3MTE4IDUuMDE4NDkgNS42NzU5NEM0LjkxMDA0IDYuMDgwNzEgNC45NjY4MiA2LjUxMTk4IDUuMTc2MzQgNi44NzQ4OEM1LjYxMTM0IDcuNjI4MzIgNi41NzYyMiA3Ljg3OTU0IDcuMzI5NjYgNy40NDQ1NFpNOS42NTcxOCA0Ljc5NTkzTDEwLjg2NzIgNC45NTE3OUMxMC45NjI4IDQuOTc3NDEgMTEuMDQwMiA1LjA3MTMzIDExLjAzODIgNS4xODc5M0wxMS4wMzg4IDYuOTg4OTNDMTEuMDQ1NSA3LjEwMDU0IDEwLjk2MTYgNy4xOTUxOCAxMC44NTUgNy4yMTA1NEw5LjY2MDAxIDcuMzgwODNMOS4yMzkxNSA4LjEzMTg4TDkuNjY5NjEgOS4yNTc0NUM5LjcwNzI5IDkuMzYyNzEgOS42NjkzNCA5LjQ3Njk5IDkuNTc0MDggOS41MzE5OUw4LjAxNTIzIDEwLjQzMkM3LjkxMTMxIDEwLjQ5MiA3Ljc5MzM3IDEwLjQ2NzcgNy43MjEwNSAxMC4zODI0TDYuOTg3NDggOS40MzE4OEw2LjEwOTMxIDkuNDMwODNMNS4zNDcwNCAxMC4zOTA1QzUuMjg5MDkgMTAuNDcwMiA1LjE3MzgzIDEwLjQ5MDUgNS4wNzE4NyAxMC40MzM5TDMuNTEyNDUgOS41MzI5M0MzLjQxMDQ5IDkuNDc2MzMgMy4zNzY0NyA5LjM1NzQxIDMuNDEwNzUgOS4yNTY3OUwzLjg2MzQ3IDguMTQwOTNMMy42MTc0OSA3Ljc3NDg4TDMuNDIzNDcgNy4zNzg4M0wyLjIzMDc1IDcuMjEyOTdDMi4xMjY0NyA3LjE5MjM1IDIuMDQwNDkgNy4xMDM0MiAyLjA0MjQ1IDYuOTg2ODJMMi4wNDE4NyA1LjE4NTgyQzIuMDQzODMgNS4wNjkyMiAyLjExOTA5IDQuOTc5NTggMi4yMTcwNCA0Ljk2OTIyTDMuNDIwNjUgNC43OTM5M0wzLjg2NzQ5IDQuMDI3ODhMMy40MTEwNSAyLjkxNzMxQzMuMzczMzcgMi44MTIwNCAzLjQxMTMxIDIuNjk3NzYgMy41MTUyMyAyLjYzNzc2TDUuMDc0MDggMS43Mzc3NkM1LjE2OTM0IDEuNjgyNzYgNS4yODcyOSAxLjcwNzA0IDUuMzU5NjEgMS43OTIzMUw2LjExOTE1IDIuNzI3ODhMNi45ODAwMSAyLjczODkzTDcuNzI0OTYgMS43ODkyMkM3Ljc5MTU2IDEuNzA0NTggNy45MTU0OCAxLjY3OTIyIDguMDA4NzkgMS43NDA4Mkw5LjU2ODIxIDIuNjQxODJDOS42NzAxNyAyLjY5ODQyIDkuNzEyODUgMi44MTIzNCA5LjY4NzIzIDIuOTA3OTdMOS4yMTcxOCA0LjAzMzgzTDkuNDYzMTYgNC4zOTk4OEw5LjY1NzE4IDQuNzk1OTNaIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down-empty-thin: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwb2x5Z29uIGNsYXNzPSJzdDEiIHBvaW50cz0iOS45LDEzLjYgMy42LDcuNCA0LjQsNi42IDkuOSwxMi4yIDE1LjQsNi43IDE2LjEsNy40ICIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down-empty: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik01LjIsNS45TDksOS43bDMuOC0zLjhsMS4yLDEuMmwtNC45LDVsLTQuOS01TDUuMiw1Ljl6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik01LjIsNy41TDksMTEuMmwzLjgtMy44SDUuMnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-caret-left: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwYXRoIGQ9Ik0xMC44LDEyLjhMNy4xLDlsMy44LTMuOGwwLDcuNkgxMC44eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-caret-right: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik03LjIsNS4yTDEwLjksOWwtMy44LDMuOFY1LjJINy4yeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-caret-up-empty-thin: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwb2x5Z29uIGNsYXNzPSJzdDEiIHBvaW50cz0iMTUuNCwxMy4zIDkuOSw3LjcgNC40LDEzLjIgMy42LDEyLjUgOS45LDYuMyAxNi4xLDEyLjYgIi8+Cgk8L2c+Cjwvc3ZnPgo=);
  --jp-icon-caret-up: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwYXRoIGQ9Ik01LjIsMTAuNUw5LDYuOGwzLjgsMy44SDUuMnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-case-sensitive: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0MTQxNDEiPgogICAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiAgPC9nPgogIDxnIGNsYXNzPSJqcC1pY29uLWFjY2VudDIiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTcuNiw4aDAuOWwzLjUsOGgtMS4xTDEwLDE0SDZsLTAuOSwySDRMNy42LDh6IE04LDkuMUw2LjQsMTNoMy4yTDgsOS4xeiIvPgogICAgPHBhdGggZD0iTTE2LjYsOS44Yy0wLjIsMC4xLTAuNCwwLjEtMC43LDAuMWMtMC4yLDAtMC40LTAuMS0wLjYtMC4yYy0wLjEtMC4xLTAuMi0wLjQtMC4yLTAuNyBjLTAuMywwLjMtMC42LDAuNS0wLjksMC43Yy0wLjMsMC4xLTAuNywwLjItMS4xLDAuMmMtMC4zLDAtMC41LDAtMC43LTAuMWMtMC4yLTAuMS0wLjQtMC4yLTAuNi0wLjNjLTAuMi0wLjEtMC4zLTAuMy0wLjQtMC41IGMtMC4xLTAuMi0wLjEtMC40LTAuMS0wLjdjMC0wLjMsMC4xLTAuNiwwLjItMC44YzAuMS0wLjIsMC4zLTAuNCwwLjQtMC41QzEyLDcsMTIuMiw2LjksMTIuNSw2LjhjMC4yLTAuMSwwLjUtMC4xLDAuNy0wLjIgYzAuMy0wLjEsMC41LTAuMSwwLjctMC4xYzAuMiwwLDAuNC0wLjEsMC42LTAuMWMwLjIsMCwwLjMtMC4xLDAuNC0wLjJjMC4xLTAuMSwwLjItMC4yLDAuMi0wLjRjMC0xLTEuMS0xLTEuMy0xIGMtMC40LDAtMS40LDAtMS40LDEuMmgtMC45YzAtMC40LDAuMS0wLjcsMC4yLTFjMC4xLTAuMiwwLjMtMC40LDAuNS0wLjZjMC4yLTAuMiwwLjUtMC4zLDAuOC0wLjNDMTMuMyw0LDEzLjYsNCwxMy45LDQgYzAuMywwLDAuNSwwLDAuOCwwLjFjMC4zLDAsMC41LDAuMSwwLjcsMC4yYzAuMiwwLjEsMC40LDAuMywwLjUsMC41QzE2LDUsMTYsNS4yLDE2LDUuNnYyLjljMCwwLjIsMCwwLjQsMCwwLjUgYzAsMC4xLDAuMSwwLjIsMC4zLDAuMmMwLjEsMCwwLjIsMCwwLjMsMFY5Ljh6IE0xNS4yLDYuOWMtMS4yLDAuNi0zLjEsMC4yLTMuMSwxLjRjMCwxLjQsMy4xLDEsMy4xLTAuNVY2Ljl6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-check: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik05IDE2LjE3TDQuODMgMTJsLTEuNDIgMS40MUw5IDE5IDIxIDdsLTEuNDEtMS40MXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-circle-empty: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyIDJDNi40NyAyIDIgNi40NyAyIDEyczQuNDcgMTAgMTAgMTAgMTAtNC40NyAxMC0xMFMxNy41MyAyIDEyIDJ6bTAgMThjLTQuNDEgMC04LTMuNTktOC04czMuNTktOCA4LTggOCAzLjU5IDggOC0zLjU5IDgtOCA4eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-circle: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPGNpcmNsZSBjeD0iOSIgY3k9IjkiIHI9IjgiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-clear: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8bWFzayBpZD0iZG9udXRIb2xlIj4KICAgIDxyZWN0IHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgZmlsbD0id2hpdGUiIC8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSI4IiBmaWxsPSJibGFjayIvPgogIDwvbWFzaz4KCiAgPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxyZWN0IGhlaWdodD0iMTgiIHdpZHRoPSIyIiB4PSIxMSIgeT0iMyIgdHJhbnNmb3JtPSJyb3RhdGUoMzE1LCAxMiwgMTIpIi8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIxMCIgbWFzaz0idXJsKCNkb251dEhvbGUpIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-close: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1ub25lIGpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIGpwLWljb24zLWhvdmVyIiBmaWxsPSJub25lIj4KICAgIDxjaXJjbGUgY3g9IjEyIiBjeT0iMTIiIHI9IjExIi8+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIGpwLWljb24tYWNjZW50Mi1ob3ZlciIgZmlsbD0iIzYxNjE2MSI+CiAgICA8cGF0aCBkPSJNMTkgNi40MUwxNy41OSA1IDEyIDEwLjU5IDYuNDEgNSA1IDYuNDEgMTAuNTkgMTIgNSAxNy41OSA2LjQxIDE5IDEyIDEzLjQxIDE3LjU5IDE5IDE5IDE3LjU5IDEzLjQxIDEyeiIvPgogIDwvZz4KCiAgPGcgY2xhc3M9ImpwLWljb24tbm9uZSBqcC1pY29uLWJ1c3kiIGZpbGw9Im5vbmUiPgogICAgPGNpcmNsZSBjeD0iMTIiIGN5PSIxMiIgcj0iNyIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-code-check: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBzaGFwZS1yZW5kZXJpbmc9Imdlb21ldHJpY1ByZWNpc2lvbiI+CiAgICA8cGF0aCBkPSJNNi41OSwzLjQxTDIsOEw2LjU5LDEyLjZMOCwxMS4xOEw0LjgyLDhMOCw0LjgyTDYuNTksMy40MU0xMi40MSwzLjQxTDExLDQuODJMMTQuMTgsOEwxMSwxMS4xOEwxMi40MSwxMi42TDE3LDhMMTIuNDEsMy40MU0yMS41OSwxMS41OUwxMy41LDE5LjY4TDkuODMsMTZMOC40MiwxNy40MUwxMy41LDIyLjVMMjMsMTNMMjEuNTksMTEuNTlaIiAvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-code: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjIiIGhlaWdodD0iMjIiIHZpZXdCb3g9IjAgMCAyOCAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTExLjQgMTguNkw2LjggMTRMMTEuNCA5LjRMMTAgOEw0IDE0TDEwIDIwTDExLjQgMTguNlpNMTYuNiAxOC42TDIxLjIgMTRMMTYuNiA5LjRMMTggOEwyNCAxNEwxOCAyMEwxNi42IDE4LjZWMTguNloiLz4KCTwvZz4KPC9zdmc+Cg==);
  --jp-icon-collapse-all: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTggMmMxIDAgMTEgMCAxMiAwczIgMSAyIDJjMCAxIDAgMTEgMCAxMnMwIDItMiAyQzIwIDE0IDIwIDQgMjAgNFMxMCA0IDYgNGMwLTIgMS0yIDItMnoiIC8+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTE4IDhjMC0xLTEtMi0yLTJTNSA2IDQgNnMtMiAxLTIgMmMwIDEgMCAxMSAwIDEyczEgMiAyIDJjMSAwIDExIDAgMTIgMHMyLTEgMi0yYzAtMSAwLTExIDAtMTJ6bS0yIDB2MTJINFY4eiIgLz4KICAgICAgICA8cGF0aCBkPSJNNiAxM3YyaDh2LTJ6IiAvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-console: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwMCAyMDAiPgogIDxnIGNsYXNzPSJqcC1jb25zb2xlLWljb24tYmFja2dyb3VuZC1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiMwMjg4RDEiPgogICAgPHBhdGggZD0iTTIwIDE5LjhoMTYwdjE1OS45SDIweiIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtY29uc29sZS1pY29uLWNvbG9yIGpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIiBmaWxsPSIjZmZmIj4KICAgIDxwYXRoIGQ9Ik0xMDUgMTI3LjNoNDB2MTIuOGgtNDB6TTUxLjEgNzdMNzQgOTkuOWwtMjMuMyAyMy4zIDEwLjUgMTAuNSAyMy4zLTIzLjNMOTUgOTkuOSA4NC41IDg5LjQgNjEuNiA2Ni41eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-copy: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTExLjksMUgzLjJDMi40LDEsMS43LDEuNywxLjcsMi41djEwLjJoMS41VjIuNWg4LjdWMXogTTE0LjEsMy45aC04Yy0wLjgsMC0xLjUsMC43LTEuNSwxLjV2MTAuMmMwLDAuOCwwLjcsMS41LDEuNSwxLjVoOCBjMC44LDAsMS41LTAuNywxLjUtMS41VjUuNEMxNS41LDQuNiwxNC45LDMuOSwxNC4xLDMuOXogTTE0LjEsMTUuNWgtOFY1LjRoOFYxNS41eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-copyright: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGVuYWJsZS1iYWNrZ3JvdW5kPSJuZXcgMCAwIDI0IDI0IiBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCI+CiAgPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0xMS44OCw5LjE0YzEuMjgsMC4wNiwxLjYxLDEuMTUsMS42MywxLjY2aDEuNzljLTAuMDgtMS45OC0xLjQ5LTMuMTktMy40NS0zLjE5QzkuNjQsNy42MSw4LDksOCwxMi4xNCBjMCwxLjk0LDAuOTMsNC4yNCwzLjg0LDQuMjRjMi4yMiwwLDMuNDEtMS42NSwzLjQ0LTIuOTVoLTEuNzljLTAuMDMsMC41OS0wLjQ1LDEuMzgtMS42MywxLjQ0QzEwLjU1LDE0LjgzLDEwLDEzLjgxLDEwLDEyLjE0IEMxMCw5LjI1LDExLjI4LDkuMTYsMTEuODgsOS4xNHogTTEyLDJDNi40OCwyLDIsNi40OCwyLDEyczQuNDgsMTAsMTAsMTBzMTAtNC40OCwxMC0xMFMxNy41MiwyLDEyLDJ6IE0xMiwyMGMtNC40MSwwLTgtMy41OS04LTggczMuNTktOCw4LThzOCwzLjU5LDgsOFMxNi40MSwyMCwxMiwyMHoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-cut: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkuNjQgNy42NGMuMjMtLjUuMzYtMS4wNS4zNi0xLjY0IDAtMi4yMS0xLjc5LTQtNC00UzIgMy43OSAyIDZzMS43OSA0IDQgNGMuNTkgMCAxLjE0LS4xMyAxLjY0LS4zNkwxMCAxMmwtMi4zNiAyLjM2QzcuMTQgMTQuMTMgNi41OSAxNCA2IDE0Yy0yLjIxIDAtNCAxLjc5LTQgNHMxLjc5IDQgNCA0IDQtMS43OSA0LTRjMC0uNTktLjEzLTEuMTQtLjM2LTEuNjRMMTIgMTRsNyA3aDN2LTFMOS42NCA3LjY0ek02IDhjLTEuMSAwLTItLjg5LTItMnMuOS0yIDItMiAyIC44OSAyIDItLjkgMi0yIDJ6bTAgMTJjLTEuMSAwLTItLjg5LTItMnMuOS0yIDItMiAyIC44OSAyIDItLjkgMi0yIDJ6bTYtNy41Yy0uMjggMC0uNS0uMjItLjUtLjVzLjIyLS41LjUtLjUuNS4yMi41LjUtLjIyLjUtLjUuNXpNMTkgM2wtNiA2IDIgMiA3LTdWM3oiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-delete: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2cHgiIGhlaWdodD0iMTZweCI+CiAgICA8cGF0aCBkPSJNMCAwaDI0djI0SDB6IiBmaWxsPSJub25lIiAvPgogICAgPHBhdGggY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjI2MjYyIiBkPSJNNiAxOWMwIDEuMS45IDIgMiAyaDhjMS4xIDAgMi0uOSAyLTJWN0g2djEyek0xOSA0aC0zLjVsLTEtMWgtNWwtMSAxSDV2MmgxNFY0eiIgLz4KPC9zdmc+Cg==);
  --jp-icon-download: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE5IDloLTRWM0g5djZINWw3IDcgNy03ek01IDE4djJoMTR2LTJINXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-duplicate: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTIuNzk5OTggMC44NzVIOC44OTU4MkM5LjIwMDYxIDAuODc1IDkuNDQ5OTggMS4xMzkxNCA5LjQ0OTk4IDEuNDYxOThDOS40NDk5OCAxLjc4NDgyIDkuMjAwNjEgMi4wNDg5NiA4Ljg5NTgyIDIuMDQ4OTZIMy4zNTQxNUMzLjA0OTM2IDIuMDQ4OTYgMi43OTk5OCAyLjMxMzEgMi43OTk5OCAyLjYzNTk0VjkuNjc5NjlDMi43OTk5OCAxMC4wMDI1IDIuNTUwNjEgMTAuMjY2NyAyLjI0NTgyIDEwLjI2NjdDMS45NDEwMyAxMC4yNjY3IDEuNjkxNjUgMTAuMDAyNSAxLjY5MTY1IDkuNjc5NjlWMi4wNDg5NkMxLjY5MTY1IDEuNDAzMjggMi4xOTA0IDAuODc1IDIuNzk5OTggMC44NzVaTTUuMzY2NjUgMTEuOVY0LjU1SDExLjA4MzNWMTEuOUg1LjM2NjY1Wk00LjE0MTY1IDQuMTQxNjdDNC4xNDE2NSAzLjY5MDYzIDQuNTA3MjggMy4zMjUgNC45NTgzMiAzLjMyNUgxMS40OTE3QzExLjk0MjcgMy4zMjUgMTIuMzA4MyAzLjY5MDYzIDEyLjMwODMgNC4xNDE2N1YxMi4zMDgzQzEyLjMwODMgMTIuNzU5NCAxMS45NDI3IDEzLjEyNSAxMS40OTE3IDEzLjEyNUg0Ljk1ODMyQzQuNTA3MjggMTMuMTI1IDQuMTQxNjUgMTIuNzU5NCA0LjE0MTY1IDEyLjMwODNWNC4xNDE2N1oiIGZpbGw9IiM2MTYxNjEiLz4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBkPSJNOS40MzU3NCA4LjI2NTA3SDguMzY0MzFWOS4zMzY1QzguMzY0MzEgOS40NTQzNSA4LjI2Nzg4IDkuNTUwNzggOC4xNTAwMiA5LjU1MDc4QzguMDMyMTcgOS41NTA3OCA3LjkzNTc0IDkuNDU0MzUgNy45MzU3NCA5LjMzNjVWOC4yNjUwN0g2Ljg2NDMxQzYuNzQ2NDUgOC4yNjUwNyA2LjY1MDAyIDguMTY4NjQgNi42NTAwMiA4LjA1MDc4QzYuNjUwMDIgNy45MzI5MiA2Ljc0NjQ1IDcuODM2NSA2Ljg2NDMxIDcuODM2NUg3LjkzNTc0VjYuNzY1MDdDNy45MzU3NCA2LjY0NzIxIDguMDMyMTcgNi41NTA3OCA4LjE1MDAyIDYuNTUwNzhDOC4yNjc4OCA2LjU1MDc4IDguMzY0MzEgNi42NDcyMSA4LjM2NDMxIDYuNzY1MDdWNy44MzY1SDkuNDM1NzRDOS41NTM2IDcuODM2NSA5LjY1MDAyIDcuOTMyOTIgOS42NTAwMiA4LjA1MDc4QzkuNjUwMDIgOC4xNjg2NCA5LjU1MzYgOC4yNjUwNyA5LjQzNTc0IDguMjY1MDdaIiBmaWxsPSIjNjE2MTYxIiBzdHJva2U9IiM2MTYxNjEiIHN0cm9rZS13aWR0aD0iMC41Ii8+Cjwvc3ZnPgo=);
  --jp-icon-edit: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTMgMTcuMjVWMjFoMy43NUwxNy44MSA5Ljk0bC0zLjc1LTMuNzVMMyAxNy4yNXpNMjAuNzEgNy4wNGMuMzktLjM5LjM5LTEuMDIgMC0xLjQxbC0yLjM0LTIuMzRjLS4zOS0uMzktMS4wMi0uMzktMS40MSAwbC0xLjgzIDEuODMgMy43NSAzLjc1IDEuODMtMS44M3oiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-ellipses: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPGNpcmNsZSBjeD0iNSIgY3k9IjEyIiByPSIyIi8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIyIi8+CiAgICA8Y2lyY2xlIGN4PSIxOSIgY3k9IjEyIiByPSIyIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-error: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj48Y2lyY2xlIGN4PSIxMiIgY3k9IjE5IiByPSIyIi8+PHBhdGggZD0iTTEwIDNoNHYxMmgtNHoiLz48L2c+CjxwYXRoIGZpbGw9Im5vbmUiIGQ9Ik0wIDBoMjR2MjRIMHoiLz4KPC9zdmc+Cg==);
  --jp-icon-expand-all: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTggMmMxIDAgMTEgMCAxMiAwczIgMSAyIDJjMCAxIDAgMTEgMCAxMnMwIDItMiAyQzIwIDE0IDIwIDQgMjAgNFMxMCA0IDYgNGMwLTIgMS0yIDItMnoiIC8+CiAgICAgICAgPHBhdGgKICAgICAgICAgICAgZD0iTTE4IDhjMC0xLTEtMi0yLTJTNSA2IDQgNnMtMiAxLTIgMmMwIDEgMCAxMSAwIDEyczEgMiAyIDJjMSAwIDExIDAgMTIgMHMyLTEgMi0yYzAtMSAwLTExIDAtMTJ6bS0yIDB2MTJINFY4eiIgLz4KICAgICAgICA8cGF0aCBkPSJNMTEgMTBIOXYzSDZ2MmgzdjNoMnYtM2gzdi0yaC0zeiIgLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-extension: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwLjUgMTFIMTlWN2MwLTEuMS0uOS0yLTItMmgtNFYzLjVDMTMgMi4xMiAxMS44OCAxIDEwLjUgMVM4IDIuMTIgOCAzLjVWNUg0Yy0xLjEgMC0xLjk5LjktMS45OSAydjMuOEgzLjVjMS40OSAwIDIuNyAxLjIxIDIuNyAyLjdzLTEuMjEgMi43LTIuNyAyLjdIMlYyMGMwIDEuMS45IDIgMiAyaDMuOHYtMS41YzAtMS40OSAxLjIxLTIuNyAyLjctMi43IDEuNDkgMCAyLjcgMS4yMSAyLjcgMi43VjIySDE3YzEuMSAwIDItLjkgMi0ydi00aDEuNWMxLjM4IDAgMi41LTEuMTIgMi41LTIuNVMyMS44OCAxMSAyMC41IDExeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-fast-forward: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTQgMThsOC41LTZMNCA2djEyem05LTEydjEybDguNS02TDEzIDZ6Ii8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-file-upload: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkgMTZoNnYtNmg0bC03LTctNyA3aDR6bS00IDJoMTR2Mkg1eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-file: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkuMyA4LjJsLTUuNS01LjVjLS4zLS4zLS43LS41LTEuMi0uNUgzLjljLS44LjEtMS42LjktMS42IDEuOHYxNC4xYzAgLjkuNyAxLjYgMS42IDEuNmgxNC4yYy45IDAgMS42LS43IDEuNi0xLjZWOS40Yy4xLS41LS4xLS45LS40LTEuMnptLTUuOC0zLjNsMy40IDMuNmgtMy40VjQuOXptMy45IDEyLjdINC43Yy0uMSAwLS4yIDAtLjItLjJWNC43YzAtLjIuMS0uMy4yLS4zaDcuMnY0LjRzMCAuOC4zIDEuMWMuMy4zIDEuMS4zIDEuMS4zaDQuM3Y3LjJzLS4xLjItLjIuMnoiLz4KPC9zdmc+Cg==);
  --jp-icon-filter-dot: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTE0LDEyVjE5Ljg4QzE0LjA0LDIwLjE4IDEzLjk0LDIwLjUgMTMuNzEsMjAuNzFDMTMuMzIsMjEuMSAxMi42OSwyMS4xIDEyLjMsMjAuNzFMMTAuMjksMTguN0MxMC4wNiwxOC40NyA5Ljk2LDE4LjE2IDEwLDE3Ljg3VjEySDkuOTdMNC4yMSw0LjYyQzMuODcsNC4xOSAzLjk1LDMuNTYgNC4zOCwzLjIyQzQuNTcsMy4wOCA0Ljc4LDMgNSwzVjNIMTlWM0MxOS4yMiwzIDE5LjQzLDMuMDggMTkuNjIsMy4yMkMyMC4wNSwzLjU2IDIwLjEzLDQuMTkgMTkuNzksNC42MkwxNC4wMywxMkgxNFoiIC8+CiAgPC9nPgogIDxnIGNsYXNzPSJqcC1pY29uLWRvdCIgZmlsbD0iI0ZGRiI+CiAgICA8Y2lyY2xlIGN4PSIxOCIgY3k9IjE3IiByPSIzIj48L2NpcmNsZT4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-filter-list: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEwIDE4aDR2LTJoLTR2MnpNMyA2djJoMThWNkgzem0zIDdoMTJ2LTJINnYyeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-filter: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTE0LDEyVjE5Ljg4QzE0LjA0LDIwLjE4IDEzLjk0LDIwLjUgMTMuNzEsMjAuNzFDMTMuMzIsMjEuMSAxMi42OSwyMS4xIDEyLjMsMjAuNzFMMTAuMjksMTguN0MxMC4wNiwxOC40NyA5Ljk2LDE4LjE2IDEwLDE3Ljg3VjEySDkuOTdMNC4yMSw0LjYyQzMuODcsNC4xOSAzLjk1LDMuNTYgNC4zOCwzLjIyQzQuNTcsMy4wOCA0Ljc4LDMgNSwzVjNIMTlWM0MxOS4yMiwzIDE5LjQzLDMuMDggMTkuNjIsMy4yMkMyMC4wNSwzLjU2IDIwLjEzLDQuMTkgMTkuNzksNC42MkwxNC4wMywxMkgxNFoiIC8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-folder-favorite: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjRweCIgdmlld0JveD0iMCAwIDI0IDI0IiB3aWR0aD0iMjRweCIgZmlsbD0iIzAwMDAwMCI+CiAgPHBhdGggZD0iTTAgMGgyNHYyNEgwVjB6IiBmaWxsPSJub25lIi8+PHBhdGggY2xhc3M9ImpwLWljb24zIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzYxNjE2MSIgZD0iTTIwIDZoLThsLTItMkg0Yy0xLjEgMC0yIC45LTIgMnYxMmMwIDEuMS45IDIgMiAyaDE2YzEuMSAwIDItLjkgMi0yVjhjMC0xLjEtLjktMi0yLTJ6bS0yLjA2IDExTDE1IDE1LjI4IDEyLjA2IDE3bC43OC0zLjMzLTIuNTktMi4yNCAzLjQxLS4yOUwxNSA4bDEuMzQgMy4xNCAzLjQxLjI5LTIuNTkgMi4yNC43OCAzLjMzeiIvPgo8L3N2Zz4K);
  --jp-icon-folder: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTAgNEg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMThjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY4YzAtMS4xLS45LTItMi0yaC04bC0yLTJ6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-home: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjRweCIgdmlld0JveD0iMCAwIDI0IDI0IiB3aWR0aD0iMjRweCIgZmlsbD0iIzAwMDAwMCI+CiAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPjxwYXRoIGNsYXNzPSJqcC1pY29uMyBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xMCAyMHYtNmg0djZoNXYtOGgzTDEyIDMgMiAxMmgzdjh6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-html5: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUxMiA1MTIiPgogIDxwYXRoIGNsYXNzPSJqcC1pY29uMCBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiMwMDAiIGQ9Ik0xMDguNCAwaDIzdjIyLjhoMjEuMlYwaDIzdjY5aC0yM1Y0NmgtMjF2MjNoLTIzLjJNMjA2IDIzaC0yMC4zVjBoNjMuN3YyM0gyMjl2NDZoLTIzbTUzLjUtNjloMjQuMWwxNC44IDI0LjNMMzEzLjIgMGgyNC4xdjY5aC0yM1YzNC44bC0xNi4xIDI0LjgtMTYuMS0yNC44VjY5aC0yMi42bTg5LjItNjloMjN2NDYuMmgzMi42VjY5aC01NS42Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI2U0NGQyNiIgZD0iTTEwNy42IDQ3MWwtMzMtMzcwLjRoMzYyLjhsLTMzIDM3MC4yTDI1NS43IDUxMiIvPgogIDxwYXRoIGNsYXNzPSJqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNmMTY1MjkiIGQ9Ik0yNTYgNDgwLjVWMTMxaDE0OC4zTDM3NiA0NDciLz4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNlYmViZWIiIGQ9Ik0xNDIgMTc2LjNoMTE0djQ1LjRoLTY0LjJsNC4yIDQ2LjVoNjB2NDUuM0gxNTQuNG0yIDIyLjhIMjAybDMuMiAzNi4zIDUwLjggMTMuNnY0Ny40bC05My4yLTI2Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIiBmaWxsPSIjZmZmIiBkPSJNMzY5LjYgMTc2LjNIMjU1Ljh2NDUuNGgxMDkuNm0tNC4xIDQ2LjVIMjU1Ljh2NDUuNGg1NmwtNS4zIDU5LTUwLjcgMTMuNnY0Ny4ybDkzLTI1LjgiLz4KPC9zdmc+Cg==);
  --jp-icon-image: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1icmFuZDQganAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNGRkYiIGQ9Ik0yLjIgMi4yaDE3LjV2MTcuNUgyLjJ6Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzNGNTFCNSIgZD0iTTIuMiAyLjJ2MTcuNWgxNy41bC4xLTE3LjVIMi4yem0xMi4xIDIuMmMxLjIgMCAyLjIgMSAyLjIgMi4ycy0xIDIuMi0yLjIgMi4yLTIuMi0xLTIuMi0yLjIgMS0yLjIgMi4yLTIuMnpNNC40IDE3LjZsMy4zLTguOCAzLjMgNi42IDIuMi0zLjIgNC40IDUuNEg0LjR6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-info: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUwLjk3OCA1MC45NzgiPgoJPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KCQk8cGF0aCBkPSJNNDMuNTIsNy40NThDMzguNzExLDIuNjQ4LDMyLjMwNywwLDI1LjQ4OSwwQzE4LjY3LDAsMTIuMjY2LDIuNjQ4LDcuNDU4LDcuNDU4CgkJCWMtOS45NDMsOS45NDEtOS45NDMsMjYuMTE5LDAsMzYuMDYyYzQuODA5LDQuODA5LDExLjIxMiw3LjQ1NiwxOC4wMzEsNy40NThjMCwwLDAuMDAxLDAsMC4wMDIsMAoJCQljNi44MTYsMCwxMy4yMjEtMi42NDgsMTguMDI5LTcuNDU4YzQuODA5LTQuODA5LDcuNDU3LTExLjIxMiw3LjQ1Ny0xOC4wM0M1MC45NzcsMTguNjcsNDguMzI4LDEyLjI2Niw0My41Miw3LjQ1OHoKCQkJIE00Mi4xMDYsNDIuMTA1Yy00LjQzMiw0LjQzMS0xMC4zMzIsNi44NzItMTYuNjE1LDYuODcyaC0wLjAwMmMtNi4yODUtMC4wMDEtMTIuMTg3LTIuNDQxLTE2LjYxNy02Ljg3MgoJCQljLTkuMTYyLTkuMTYzLTkuMTYyLTI0LjA3MSwwLTMzLjIzM0MxMy4zMDMsNC40NCwxOS4yMDQsMiwyNS40ODksMmM2LjI4NCwwLDEyLjE4NiwyLjQ0LDE2LjYxNyw2Ljg3MgoJCQljNC40MzEsNC40MzEsNi44NzEsMTAuMzMyLDYuODcxLDE2LjYxN0M0OC45NzcsMzEuNzcyLDQ2LjUzNiwzNy42NzUsNDIuMTA2LDQyLjEwNXoiLz4KCQk8cGF0aCBkPSJNMjMuNTc4LDMyLjIxOGMtMC4wMjMtMS43MzQsMC4xNDMtMy4wNTksMC40OTYtMy45NzJjMC4zNTMtMC45MTMsMS4xMS0xLjk5NywyLjI3Mi0zLjI1MwoJCQljMC40NjgtMC41MzYsMC45MjMtMS4wNjIsMS4zNjctMS41NzVjMC42MjYtMC43NTMsMS4xMDQtMS40NzgsMS40MzYtMi4xNzVjMC4zMzEtMC43MDcsMC40OTUtMS41NDEsMC40OTUtMi41CgkJCWMwLTEuMDk2LTAuMjYtMi4wODgtMC43NzktMi45NzljLTAuNTY1LTAuODc5LTEuNTAxLTEuMzM2LTIuODA2LTEuMzY5Yy0xLjgwMiwwLjA1Ny0yLjk4NSwwLjY2Ny0zLjU1LDEuODMyCgkJCWMtMC4zMDEsMC41MzUtMC41MDMsMS4xNDEtMC42MDcsMS44MTRjLTAuMTM5LDAuNzA3LTAuMjA3LDEuNDMyLTAuMjA3LDIuMTc0aC0yLjkzN2MtMC4wOTEtMi4yMDgsMC40MDctNC4xMTQsMS40OTMtNS43MTkKCQkJYzEuMDYyLTEuNjQsMi44NTUtMi40ODEsNS4zNzgtMi41MjdjMi4xNiwwLjAyMywzLjg3NCwwLjYwOCw1LjE0MSwxLjc1OGMxLjI3OCwxLjE2LDEuOTI5LDIuNzY0LDEuOTUsNC44MTEKCQkJYzAsMS4xNDItMC4xMzcsMi4xMTEtMC40MSwyLjkxMWMtMC4zMDksMC44NDUtMC43MzEsMS41OTMtMS4yNjgsMi4yNDNjLTAuNDkyLDAuNjUtMS4wNjgsMS4zMTgtMS43MywyLjAwMgoJCQljLTAuNjUsMC42OTctMS4zMTMsMS40NzktMS45ODcsMi4zNDZjLTAuMjM5LDAuMzc3LTAuNDI5LDAuNzc3LTAuNTY1LDEuMTk5Yy0wLjE2LDAuOTU5LTAuMjE3LDEuOTUxLTAuMTcxLDIuOTc5CgkJCUMyNi41ODksMzIuMjE4LDIzLjU3OCwzMi4yMTgsMjMuNTc4LDMyLjIxOHogTTIzLjU3OCwzOC4yMnYtMy40ODRoMy4wNzZ2My40ODRIMjMuNTc4eiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-inspector: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaW5zcGVjdG9yLWljb24tY29sb3IganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMjAgNEg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMThjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY2YzAtMS4xLS45LTItMi0yem0tNSAxNEg0di00aDExdjR6bTAtNUg0VjloMTF2NHptNSA1aC00VjloNHY5eiIvPgo8L3N2Zz4K);
  --jp-icon-json: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtanNvbi1pY29uLWNvbG9yIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI0Y5QTgyNSI+CiAgICA8cGF0aCBkPSJNMjAuMiAxMS44Yy0xLjYgMC0xLjcuNS0xLjcgMSAwIC40LjEuOS4xIDEuMy4xLjUuMS45LjEgMS4zIDAgMS43LTEuNCAyLjMtMy41IDIuM2gtLjl2LTEuOWguNWMxLjEgMCAxLjQgMCAxLjQtLjggMC0uMyAwLS42LS4xLTEgMC0uNC0uMS0uOC0uMS0xLjIgMC0xLjMgMC0xLjggMS4zLTItMS4zLS4yLTEuMy0uNy0xLjMtMiAwLS40LjEtLjguMS0xLjIuMS0uNC4xLS43LjEtMSAwLS44LS40LS43LTEuNC0uOGgtLjVWNC4xaC45YzIuMiAwIDMuNS43IDMuNSAyLjMgMCAuNC0uMS45LS4xIDEuMy0uMS41LS4xLjktLjEgMS4zIDAgLjUuMiAxIDEuNyAxdjEuOHpNMS44IDEwLjFjMS42IDAgMS43LS41IDEuNy0xIDAtLjQtLjEtLjktLjEtMS4zLS4xLS41LS4xLS45LS4xLTEuMyAwLTEuNiAxLjQtMi4zIDMuNS0yLjNoLjl2MS45aC0uNWMtMSAwLTEuNCAwLTEuNC44IDAgLjMgMCAuNi4xIDEgMCAuMi4xLjYuMSAxIDAgMS4zIDAgMS44LTEuMyAyQzYgMTEuMiA2IDExLjcgNiAxM2MwIC40LS4xLjgtLjEgMS4yLS4xLjMtLjEuNy0uMSAxIDAgLjguMy44IDEuNC44aC41djEuOWgtLjljLTIuMSAwLTMuNS0uNi0zLjUtMi4zIDAtLjQuMS0uOS4xLTEuMy4xLS41LjEtLjkuMS0xLjMgMC0uNS0uMi0xLTEuNy0xdi0xLjl6Ii8+CiAgICA8Y2lyY2xlIGN4PSIxMSIgY3k9IjEzLjgiIHI9IjIuMSIvPgogICAgPGNpcmNsZSBjeD0iMTEiIGN5PSI4LjIiIHI9IjIuMSIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-julia: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDMyNSAzMDAiPgogIDxnIGNsYXNzPSJqcC1icmFuZDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjY2IzYzMzIj4KICAgIDxwYXRoIGQ9Ik0gMTUwLjg5ODQzOCAyMjUgQyAxNTAuODk4NDM4IDI2Ni40MjE4NzUgMTE3LjMyMDMxMiAzMDAgNzUuODk4NDM4IDMwMCBDIDM0LjQ3NjU2MiAzMDAgMC44OTg0MzggMjY2LjQyMTg3NSAwLjg5ODQzOCAyMjUgQyAwLjg5ODQzOCAxODMuNTc4MTI1IDM0LjQ3NjU2MiAxNTAgNzUuODk4NDM4IDE1MCBDIDExNy4zMjAzMTIgMTUwIDE1MC44OTg0MzggMTgzLjU3ODEyNSAxNTAuODk4NDM4IDIyNSIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzM4OTgyNiI+CiAgICA8cGF0aCBkPSJNIDIzNy41IDc1IEMgMjM3LjUgMTE2LjQyMTg3NSAyMDMuOTIxODc1IDE1MCAxNjIuNSAxNTAgQyAxMjEuMDc4MTI1IDE1MCA4Ny41IDExNi40MjE4NzUgODcuNSA3NSBDIDg3LjUgMzMuNTc4MTI1IDEyMS4wNzgxMjUgMCAxNjIuNSAwIEMgMjAzLjkyMTg3NSAwIDIzNy41IDMzLjU3ODEyNSAyMzcuNSA3NSIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzk1NThiMiI+CiAgICA8cGF0aCBkPSJNIDMyNC4xMDE1NjIgMjI1IEMgMzI0LjEwMTU2MiAyNjYuNDIxODc1IDI5MC41MjM0MzggMzAwIDI0OS4xMDE1NjIgMzAwIEMgMjA3LjY3OTY4OCAzMDAgMTc0LjEwMTU2MiAyNjYuNDIxODc1IDE3NC4xMDE1NjIgMjI1IEMgMTc0LjEwMTU2MiAxODMuNTc4MTI1IDIwNy42Nzk2ODggMTUwIDI0OS4xMDE1NjIgMTUwIEMgMjkwLjUyMzQzOCAxNTAgMzI0LjEwMTU2MiAxODMuNTc4MTI1IDMyNC4xMDE1NjIgMjI1Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-jupyter-favicon: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTUyIiBoZWlnaHQ9IjE2NSIgdmlld0JveD0iMCAwIDE1MiAxNjUiIHZlcnNpb249IjEuMSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgPGcgY2xhc3M9ImpwLWp1cHl0ZXItaWNvbi1jb2xvciIgZmlsbD0iI0YzNzcyNiI+CiAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjA3ODk0NywgMTEwLjU4MjkyNykiIGQ9Ik03NS45NDIyODQyLDI5LjU4MDQ1NjEgQzQzLjMwMjM5NDcsMjkuNTgwNDU2MSAxNC43OTY3ODMyLDE3LjY1MzQ2MzQgMCwwIEM1LjUxMDgzMjExLDE1Ljg0MDY4MjkgMTUuNzgxNTM4OSwyOS41NjY3NzMyIDI5LjM5MDQ5NDcsMzkuMjc4NDE3MSBDNDIuOTk5Nyw0OC45ODk4NTM3IDU5LjI3MzcsNTQuMjA2NzgwNSA3NS45NjA1Nzg5LDU0LjIwNjc4MDUgQzkyLjY0NzQ1NzksNTQuMjA2NzgwNSAxMDguOTIxNDU4LDQ4Ljk4OTg1MzcgMTIyLjUzMDY2MywzOS4yNzg0MTcxIEMxMzYuMTM5NDUzLDI5LjU2Njc3MzIgMTQ2LjQxMDI4NCwxNS44NDA2ODI5IDE1MS45MjExNTgsMCBDMTM3LjA4Nzg2OCwxNy42NTM0NjM0IDEwOC41ODI1ODksMjkuNTgwNDU2MSA3NS45NDIyODQyLDI5LjU4MDQ1NjEgTDc1Ljk0MjI4NDIsMjkuNTgwNDU2MSBaIiAvPgogICAgPHBhdGggdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC4wMzczNjgsIDAuNzA0ODc4KSIgZD0iTTc1Ljk3ODQ1NzksMjQuNjI2NDA3MyBDMTA4LjYxODc2MywyNC42MjY0MDczIDEzNy4xMjQ0NTgsMzYuNTUzNDQxNSAxNTEuOTIxMTU4LDU0LjIwNjc4MDUgQzE0Ni40MTAyODQsMzguMzY2MjIyIDEzNi4xMzk0NTMsMjQuNjQwMTMxNyAxMjIuNTMwNjYzLDE0LjkyODQ4NzggQzEwOC45MjE0NTgsNS4yMTY4NDM5IDkyLjY0NzQ1NzksMCA3NS45NjA1Nzg5LDAgQzU5LjI3MzcsMCA0Mi45OTk3LDUuMjE2ODQzOSAyOS4zOTA0OTQ3LDE0LjkyODQ4NzggQzE1Ljc4MTUzODksMjQuNjQwMTMxNyA1LjUxMDgzMjExLDM4LjM2NjIyMiAwLDU0LjIwNjc4MDUgQzE0LjgzMzA4MTYsMzYuNTg5OTI5MyA0My4zMzg1Njg0LDI0LjYyNjQwNzMgNzUuOTc4NDU3OSwyNC42MjY0MDczIEw3NS45Nzg0NTc5LDI0LjYyNjQwNzMgWiIgLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-jupyter: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMzkiIGhlaWdodD0iNTEiIHZpZXdCb3g9IjAgMCAzOSA1MSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMTYzOCAtMjI4MSkiPgogICAgIDxnIGNsYXNzPSJqcC1qdXB5dGVyLWljb24tY29sb3IiIGZpbGw9IiNGMzc3MjYiPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM5Ljc0IDIzMTEuOTgpIiBkPSJNIDE4LjI2NDYgNy4xMzQxMUMgMTAuNDE0NSA3LjEzNDExIDMuNTU4NzIgNC4yNTc2IDAgMEMgMS4zMjUzOSAzLjgyMDQgMy43OTU1NiA3LjEzMDgxIDcuMDY4NiA5LjQ3MzAzQyAxMC4zNDE3IDExLjgxNTIgMTQuMjU1NyAxMy4wNzM0IDE4LjI2OSAxMy4wNzM0QyAyMi4yODIzIDEzLjA3MzQgMjYuMTk2MyAxMS44MTUyIDI5LjQ2OTQgOS40NzMwM0MgMzIuNzQyNCA3LjEzMDgxIDM1LjIxMjYgMy44MjA0IDM2LjUzOCAwQyAzMi45NzA1IDQuMjU3NiAyNi4xMTQ4IDcuMTM0MTEgMTguMjY0NiA3LjEzNDExWiIvPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM5LjczIDIyODUuNDgpIiBkPSJNIDE4LjI3MzMgNS45MzkzMUMgMjYuMTIzNSA1LjkzOTMxIDMyLjk3OTMgOC44MTU4MyAzNi41MzggMTMuMDczNEMgMzUuMjEyNiA5LjI1MzAzIDMyLjc0MjQgNS45NDI2MiAyOS40Njk0IDMuNjAwNEMgMjYuMTk2MyAxLjI1ODE4IDIyLjI4MjMgMCAxOC4yNjkgMEMgMTQuMjU1NyAwIDEwLjM0MTcgMS4yNTgxOCA3LjA2ODYgMy42MDA0QyAzLjc5NTU2IDUuOTQyNjIgMS4zMjUzOSA5LjI1MzAzIDAgMTMuMDczNEMgMy41Njc0NSA4LjgyNDYzIDEwLjQyMzIgNS45MzkzMSAxOC4yNzMzIDUuOTM5MzFaIi8+CiAgICA8L2c+CiAgICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjY5LjMgMjI4MS4zMSkiIGQ9Ik0gNS44OTM1MyAyLjg0NEMgNS45MTg4OSAzLjQzMTY1IDUuNzcwODUgNC4wMTM2NyA1LjQ2ODE1IDQuNTE2NDVDIDUuMTY1NDUgNS4wMTkyMiA0LjcyMTY4IDUuNDIwMTUgNC4xOTI5OSA1LjY2ODUxQyAzLjY2NDMgNS45MTY4OCAzLjA3NDQ0IDYuMDAxNTEgMi40OTgwNSA1LjkxMTcxQyAxLjkyMTY2IDUuODIxOSAxLjM4NDYzIDUuNTYxNyAwLjk1NDg5OCA1LjE2NDAxQyAwLjUyNTE3IDQuNzY2MzMgMC4yMjIwNTYgNC4yNDkwMyAwLjA4MzkwMzcgMy42Nzc1N0MgLTAuMDU0MjQ4MyAzLjEwNjExIC0wLjAyMTIzIDIuNTA2MTcgMC4xNzg3ODEgMS45NTM2NEMgMC4zNzg3OTMgMS40MDExIDAuNzM2ODA5IDAuOTIwODE3IDEuMjA3NTQgMC41NzM1MzhDIDEuNjc4MjYgMC4yMjYyNTkgMi4yNDA1NSAwLjAyNzU5MTkgMi44MjMyNiAwLjAwMjY3MjI5QyAzLjYwMzg5IC0wLjAzMDcxMTUgNC4zNjU3MyAwLjI0OTc4OSA0Ljk0MTQyIDAuNzgyNTUxQyA1LjUxNzExIDEuMzE1MzEgNS44NTk1NiAyLjA1Njc2IDUuODkzNTMgMi44NDRaIi8+CiAgICAgIDxwYXRoIHRyYW5zZm9ybT0idHJhbnNsYXRlKDE2MzkuOCAyMzIzLjgxKSIgZD0iTSA3LjQyNzg5IDMuNTgzMzhDIDcuNDYwMDggNC4zMjQzIDcuMjczNTUgNS4wNTgxOSA2Ljg5MTkzIDUuNjkyMTNDIDYuNTEwMzEgNi4zMjYwNyA1Ljk1MDc1IDYuODMxNTYgNS4yODQxMSA3LjE0NDZDIDQuNjE3NDcgNy40NTc2MyAzLjg3MzcxIDcuNTY0MTQgMy4xNDcwMiA3LjQ1MDYzQyAyLjQyMDMyIDcuMzM3MTIgMS43NDMzNiA3LjAwODcgMS4yMDE4NCA2LjUwNjk1QyAwLjY2MDMyOCA2LjAwNTIgMC4yNzg2MSA1LjM1MjY4IDAuMTA1MDE3IDQuNjMyMDJDIC0wLjA2ODU3NTcgMy45MTEzNSAtMC4wMjYyMzYxIDMuMTU0OTQgMC4yMjY2NzUgMi40NTg1NkMgMC40Nzk1ODcgMS43NjIxNyAwLjkzMTY5NyAxLjE1NzEzIDEuNTI1NzYgMC43MjAwMzNDIDIuMTE5ODMgMC4yODI5MzUgMi44MjkxNCAwLjAzMzQzOTUgMy41NjM4OSAwLjAwMzEzMzQ0QyA0LjU0NjY3IC0wLjAzNzQwMzMgNS41MDUyOSAwLjMxNjcwNiA2LjIyOTYxIDAuOTg3ODM1QyA2Ljk1MzkzIDEuNjU4OTYgNy4zODQ4NCAyLjU5MjM1IDcuNDI3ODkgMy41ODMzOEwgNy40Mjc4OSAzLjU4MzM4WiIvPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM4LjM2IDIyODYuMDYpIiBkPSJNIDIuMjc0NzEgNC4zOTYyOUMgMS44NDM2MyA0LjQxNTA4IDEuNDE2NzEgNC4zMDQ0NSAxLjA0Nzk5IDQuMDc4NDNDIDAuNjc5MjY4IDMuODUyNCAwLjM4NTMyOCAzLjUyMTE0IDAuMjAzMzcxIDMuMTI2NTZDIDAuMDIxNDEzNiAyLjczMTk4IC0wLjA0MDM3OTggMi4yOTE4MyAwLjAyNTgxMTYgMS44NjE4MUMgMC4wOTIwMDMxIDEuNDMxOCAwLjI4MzIwNCAxLjAzMTI2IDAuNTc1MjEzIDAuNzEwODgzQyAwLjg2NzIyMiAwLjM5MDUxIDEuMjQ2OTEgMC4xNjQ3MDggMS42NjYyMiAwLjA2MjA1OTJDIDIuMDg1NTMgLTAuMDQwNTg5NyAyLjUyNTYxIC0wLjAxNTQ3MTQgMi45MzA3NiAwLjEzNDIzNUMgMy4zMzU5MSAwLjI4Mzk0MSAzLjY4NzkyIDAuNTUxNTA1IDMuOTQyMjIgMC45MDMwNkMgNC4xOTY1MiAxLjI1NDYyIDQuMzQxNjkgMS42NzQzNiA0LjM1OTM1IDIuMTA5MTZDIDQuMzgyOTkgMi42OTEwNyA0LjE3Njc4IDMuMjU4NjkgMy43ODU5NyAzLjY4NzQ2QyAzLjM5NTE2IDQuMTE2MjQgMi44NTE2NiA0LjM3MTE2IDIuMjc0NzEgNC4zOTYyOUwgMi4yNzQ3MSA0LjM5NjI5WiIvPgogICAgPC9nPgogIDwvZz4+Cjwvc3ZnPgo=);
  --jp-icon-jupyterlab-wordmark: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyMDAiIHZpZXdCb3g9IjAgMCAxODYwLjggNDc1Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0RTRFNEUiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDQ4MC4xMzY0MDEsIDY0LjI3MTQ5MykiPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC4wMDAwMDAsIDU4Ljg3NTU2NikiPgogICAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjA4NzYwMywgMC4xNDAyOTQpIj4KICAgICAgICA8cGF0aCBkPSJNLTQyNi45LDE2OS44YzAsNDguNy0zLjcsNjQuNy0xMy42LDc2LjRjLTEwLjgsMTAtMjUsMTUuNS0zOS43LDE1LjVsMy43LDI5IGMyMi44LDAuMyw0NC44LTcuOSw2MS45LTIzLjFjMTcuOC0xOC41LDI0LTQ0LjEsMjQtODMuM1YwSC00Mjd2MTcwLjFMLTQyNi45LDE2OS44TC00MjYuOSwxNjkuOHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMTU1LjA0NTI5NiwgNTYuODM3MTA0KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEuNTYyNDUzLCAxLjc5OTg0MikiPgogICAgICAgIDxwYXRoIGQ9Ik0tMzEyLDE0OGMwLDIxLDAsMzkuNSwxLjcsNTUuNGgtMzEuOGwtMi4xLTMzLjNoLTAuOGMtNi43LDExLjYtMTYuNCwyMS4zLTI4LDI3LjkgYy0xMS42LDYuNi0yNC44LDEwLTM4LjIsOS44Yy0zMS40LDAtNjktMTcuNy02OS04OVYwaDM2LjR2MTEyLjdjMCwzOC43LDExLjYsNjQuNyw0NC42LDY0LjdjMTAuMy0wLjIsMjAuNC0zLjUsMjguOS05LjQgYzguNS01LjksMTUuMS0xNC4zLDE4LjktMjMuOWMyLjItNi4xLDMuMy0xMi41LDMuMy0xOC45VjAuMmgzNi40VjE0OEgtMzEyTC0zMTIsMTQ4eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgzOTAuMDEzMzIyLCA1My40Nzk2MzgpIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMS43MDY0NTgsIDAuMjMxNDI1KSI+CiAgICAgICAgPHBhdGggZD0iTS00NzguNiw3MS40YzAtMjYtMC44LTQ3LTEuNy02Ni43aDMyLjdsMS43LDM0LjhoMC44YzcuMS0xMi41LDE3LjUtMjIuOCwzMC4xLTI5LjcgYzEyLjUtNywyNi43LTEwLjMsNDEtOS44YzQ4LjMsMCw4NC43LDQxLjcsODQuNywxMDMuM2MwLDczLjEtNDMuNywxMDkuMi05MSwxMDkuMmMtMTIuMSwwLjUtMjQuMi0yLjItMzUtNy44IGMtMTAuOC01LjYtMTkuOS0xMy45LTI2LjYtMjQuMmgtMC44VjI5MWgtMzZ2LTIyMEwtNDc4LjYsNzEuNEwtNDc4LjYsNzEuNHogTS00NDIuNiwxMjUuNmMwLjEsNS4xLDAuNiwxMC4xLDEuNywxNS4xIGMzLDEyLjMsOS45LDIzLjMsMTkuOCwzMS4xYzkuOSw3LjgsMjIuMSwxMi4xLDM0LjcsMTIuMWMzOC41LDAsNjAuNy0zMS45LDYwLjctNzguNWMwLTQwLjctMjEuMS03NS42LTU5LjUtNzUuNiBjLTEyLjksMC40LTI1LjMsNS4xLTM1LjMsMTMuNGMtOS45LDguMy0xNi45LDE5LjctMTkuNiwzMi40Yy0xLjUsNC45LTIuMywxMC0yLjUsMTUuMVYxMjUuNkwtNDQyLjYsMTI1LjZMLTQ0Mi42LDEyNS42eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSg2MDYuNzQwNzI2LCA1Ni44MzcxMDQpIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC43NTEyMjYsIDEuOTg5Mjk5KSI+CiAgICAgICAgPHBhdGggZD0iTS00NDAuOCwwbDQzLjcsMTIwLjFjNC41LDEzLjQsOS41LDI5LjQsMTIuOCw0MS43aDAuOGMzLjctMTIuMiw3LjktMjcuNywxMi44LTQyLjQgbDM5LjctMTE5LjJoMzguNUwtMzQ2LjksMTQ1Yy0yNiw2OS43LTQzLjcsMTA1LjQtNjguNiwxMjcuMmMtMTIuNSwxMS43LTI3LjksMjAtNDQuNiwyMy45bC05LjEtMzEuMSBjMTEuNy0zLjksMjIuNS0xMC4xLDMxLjgtMTguMWMxMy4yLTExLjEsMjMuNy0yNS4yLDMwLjYtNDEuMmMxLjUtMi44LDIuNS01LjcsMi45LTguOGMtMC4zLTMuMy0xLjItNi42LTIuNS05LjdMLTQ4MC4yLDAuMSBoMzkuN0wtNDQwLjgsMEwtNDQwLjgsMHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoODIyLjc0ODEwNCwgMC4wMDAwMDApIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMS40NjQwNTAsIDAuMzc4OTE0KSI+CiAgICAgICAgPHBhdGggZD0iTS00MTMuNywwdjU4LjNoNTJ2MjguMmgtNTJWMTk2YzAsMjUsNywzOS41LDI3LjMsMzkuNWM3LjEsMC4xLDE0LjItMC43LDIxLjEtMi41IGwxLjcsMjcuN2MtMTAuMywzLjctMjEuMyw1LjQtMzIuMiw1Yy03LjMsMC40LTE0LjYtMC43LTIxLjMtMy40Yy02LjgtMi43LTEyLjktNi44LTE3LjktMTIuMWMtMTAuMy0xMC45LTE0LjEtMjktMTQuMS01Mi45IFY4Ni41aC0zMVY1OC4zaDMxVjkuNkwtNDEzLjcsMEwtNDEzLjcsMHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOTc0LjQzMzI4NiwgNTMuNDc5NjM4KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDAuOTkwMDM0LCAwLjYxMDMzOSkiPgogICAgICAgIDxwYXRoIGQ9Ik0tNDQ1LjgsMTEzYzAuOCw1MCwzMi4yLDcwLjYsNjguNiw3MC42YzE5LDAuNiwzNy45LTMsNTUuMy0xMC41bDYuMiwyNi40IGMtMjAuOSw4LjktNDMuNSwxMy4xLTY2LjIsMTIuNmMtNjEuNSwwLTk4LjMtNDEuMi05OC4zLTEwMi41Qy00ODAuMiw0OC4yLTQ0NC43LDAtMzg2LjUsMGM2NS4yLDAsODIuNyw1OC4zLDgyLjcsOTUuNyBjLTAuMSw1LjgtMC41LDExLjUtMS4yLDE3LjJoLTE0MC42SC00NDUuOEwtNDQ1LjgsMTEzeiBNLTMzOS4yLDg2LjZjMC40LTIzLjUtOS41LTYwLjEtNTAuNC02MC4xIGMtMzYuOCwwLTUyLjgsMzQuNC01NS43LDYwLjFILTMzOS4yTC0zMzkuMiw4Ni42TC0zMzkuMiw4Ni42eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxMjAxLjk2MTA1OCwgNTMuNDc5NjM4KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEuMTc5NjQwLCAwLjcwNTA2OCkiPgogICAgICAgIDxwYXRoIGQ9Ik0tNDc4LjYsNjhjMC0yMy45LTAuNC00NC41LTEuNy02My40aDMxLjhsMS4yLDM5LjloMS43YzkuMS0yNy4zLDMxLTQ0LjUsNTUuMy00NC41IGMzLjUtMC4xLDcsMC40LDEwLjMsMS4ydjM0LjhjLTQuMS0wLjktOC4yLTEuMy0xMi40LTEuMmMtMjUuNiwwLTQzLjcsMTkuNy00OC43LDQ3LjRjLTEsNS43LTEuNiwxMS41LTEuNywxNy4ydjEwOC4zaC0zNlY2OCBMLTQ3OC42LDY4eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbi13YXJuMCIgZmlsbD0iI0YzNzcyNiI+CiAgICA8cGF0aCBkPSJNMTM1Mi4zLDMyNi4yaDM3VjI4aC0zN1YzMjYuMnogTTE2MDQuOCwzMjYuMmMtMi41LTEzLjktMy40LTMxLjEtMy40LTQ4Ljd2LTc2IGMwLTQwLjctMTUuMS04My4xLTc3LjMtODMuMWMtMjUuNiwwLTUwLDcuMS02Ni44LDE4LjFsOC40LDI0LjRjMTQuMy05LjIsMzQtMTUuMSw1My0xNS4xYzQxLjYsMCw0Ni4yLDMwLjIsNDYuMiw0N3Y0LjIgYy03OC42LTAuNC0xMjIuMywyNi41LTEyMi4zLDc1LjZjMCwyOS40LDIxLDU4LjQsNjIuMiw1OC40YzI5LDAsNTAuOS0xNC4zLDYyLjItMzAuMmgxLjNsMi45LDI1LjZIMTYwNC44eiBNMTU2NS43LDI1Ny43IGMwLDMuOC0wLjgsOC0yLjEsMTEuOGMtNS45LDE3LjItMjIuNywzNC00OS4yLDM0Yy0xOC45LDAtMzQuOS0xMS4zLTM0LjktMzUuM2MwLTM5LjUsNDUuOC00Ni42LDg2LjItNDUuOFYyNTcuN3ogTTE2OTguNSwzMjYuMiBsMS43LTMzLjZoMS4zYzE1LjEsMjYuOSwzOC43LDM4LjIsNjguMSwzOC4yYzQ1LjQsMCw5MS4yLTM2LjEsOTEuMi0xMDguOGMwLjQtNjEuNy0zNS4zLTEwMy43LTg1LjctMTAzLjcgYy0zMi44LDAtNTYuMywxNC43LTY5LjMsMzcuNGgtMC44VjI4aC0zNi42djI0NS43YzAsMTguMS0wLjgsMzguNi0xLjcsNTIuNUgxNjk4LjV6IE0xNzA0LjgsMjA4LjJjMC01LjksMS4zLTEwLjksMi4xLTE1LjEgYzcuNi0yOC4xLDMxLjEtNDUuNCw1Ni4zLTQ1LjRjMzkuNSwwLDYwLjUsMzQuOSw2MC41LDc1LjZjMCw0Ni42LTIzLjEsNzguMS02MS44LDc4LjFjLTI2LjksMC00OC4zLTE3LjYtNTUuNS00My4zIGMtMC44LTQuMi0xLjctOC44LTEuNy0xMy40VjIwOC4yeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-kernel: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgZmlsbD0iIzYxNjE2MSIgZD0iTTE1IDlIOXY2aDZWOXptLTIgNGgtMnYtMmgydjJ6bTgtMlY5aC0yVjdjMC0xLjEtLjktMi0yLTJoLTJWM2gtMnYyaC0yVjNIOXYySDdjLTEuMSAwLTIgLjktMiAydjJIM3YyaDJ2MkgzdjJoMnYyYzAgMS4xLjkgMiAyIDJoMnYyaDJ2LTJoMnYyaDJ2LTJoMmMxLjEgMCAyLS45IDItMnYtMmgydi0yaC0ydi0yaDJ6bS00IDZIN1Y3aDEwdjEweiIvPgo8L3N2Zz4K);
  --jp-icon-keyboard: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMjAgNUg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMTdjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY3YzAtMS4xLS45LTItMi0yem0tOSAzaDJ2MmgtMlY4em0wIDNoMnYyaC0ydi0yek04IDhoMnYySDhWOHptMCAzaDJ2Mkg4di0yem0tMSAySDV2LTJoMnYyem0wLTNINVY4aDJ2MnptOSA3SDh2LTJoOHYyem0wLTRoLTJ2LTJoMnYyem0wLTNoLTJWOGgydjJ6bTMgM2gtMnYtMmgydjJ6bTAtM2gtMlY4aDJ2MnoiLz4KPC9zdmc+Cg==);
  --jp-icon-launch: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMzIgMzIiIHdpZHRoPSIzMiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0yNiwyOEg2YTIuMDAyNywyLjAwMjcsMCwwLDEtMi0yVjZBMi4wMDI3LDIuMDAyNywwLDAsMSw2LDRIMTZWNkg2VjI2SDI2VjE2aDJWMjZBMi4wMDI3LDIuMDAyNywwLDAsMSwyNiwyOFoiLz4KICAgIDxwb2x5Z29uIHBvaW50cz0iMjAgMiAyMCA0IDI2LjU4NiA0IDE4IDEyLjU4NiAxOS40MTQgMTQgMjggNS40MTQgMjggMTIgMzAgMTIgMzAgMiAyMCAyIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-launcher: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkgMTlINVY1aDdWM0g1YTIgMiAwIDAwLTIgMnYxNGEyIDIgMCAwMDIgMmgxNGMxLjEgMCAyLS45IDItMnYtN2gtMnY3ek0xNCAzdjJoMy41OWwtOS44MyA5LjgzIDEuNDEgMS40MUwxOSA2LjQxVjEwaDJWM2gtN3oiLz4KPC9zdmc+Cg==);
  --jp-icon-line-form: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGZpbGw9IndoaXRlIiBkPSJNNS44OCA0LjEyTDEzLjc2IDEybC03Ljg4IDcuODhMOCAyMmwxMC0xMEw4IDJ6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-link: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTMuOSAxMmMwLTEuNzEgMS4zOS0zLjEgMy4xLTMuMWg0VjdIN2MtMi43NiAwLTUgMi4yNC01IDVzMi4yNCA1IDUgNWg0di0xLjlIN2MtMS43MSAwLTMuMS0xLjM5LTMuMS0zLjF6TTggMTNoOHYtMkg4djJ6bTktNmgtNHYxLjloNGMxLjcxIDAgMy4xIDEuMzkgMy4xIDMuMXMtMS4zOSAzLjEtMy4xIDMuMWgtNFYxN2g0YzIuNzYgMCA1LTIuMjQgNS01cy0yLjI0LTUtNS01eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-list: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xOSA1djE0SDVWNWgxNG0xLjEtMkgzLjljLS41IDAtLjkuNC0uOS45djE2LjJjMCAuNC40LjkuOS45aDE2LjJjLjQgMCAuOS0uNS45LS45VjMuOWMwLS41LS41LS45LS45LS45ek0xMSA3aDZ2MmgtNlY3em0wIDRoNnYyaC02di0yem0wIDRoNnYyaC02ek03IDdoMnYySDd6bTAgNGgydjJIN3ptMCA0aDJ2Mkg3eiIvPgo8L3N2Zz4K);
  --jp-icon-markdown: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjN0IxRkEyIiBkPSJNNSAxNC45aDEybC02LjEgNnptOS40LTYuOGMwLTEuMy0uMS0yLjktLjEtNC41LS40IDEuNC0uOSAyLjktMS4zIDQuM2wtMS4zIDQuM2gtMkw4LjUgNy45Yy0uNC0xLjMtLjctMi45LTEtNC4zLS4xIDEuNi0uMSAzLjItLjIgNC42TDcgMTIuNEg0LjhsLjctMTFoMy4zTDEwIDVjLjQgMS4yLjcgMi43IDEgMy45LjMtMS4yLjctMi42IDEtMy45bDEuMi0zLjdoMy4zbC42IDExaC0yLjRsLS4zLTQuMnoiLz4KPC9zdmc+Cg==);
  --jp-icon-move-down: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBkPSJNMTIuNDcxIDcuNTI4OTlDMTIuNzYzMiA3LjIzNjg0IDEyLjc2MzIgNi43NjMxNiAxMi40NzEgNi40NzEwMVY2LjQ3MTAxQzEyLjE3OSA2LjE3OTA1IDExLjcwNTcgNi4xNzg4NCAxMS40MTM1IDYuNDcwNTRMNy43NSAxMC4xMjc1VjEuNzVDNy43NSAxLjMzNTc5IDcuNDE0MjEgMSA3IDFWMUM2LjU4NTc5IDEgNi4yNSAxLjMzNTc5IDYuMjUgMS43NVYxMC4xMjc1TDIuNTk3MjYgNi40NjgyMkMyLjMwMzM4IDYuMTczODEgMS44MjY0MSA2LjE3MzU5IDEuNTMyMjYgNi40Njc3NFY2LjQ2Nzc0QzEuMjM4MyA2Ljc2MTcgMS4yMzgzIDcuMjM4MyAxLjUzMjI2IDcuNTMyMjZMNi4yOTI4OSAxMi4yOTI5QzYuNjgzNDIgMTIuNjgzNCA3LjMxNjU4IDEyLjY4MzQgNy43MDcxMSAxMi4yOTI5TDEyLjQ3MSA3LjUyODk5WiIgZmlsbD0iIzYxNjE2MSIvPgo8L3N2Zz4K);
  --jp-icon-move-up: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTQiIGhlaWdodD0iMTQiIHZpZXdCb3g9IjAgMCAxNCAxNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggY2xhc3M9ImpwLWljb24zIiBkPSJNMS41Mjg5OSA2LjQ3MTAxQzEuMjM2ODQgNi43NjMxNiAxLjIzNjg0IDcuMjM2ODQgMS41Mjg5OSA3LjUyODk5VjcuNTI4OTlDMS44MjA5NSA3LjgyMDk1IDIuMjk0MjYgNy44MjExNiAyLjU4NjQ5IDcuNTI5NDZMNi4yNSAzLjg3MjVWMTIuMjVDNi4yNSAxMi42NjQyIDYuNTg1NzkgMTMgNyAxM1YxM0M3LjQxNDIxIDEzIDcuNzUgMTIuNjY0MiA3Ljc1IDEyLjI1VjMuODcyNUwxMS40MDI3IDcuNTMxNzhDMTEuNjk2NiA3LjgyNjE5IDEyLjE3MzYgNy44MjY0MSAxMi40Njc3IDcuNTMyMjZWNy41MzIyNkMxMi43NjE3IDcuMjM4MyAxMi43NjE3IDYuNzYxNyAxMi40Njc3IDYuNDY3NzRMNy43MDcxMSAxLjcwNzExQzcuMzE2NTggMS4zMTY1OCA2LjY4MzQyIDEuMzE2NTggNi4yOTI4OSAxLjcwNzExTDEuNTI4OTkgNi40NzEwMVoiIGZpbGw9IiM2MTYxNjEiLz4KPC9zdmc+Cg==);
  --jp-icon-new-folder: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwIDZoLThsLTItMkg0Yy0xLjExIDAtMS45OS44OS0xLjk5IDJMMiAxOGMwIDEuMTEuODkgMiAyIDJoMTZjMS4xMSAwIDItLjg5IDItMlY4YzAtMS4xMS0uODktMi0yLTJ6bS0xIDhoLTN2M2gtMnYtM2gtM3YtMmgzVjloMnYzaDN2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-not-trusted: url(data:image/svg+xml;base64,PHN2ZyBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI1IDI1Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDMgMykiIGQ9Ik0xLjg2MDk0IDExLjQ0MDlDMC44MjY0NDggOC43NzAyNyAwLjg2Mzc3OSA2LjA1NzY0IDEuMjQ5MDcgNC4xOTkzMkMyLjQ4MjA2IDMuOTMzNDcgNC4wODA2OCAzLjQwMzQ3IDUuNjAxMDIgMi44NDQ5QzcuMjM1NDkgMi4yNDQ0IDguODU2NjYgMS41ODE1IDkuOTg3NiAxLjA5NTM5QzExLjA1OTcgMS41ODM0MSAxMi42MDk0IDIuMjQ0NCAxNC4yMTggMi44NDMzOUMxNS43NTAzIDMuNDEzOTQgMTcuMzk5NSAzLjk1MjU4IDE4Ljc1MzkgNC4yMTM4NUMxOS4xMzY0IDYuMDcxNzcgMTkuMTcwOSA4Ljc3NzIyIDE4LjEzOSAxMS40NDA5QzE3LjAzMDMgMTQuMzAzMiAxNC42NjY4IDE3LjE4NDQgOS45OTk5OSAxOC45MzU0QzUuMzMzMTkgMTcuMTg0NCAyLjk2OTY4IDE0LjMwMzIgMS44NjA5NCAxMS40NDA5WiIvPgogICAgPHBhdGggY2xhc3M9ImpwLWljb24yIiBzdHJva2U9IiMzMzMzMzMiIHN0cm9rZS13aWR0aD0iMiIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOS4zMTU5MiA5LjMyMDMxKSIgZD0iTTcuMzY4NDIgMEwwIDcuMzY0NzkiLz4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDkuMzE1OTIgMTYuNjgzNikgc2NhbGUoMSAtMSkiIGQ9Ik03LjM2ODQyIDBMMCA3LjM2NDc5Ii8+Cjwvc3ZnPgo=);
  --jp-icon-notebook: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtbm90ZWJvb2staWNvbi1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNFRjZDMDAiPgogICAgPHBhdGggZD0iTTE4LjcgMy4zdjE1LjRIMy4zVjMuM2gxNS40bTEuNS0xLjVIMS44djE4LjNoMTguM2wuMS0xOC4zeiIvPgogICAgPHBhdGggZD0iTTE2LjUgMTYuNWwtNS40LTQuMy01LjYgNC4zdi0xMWgxMXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-numbering: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjIiIGhlaWdodD0iMjIiIHZpZXdCb3g9IjAgMCAyOCAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTQgMTlINlYxOS41SDVWMjAuNUg2VjIxSDRWMjJIN1YxOEg0VjE5Wk01IDEwSDZWNkg0VjdINVYxMFpNNCAxM0g1LjhMNCAxNS4xVjE2SDdWMTVINS4yTDcgMTIuOVYxMkg0VjEzWk05IDdWOUgyM1Y3SDlaTTkgMjFIMjNWMTlIOVYyMVpNOSAxNUgyM1YxM0g5VjE1WiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-offline-bolt: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyIDIuMDJjLTUuNTEgMC05Ljk4IDQuNDctOS45OCA5Ljk4czQuNDcgOS45OCA5Ljk4IDkuOTggOS45OC00LjQ3IDkuOTgtOS45OFMxNy41MSAyLjAyIDEyIDIuMDJ6TTExLjQ4IDIwdi02LjI2SDhMMTMgNHY2LjI2aDMuMzVMMTEuNDggMjB6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-palette: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE4IDEzVjIwSDRWNkg5LjAyQzkuMDcgNS4yOSA5LjI0IDQuNjIgOS41IDRINEMyLjkgNCAyIDQuOSAyIDZWMjBDMiAyMS4xIDIuOSAyMiA0IDIySDE4QzE5LjEgMjIgMjAgMjEuMSAyMCAyMFYxNUwxOCAxM1pNMTkuMyA4Ljg5QzE5Ljc0IDguMTkgMjAgNy4zOCAyMCA2LjVDMjAgNC4wMSAxNy45OSAyIDE1LjUgMkMxMy4wMSAyIDExIDQuMDEgMTEgNi41QzExIDguOTkgMTMuMDEgMTEgMTUuNDkgMTFDMTYuMzcgMTEgMTcuMTkgMTAuNzQgMTcuODggMTAuM0wyMSAxMy40MkwyMi40MiAxMkwxOS4zIDguODlaTTE1LjUgOUMxNC4xMiA5IDEzIDcuODggMTMgNi41QzEzIDUuMTIgMTQuMTIgNCAxNS41IDRDMTYuODggNCAxOCA1LjEyIDE4IDYuNUMxOCA3Ljg4IDE2Ljg4IDkgMTUuNSA5WiIvPgogICAgPHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBjbGlwLXJ1bGU9ImV2ZW5vZGQiIGQ9Ik00IDZIOS4wMTg5NEM5LjAwNjM5IDYuMTY1MDIgOSA2LjMzMTc2IDkgNi41QzkgOC44MTU3NyAxMC4yMTEgMTAuODQ4NyAxMi4wMzQzIDEySDlWMTRIMTZWMTIuOTgxMUMxNi41NzAzIDEyLjkzNzcgMTcuMTIgMTIuODIwNyAxNy42Mzk2IDEyLjYzOTZMMTggMTNWMjBINFY2Wk04IDhINlYxMEg4VjhaTTYgMTJIOFYxNEg2VjEyWk04IDE2SDZWMThIOFYxNlpNOSAxNkgxNlYxOEg5VjE2WiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-paste: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTE5IDJoLTQuMThDMTQuNC44NCAxMy4zIDAgMTIgMGMtMS4zIDAtMi40Ljg0LTIuODIgMkg1Yy0xLjEgMC0yIC45LTIgMnYxNmMwIDEuMS45IDIgMiAyaDE0YzEuMSAwIDItLjkgMi0yVjRjMC0xLjEtLjktMi0yLTJ6bS03IDBjLjU1IDAgMSAuNDUgMSAxcy0uNDUgMS0xIDEtMS0uNDUtMS0xIC40NS0xIDEtMXptNyAxOEg1VjRoMnYzaDEwVjRoMnYxNnoiLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-pdf: url(data:image/svg+xml;base64,PHN2ZwogICB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyMiAyMiIgd2lkdGg9IjE2Ij4KICAgIDxwYXRoIHRyYW5zZm9ybT0icm90YXRlKDQ1KSIgY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI0ZGMkEyQSIKICAgICAgIGQ9Im0gMjIuMzQ0MzY5LC0zLjAxNjM2NDIgaCA1LjYzODYwNCB2IDEuNTc5MjQzMyBoIC0zLjU0OTIyNyB2IDEuNTA4NjkyOTkgaCAzLjMzNzU3NiBWIDEuNjUwODE1NCBoIC0zLjMzNzU3NiB2IDMuNDM1MjYxMyBoIC0yLjA4OTM3NyB6IG0gLTcuMTM2NDQ0LDEuNTc5MjQzMyB2IDQuOTQzOTU0MyBoIDAuNzQ4OTIgcSAxLjI4MDc2MSwwIDEuOTUzNzAzLC0wLjYzNDk1MzUgMC42NzgzNjksLTAuNjM0OTUzNSAwLjY3ODM2OSwtMS44NDUxNjQxIDAsLTEuMjA0NzgzNTUgLTAuNjcyOTQyLC0xLjgzNDMxMDExIC0wLjY3Mjk0MiwtMC42Mjk1MjY1OSAtMS45NTkxMywtMC42Mjk1MjY1OSB6IG0gLTIuMDg5Mzc3LC0xLjU3OTI0MzMgaCAyLjIwMzM0MyBxIDEuODQ1MTY0LDAgMi43NDYwMzksMC4yNjU5MjA3IDAuOTA2MzAxLDAuMjYwNDkzNyAxLjU1MjEwOCwwLjg5MDAyMDMgMC41Njk4MywwLjU0ODEyMjMgMC44NDY2MDUsMS4yNjQ0ODAwNiAwLjI3Njc3NCwwLjcxNjM1NzgxIDAuMjc2Nzc0LDEuNjIyNjU4OTQgMCwwLjkxNzE1NTEgLTAuMjc2Nzc0LDEuNjM4OTM5OSAtMC4yNzY3NzUsMC43MTYzNTc4IC0wLjg0NjYwNSwxLjI2NDQ4IC0wLjY1MTIzNCwwLjYyOTUyNjYgLTEuNTYyOTYyLDAuODk1NDQ3MyAtMC45MTE3MjgsMC4yNjA0OTM3IC0yLjczNTE4NSwwLjI2MDQ5MzcgaCAtMi4yMDMzNDMgeiBtIC04LjE0NTg1NjUsMCBoIDMuNDY3ODIzIHEgMS41NDY2ODE2LDAgMi4zNzE1Nzg1LDAuNjg5MjIzIDAuODMwMzI0LDAuNjgzNzk2MSAwLjgzMDMyNCwxLjk1MzcwMzE0IDAsMS4yNzUzMzM5NyAtMC44MzAzMjQsMS45NjQ1NTcwNiBRIDkuOTg3MTk2MSwyLjI3NDkxNSA4LjQ0MDUxNDUsMi4yNzQ5MTUgSCA3LjA2MjA2ODQgViA1LjA4NjA3NjcgSCA0Ljk3MjY5MTUgWiBtIDIuMDg5Mzc2OSwxLjUxNDExOTkgdiAyLjI2MzAzOTQzIGggMS4xNTU5NDEgcSAwLjYwNzgxODgsMCAwLjkzODg2MjksLTAuMjkzMDU1NDcgMC4zMzEwNDQxLC0wLjI5ODQ4MjQxIDAuMzMxMDQ0MSwtMC44NDExNzc3MiAwLC0wLjU0MjY5NTMxIC0wLjMzMTA0NDEsLTAuODM1NzUwNzQgLTAuMzMxMDQ0MSwtMC4yOTMwNTU1IC0wLjkzODg2MjksLTAuMjkzMDU1NSB6IgovPgo8L3N2Zz4K);
  --jp-icon-python: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iLTEwIC0xMCAxMzEuMTYxMzYxNjk0MzM1OTQgMTMyLjM4ODk5OTkzODk2NDg0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMzA2OTk4IiBkPSJNIDU0LjkxODc4NSw5LjE5Mjc0MjFlLTQgQyA1MC4zMzUxMzIsMC4wMjIyMTcyNyA0NS45NTc4NDYsMC40MTMxMzY5NyA0Mi4xMDYyODUsMS4wOTQ2NjkzIDMwLjc2MDA2OSwzLjA5OTE3MzEgMjguNzAwMDM2LDcuMjk0NzcxNCAyOC43MDAwMzUsMTUuMDMyMTY5IHYgMTAuMjE4NzUgaCAyNi44MTI1IHYgMy40MDYyNSBoIC0yNi44MTI1IC0xMC4wNjI1IGMgLTcuNzkyNDU5LDAgLTE0LjYxNTc1ODgsNC42ODM3MTcgLTE2Ljc0OTk5OTgsMTMuNTkzNzUgLTIuNDYxODE5OTgsMTAuMjEyOTY2IC0yLjU3MTAxNTA4LDE2LjU4NjAyMyAwLDI3LjI1IDEuOTA1OTI4Myw3LjkzNzg1MiA2LjQ1NzU0MzIsMTMuNTkzNzQ4IDE0LjI0OTk5OTgsMTMuNTkzNzUgaCA5LjIxODc1IHYgLTEyLjI1IGMgMCwtOC44NDk5MDIgNy42NTcxNDQsLTE2LjY1NjI0OCAxNi43NSwtMTYuNjU2MjUgaCAyNi43ODEyNSBjIDcuNDU0OTUxLDAgMTMuNDA2MjUzLC02LjEzODE2NCAxMy40MDYyNSwtMTMuNjI1IHYgLTI1LjUzMTI1IGMgMCwtNy4yNjYzMzg2IC02LjEyOTk4LC0xMi43MjQ3NzcxIC0xMy40MDYyNSwtMTMuOTM3NDk5NyBDIDY0LjI4MTU0OCwwLjMyNzk0Mzk3IDU5LjUwMjQzOCwtMC4wMjAzNzkwMyA1NC45MTg3ODUsOS4xOTI3NDIxZS00IFogbSAtMTQuNSw4LjIxODc1MDEyNTc5IGMgMi43Njk1NDcsMCA1LjAzMTI1LDIuMjk4NjQ1NiA1LjAzMTI1LDUuMTI0OTk5NiAtMmUtNiwyLjgxNjMzNiAtMi4yNjE3MDMsNS4wOTM3NSAtNS4wMzEyNSw1LjA5Mzc1IC0yLjc3OTQ3NiwtMWUtNiAtNS4wMzEyNSwtMi4yNzc0MTUgLTUuMDMxMjUsLTUuMDkzNzUgLTEwZS03LC0yLjgyNjM1MyAyLjI1MTc3NCwtNS4xMjQ5OTk2IDUuMDMxMjUsLTUuMTI0OTk5NiB6Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI2ZmZDQzYiIgZD0ibSA4NS42Mzc1MzUsMjguNjU3MTY5IHYgMTEuOTA2MjUgYyAwLDkuMjMwNzU1IC03LjgyNTg5NSwxNi45OTk5OTkgLTE2Ljc1LDE3IGggLTI2Ljc4MTI1IGMgLTcuMzM1ODMzLDAgLTEzLjQwNjI0OSw2LjI3ODQ4MyAtMTMuNDA2MjUsMTMuNjI1IHYgMjUuNTMxMjQ3IGMgMCw3LjI2NjM0NCA2LjMxODU4OCwxMS41NDAzMjQgMTMuNDA2MjUsMTMuNjI1MDA0IDguNDg3MzMxLDIuNDk1NjEgMTYuNjI2MjM3LDIuOTQ2NjMgMjYuNzgxMjUsMCA2Ljc1MDE1NSwtMS45NTQzOSAxMy40MDYyNTMsLTUuODg3NjEgMTMuNDA2MjUsLTEzLjYyNTAwNCBWIDg2LjUwMDkxOSBoIC0yNi43ODEyNSB2IC0zLjQwNjI1IGggMjYuNzgxMjUgMTMuNDA2MjU0IGMgNy43OTI0NjEsMCAxMC42OTYyNTEsLTUuNDM1NDA4IDEzLjQwNjI0MSwtMTMuNTkzNzUgMi43OTkzMywtOC4zOTg4ODYgMi42ODAyMiwtMTYuNDc1Nzc2IDAsLTI3LjI1IC0xLjkyNTc4LC03Ljc1NzQ0MSAtNS42MDM4NywtMTMuNTkzNzUgLTEzLjQwNjI0MSwtMTMuNTkzNzUgeiBtIC0xNS4wNjI1LDY0LjY1NjI1IGMgMi43Nzk0NzgsM2UtNiA1LjAzMTI1LDIuMjc3NDE3IDUuMDMxMjUsNS4wOTM3NDcgLTJlLTYsMi44MjYzNTQgLTIuMjUxNzc1LDUuMTI1MDA0IC01LjAzMTI1LDUuMTI1MDA0IC0yLjc2OTU1LDAgLTUuMDMxMjUsLTIuMjk4NjUgLTUuMDMxMjUsLTUuMTI1MDA0IDJlLTYsLTIuODE2MzMgMi4yNjE2OTcsLTUuMDkzNzQ3IDUuMDMxMjUsLTUuMDkzNzQ3IHoiLz4KPC9zdmc+Cg==);
  --jp-icon-r-kernel: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMjE5NkYzIiBkPSJNNC40IDIuNWMxLjItLjEgMi45LS4zIDQuOS0uMyAyLjUgMCA0LjEuNCA1LjIgMS4zIDEgLjcgMS41IDEuOSAxLjUgMy41IDAgMi0xLjQgMy41LTIuOSA0LjEgMS4yLjQgMS43IDEuNiAyLjIgMyAuNiAxLjkgMSAzLjkgMS4zIDQuNmgtMy44Yy0uMy0uNC0uOC0xLjctMS4yLTMuN3MtMS4yLTIuNi0yLjYtMi42aC0uOXY2LjRINC40VjIuNXptMy43IDYuOWgxLjRjMS45IDAgMi45LS45IDIuOS0yLjNzLTEtMi4zLTIuOC0yLjNjLS43IDAtMS4zIDAtMS42LjJ2NC41aC4xdi0uMXoiLz4KPC9zdmc+Cg==);
  --jp-icon-react: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMTUwIDE1MCA1NDEuOSAyOTUuMyI+CiAgPGcgY2xhc3M9ImpwLWljb24tYnJhbmQyIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzYxREFGQiI+CiAgICA8cGF0aCBkPSJNNjY2LjMgMjk2LjVjMC0zMi41LTQwLjctNjMuMy0xMDMuMS04Mi40IDE0LjQtNjMuNiA4LTExNC4yLTIwLjItMTMwLjQtNi41LTMuOC0xNC4xLTUuNi0yMi40LTUuNnYyMi4zYzQuNiAwIDguMy45IDExLjQgMi42IDEzLjYgNy44IDE5LjUgMzcuNSAxNC45IDc1LjctMS4xIDkuNC0yLjkgMTkuMy01LjEgMjkuNC0xOS42LTQuOC00MS04LjUtNjMuNS0xMC45LTEzLjUtMTguNS0yNy41LTM1LjMtNDEuNi01MCAzMi42LTMwLjMgNjMuMi00Ni45IDg0LTQ2LjlWNzhjLTI3LjUgMC02My41IDE5LjYtOTkuOSA1My42LTM2LjQtMzMuOC03Mi40LTUzLjItOTkuOS01My4ydjIyLjNjMjAuNyAwIDUxLjQgMTYuNSA4NCA0Ni42LTE0IDE0LjctMjggMzEuNC00MS4zIDQ5LjktMjIuNiAyLjQtNDQgNi4xLTYzLjYgMTEtMi4zLTEwLTQtMTkuNy01LjItMjktNC43LTM4LjIgMS4xLTY3LjkgMTQuNi03NS44IDMtMS44IDYuOS0yLjYgMTEuNS0yLjZWNzguNWMtOC40IDAtMTYgMS44LTIyLjYgNS42LTI4LjEgMTYuMi0zNC40IDY2LjctMTkuOSAxMzAuMS02Mi4yIDE5LjItMTAyLjcgNDkuOS0xMDIuNyA4Mi4zIDAgMzIuNSA0MC43IDYzLjMgMTAzLjEgODIuNC0xNC40IDYzLjYtOCAxMTQuMiAyMC4yIDEzMC40IDYuNSAzLjggMTQuMSA1LjYgMjIuNSA1LjYgMjcuNSAwIDYzLjUtMTkuNiA5OS45LTUzLjYgMzYuNCAzMy44IDcyLjQgNTMuMiA5OS45IDUzLjIgOC40IDAgMTYtMS44IDIyLjYtNS42IDI4LjEtMTYuMiAzNC40LTY2LjcgMTkuOS0xMzAuMSA2Mi0xOS4xIDEwMi41LTQ5LjkgMTAyLjUtODIuM3ptLTEzMC4yLTY2LjdjLTMuNyAxMi45LTguMyAyNi4yLTEzLjUgMzkuNS00LjEtOC04LjQtMTYtMTMuMS0yNC00LjYtOC05LjUtMTUuOC0xNC40LTIzLjQgMTQuMiAyLjEgMjcuOSA0LjcgNDEgNy45em0tNDUuOCAxMDYuNWMtNy44IDEzLjUtMTUuOCAyNi4zLTI0LjEgMzguMi0xNC45IDEuMy0zMCAyLTQ1LjIgMi0xNS4xIDAtMzAuMi0uNy00NS0xLjktOC4zLTExLjktMTYuNC0yNC42LTI0LjItMzgtNy42LTEzLjEtMTQuNS0yNi40LTIwLjgtMzkuOCA2LjItMTMuNCAxMy4yLTI2LjggMjAuNy0zOS45IDcuOC0xMy41IDE1LjgtMjYuMyAyNC4xLTM4LjIgMTQuOS0xLjMgMzAtMiA0NS4yLTIgMTUuMSAwIDMwLjIuNyA0NSAxLjkgOC4zIDExLjkgMTYuNCAyNC42IDI0LjIgMzggNy42IDEzLjEgMTQuNSAyNi40IDIwLjggMzkuOC02LjMgMTMuNC0xMy4yIDI2LjgtMjAuNyAzOS45em0zMi4zLTEzYzUuNCAxMy40IDEwIDI2LjggMTMuOCAzOS44LTEzLjEgMy4yLTI2LjkgNS45LTQxLjIgOCA0LjktNy43IDkuOC0xNS42IDE0LjQtMjMuNyA0LjYtOCA4LjktMTYuMSAxMy0yNC4xek00MjEuMiA0MzBjLTkuMy05LjYtMTguNi0yMC4zLTI3LjgtMzIgOSAuNCAxOC4yLjcgMjcuNS43IDkuNCAwIDE4LjctLjIgMjcuOC0uNy05IDExLjctMTguMyAyMi40LTI3LjUgMzJ6bS03NC40LTU4LjljLTE0LjItMi4xLTI3LjktNC43LTQxLTcuOSAzLjctMTIuOSA4LjMtMjYuMiAxMy41LTM5LjUgNC4xIDggOC40IDE2IDEzLjEgMjQgNC43IDggOS41IDE1LjggMTQuNCAyMy40ek00MjAuNyAxNjNjOS4zIDkuNiAxOC42IDIwLjMgMjcuOCAzMi05LS40LTE4LjItLjctMjcuNS0uNy05LjQgMC0xOC43LjItMjcuOC43IDktMTEuNyAxOC4zLTIyLjQgMjcuNS0zMnptLTc0IDU4LjljLTQuOSA3LjctOS44IDE1LjYtMTQuNCAyMy43LTQuNiA4LTguOSAxNi0xMyAyNC01LjQtMTMuNC0xMC0yNi44LTEzLjgtMzkuOCAxMy4xLTMuMSAyNi45LTUuOCA0MS4yLTcuOXptLTkwLjUgMTI1LjJjLTM1LjQtMTUuMS01OC4zLTM0LjktNTguMy01MC42IDAtMTUuNyAyMi45LTM1LjYgNTguMy01MC42IDguNi0zLjcgMTgtNyAyNy43LTEwLjEgNS43IDE5LjYgMTMuMiA0MCAyMi41IDYwLjktOS4yIDIwLjgtMTYuNiA0MS4xLTIyLjIgNjAuNi05LjktMy4xLTE5LjMtNi41LTI4LTEwLjJ6TTMxMCA0OTBjLTEzLjYtNy44LTE5LjUtMzcuNS0xNC45LTc1LjcgMS4xLTkuNCAyLjktMTkuMyA1LjEtMjkuNCAxOS42IDQuOCA0MSA4LjUgNjMuNSAxMC45IDEzLjUgMTguNSAyNy41IDM1LjMgNDEuNiA1MC0zMi42IDMwLjMtNjMuMiA0Ni45LTg0IDQ2LjktNC41LS4xLTguMy0xLTExLjMtMi43em0yMzcuMi03Ni4yYzQuNyAzOC4yLTEuMSA2Ny45LTE0LjYgNzUuOC0zIDEuOC02LjkgMi42LTExLjUgMi42LTIwLjcgMC01MS40LTE2LjUtODQtNDYuNiAxNC0xNC43IDI4LTMxLjQgNDEuMy00OS45IDIyLjYtMi40IDQ0LTYuMSA2My42LTExIDIuMyAxMC4xIDQuMSAxOS44IDUuMiAyOS4xem0zOC41LTY2LjdjLTguNiAzLjctMTggNy0yNy43IDEwLjEtNS43LTE5LjYtMTMuMi00MC0yMi41LTYwLjkgOS4yLTIwLjggMTYuNi00MS4xIDIyLjItNjAuNiA5LjkgMy4xIDE5LjMgNi41IDI4LjEgMTAuMiAzNS40IDE1LjEgNTguMyAzNC45IDU4LjMgNTAuNi0uMSAxNS43LTIzIDM1LjYtNTguNCA1MC42ek0zMjAuOCA3OC40eiIvPgogICAgPGNpcmNsZSBjeD0iNDIwLjkiIGN5PSIyOTYuNSIgcj0iNDUuNyIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-redo: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgICA8cGF0aCBkPSJNMCAwaDI0djI0SDB6IiBmaWxsPSJub25lIi8+PHBhdGggZD0iTTE4LjQgMTAuNkMxNi41NSA4Ljk5IDE0LjE1IDggMTEuNSA4Yy00LjY1IDAtOC41OCAzLjAzLTkuOTYgNy4yMkwzLjkgMTZjMS4wNS0zLjE5IDQuMDUtNS41IDcuNi01LjUgMS45NSAwIDMuNzMuNzIgNS4xMiAxLjg4TDEzIDE2aDlWN2wtMy42IDMuNnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-refresh: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTkgMTMuNWMtMi40OSAwLTQuNS0yLjAxLTQuNS00LjVTNi41MSA0LjUgOSA0LjVjMS4yNCAwIDIuMzYuNTIgMy4xNyAxLjMzTDEwIDhoNVYzbC0xLjc2IDEuNzZDMTIuMTUgMy42OCAxMC42NiAzIDkgMyA1LjY5IDMgMy4wMSA1LjY5IDMuMDEgOVM1LjY5IDE1IDkgMTVjMi45NyAwIDUuNDMtMi4xNiA1LjktNWgtMS41MmMtLjQ2IDItMi4yNCAzLjUtNC4zOCAzLjV6Ii8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-regex: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0MTQxNDEiPgogICAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbi1hY2NlbnQyIiBmaWxsPSIjRkZGIj4KICAgIDxjaXJjbGUgY2xhc3M9InN0MiIgY3g9IjUuNSIgY3k9IjE0LjUiIHI9IjEuNSIvPgogICAgPHJlY3QgeD0iMTIiIHk9IjQiIGNsYXNzPSJzdDIiIHdpZHRoPSIxIiBoZWlnaHQ9IjgiLz4KICAgIDxyZWN0IHg9IjguNSIgeT0iNy41IiB0cmFuc2Zvcm09Im1hdHJpeCgwLjg2NiAtMC41IDAuNSAwLjg2NiAtMi4zMjU1IDcuMzIxOSkiIGNsYXNzPSJzdDIiIHdpZHRoPSI4IiBoZWlnaHQ9IjEiLz4KICAgIDxyZWN0IHg9IjEyIiB5PSI0IiB0cmFuc2Zvcm09Im1hdHJpeCgwLjUgLTAuODY2IDAuODY2IDAuNSAtMC42Nzc5IDE0LjgyNTIpIiBjbGFzcz0ic3QyIiB3aWR0aD0iMSIgaGVpZ2h0PSI4Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-run: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTggNXYxNGwxMS03eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-running: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUxMiA1MTIiPgogIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICA8cGF0aCBkPSJNMjU2IDhDMTE5IDggOCAxMTkgOCAyNTZzMTExIDI0OCAyNDggMjQ4IDI0OC0xMTEgMjQ4LTI0OFMzOTMgOCAyNTYgOHptOTYgMzI4YzAgOC44LTcuMiAxNi0xNiAxNkgxNzZjLTguOCAwLTE2LTcuMi0xNi0xNlYxNzZjMC04LjggNy4yLTE2IDE2LTE2aDE2MGM4LjggMCAxNiA3LjIgMTYgMTZ2MTYweiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-save: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTE3IDNINWMtMS4xMSAwLTIgLjktMiAydjE0YzAgMS4xLjg5IDIgMiAyaDE0YzEuMSAwIDItLjkgMi0yVjdsLTQtNHptLTUgMTZjLTEuNjYgMC0zLTEuMzQtMy0zczEuMzQtMyAzLTMgMyAxLjM0IDMgMy0xLjM0IDMtMyAzem0zLTEwSDVWNWgxMHY0eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-search: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjEsMTAuOWgtMC43bC0wLjItMC4yYzAuOC0wLjksMS4zLTIuMiwxLjMtMy41YzAtMy0yLjQtNS40LTUuNC01LjRTMS44LDQuMiwxLjgsNy4xczIuNCw1LjQsNS40LDUuNCBjMS4zLDAsMi41LTAuNSwzLjUtMS4zbDAuMiwwLjJ2MC43bDQuMSw0LjFsMS4yLTEuMkwxMi4xLDEwLjl6IE03LjEsMTAuOWMtMi4xLDAtMy43LTEuNy0zLjctMy43czEuNy0zLjcsMy43LTMuN3MzLjcsMS43LDMuNywzLjcgUzkuMiwxMC45LDcuMSwxMC45eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-settings: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkuNDMgMTIuOThjLjA0LS4zMi4wNy0uNjQuMDctLjk4cy0uMDMtLjY2LS4wNy0uOThsMi4xMS0xLjY1Yy4xOS0uMTUuMjQtLjQyLjEyLS42NGwtMi0zLjQ2Yy0uMTItLjIyLS4zOS0uMy0uNjEtLjIybC0yLjQ5IDFjLS41Mi0uNC0xLjA4LS43My0xLjY5LS45OGwtLjM4LTIuNjVBLjQ4OC40ODggMCAwMDE0IDJoLTRjLS4yNSAwLS40Ni4xOC0uNDkuNDJsLS4zOCAyLjY1Yy0uNjEuMjUtMS4xNy41OS0xLjY5Ljk4bC0yLjQ5LTFjLS4yMy0uMDktLjQ5IDAtLjYxLjIybC0yIDMuNDZjLS4xMy4yMi0uMDcuNDkuMTIuNjRsMi4xMSAxLjY1Yy0uMDQuMzItLjA3LjY1LS4wNy45OHMuMDMuNjYuMDcuOThsLTIuMTEgMS42NWMtLjE5LjE1LS4yNC40Mi0uMTIuNjRsMiAzLjQ2Yy4xMi4yMi4zOS4zLjYxLjIybDIuNDktMWMuNTIuNCAxLjA4LjczIDEuNjkuOThsLjM4IDIuNjVjLjAzLjI0LjI0LjQyLjQ5LjQyaDRjLjI1IDAgLjQ2LS4xOC40OS0uNDJsLjM4LTIuNjVjLjYxLS4yNSAxLjE3LS41OSAxLjY5LS45OGwyLjQ5IDFjLjIzLjA5LjQ5IDAgLjYxLS4yMmwyLTMuNDZjLjEyLS4yMi4wNy0uNDktLjEyLS42NGwtMi4xMS0xLjY1ek0xMiAxNS41Yy0xLjkzIDAtMy41LTEuNTctMy41LTMuNXMxLjU3LTMuNSAzLjUtMy41IDMuNSAxLjU3IDMuNSAzLjUtMS41NyAzLjUtMy41IDMuNXoiLz4KPC9zdmc+Cg==);
  --jp-icon-share: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTSAxOCAyIEMgMTYuMzU0OTkgMiAxNSAzLjM1NDk5MDQgMTUgNSBDIDE1IDUuMTkwOTUyOSAxNS4wMjE3OTEgNS4zNzcxMjI0IDE1LjA1NjY0MSA1LjU1ODU5MzggTCA3LjkyMTg3NSA5LjcyMDcwMzEgQyA3LjM5ODUzOTkgOS4yNzc4NTM5IDYuNzMyMDc3MSA5IDYgOSBDIDQuMzU0OTkwNCA5IDMgMTAuMzU0OTkgMyAxMiBDIDMgMTMuNjQ1MDEgNC4zNTQ5OTA0IDE1IDYgMTUgQyA2LjczMjA3NzEgMTUgNy4zOTg1Mzk5IDE0LjcyMjE0NiA3LjkyMTg3NSAxNC4yNzkyOTcgTCAxNS4wNTY2NDEgMTguNDM5NDUzIEMgMTUuMDIxNTU1IDE4LjYyMTUxNCAxNSAxOC44MDgzODYgMTUgMTkgQyAxNSAyMC42NDUwMSAxNi4zNTQ5OSAyMiAxOCAyMiBDIDE5LjY0NTAxIDIyIDIxIDIwLjY0NTAxIDIxIDE5IEMgMjEgMTcuMzU0OTkgMTkuNjQ1MDEgMTYgMTggMTYgQyAxNy4yNjc0OCAxNiAxNi42MDE1OTMgMTYuMjc5MzI4IDE2LjA3ODEyNSAxNi43MjI2NTYgTCA4Ljk0MzM1OTQgMTIuNTU4NTk0IEMgOC45NzgyMDk1IDEyLjM3NzEyMiA5IDEyLjE5MDk1MyA5IDEyIEMgOSAxMS44MDkwNDcgOC45NzgyMDk1IDExLjYyMjg3OCA4Ljk0MzM1OTQgMTEuNDQxNDA2IEwgMTYuMDc4MTI1IDcuMjc5Mjk2OSBDIDE2LjYwMTQ2IDcuNzIyMTQ2MSAxNy4yNjc5MjMgOCAxOCA4IEMgMTkuNjQ1MDEgOCAyMSA2LjY0NTAwOTYgMjEgNSBDIDIxIDMuMzU0OTkwNCAxOS42NDUwMSAyIDE4IDIgeiBNIDE4IDQgQyAxOC41NjQxMjkgNCAxOSA0LjQzNTg3MDYgMTkgNSBDIDE5IDUuNTY0MTI5NCAxOC41NjQxMjkgNiAxOCA2IEMgMTcuNDM1ODcxIDYgMTcgNS41NjQxMjk0IDE3IDUgQyAxNyA0LjQzNTg3MDYgMTcuNDM1ODcxIDQgMTggNCB6IE0gNiAxMSBDIDYuNTY0MTI5NCAxMSA3IDExLjQzNTg3MSA3IDEyIEMgNyAxMi41NjQxMjkgNi41NjQxMjk0IDEzIDYgMTMgQyA1LjQzNTg3MDYgMTMgNSAxMi41NjQxMjkgNSAxMiBDIDUgMTEuNDM1ODcxIDUuNDM1ODcwNiAxMSA2IDExIHogTSAxOCAxOCBDIDE4LjU2NDEyOSAxOCAxOSAxOC40MzU4NzEgMTkgMTkgQyAxOSAxOS41NjQxMjkgMTguNTY0MTI5IDIwIDE4IDIwIEMgMTcuNDM1ODcxIDIwIDE3IDE5LjU2NDEyOSAxNyAxOSBDIDE3IDE4LjQzNTg3MSAxNy40MzU4NzEgMTggMTggMTggeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-spreadsheet: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDEganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNENBRjUwIiBkPSJNMi4yIDIuMnYxNy42aDE3LjZWMi4ySDIuMnptMTUuNCA3LjdoLTUuNVY0LjRoNS41djUuNXpNOS45IDQuNHY1LjVINC40VjQuNGg1LjV6bS01LjUgNy43aDUuNXY1LjVINC40di01LjV6bTcuNyA1LjV2LTUuNWg1LjV2NS41aC01LjV6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-stop: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik02IDZoMTJ2MTJINnoiLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-tab: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIxIDNIM2MtMS4xIDAtMiAuOS0yIDJ2MTRjMCAxLjEuOSAyIDIgMmgxOGMxLjEgMCAyLS45IDItMlY1YzAtMS4xLS45LTItMi0yem0wIDE2SDNWNWgxMHY0aDh2MTB6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-table-rows: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik0yMSw4SDNWNGgxOFY4eiBNMjEsMTBIM3Y0aDE4VjEweiBNMjEsMTZIM3Y0aDE4VjE2eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-tag: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjgiIGhlaWdodD0iMjgiIHZpZXdCb3g9IjAgMCA0MyAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTI4LjgzMzIgMTIuMzM0TDMyLjk5OTggMTYuNTAwN0wzNy4xNjY1IDEyLjMzNEgyOC44MzMyWiIvPgoJCTxwYXRoIGQ9Ik0xNi4yMDk1IDIxLjYxMDRDMTUuNjg3MyAyMi4xMjk5IDE0Ljg0NDMgMjIuMTI5OSAxNC4zMjQ4IDIxLjYxMDRMNi45ODI5IDE0LjcyNDVDNi41NzI0IDE0LjMzOTQgNi4wODMxMyAxMy42MDk4IDYuMDQ3ODYgMTMuMDQ4MkM1Ljk1MzQ3IDExLjUyODggNi4wMjAwMiA4LjYxOTQ0IDYuMDY2MjEgNy4wNzY5NUM2LjA4MjgxIDYuNTE0NzcgNi41NTU0OCA2LjA0MzQ3IDcuMTE4MDQgNi4wMzA1NUM5LjA4ODYzIDUuOTg0NzMgMTMuMjYzOCA1LjkzNTc5IDEzLjY1MTggNi4zMjQyNUwyMS43MzY5IDEzLjYzOUMyMi4yNTYgMTQuMTU4NSAyMS43ODUxIDE1LjQ3MjQgMjEuMjYyIDE1Ljk5NDZMMTYuMjA5NSAyMS42MTA0Wk05Ljc3NTg1IDguMjY1QzkuMzM1NTEgNy44MjU2NiA4LjYyMzUxIDcuODI1NjYgOC4xODI4IDguMjY1QzcuNzQzNDYgOC43MDU3MSA3Ljc0MzQ2IDkuNDE3MzMgOC4xODI4IDkuODU2NjdDOC42MjM4MiAxMC4yOTY0IDkuMzM1ODIgMTAuMjk2NCA5Ljc3NTg1IDkuODU2NjdDMTAuMjE1NiA5LjQxNzMzIDEwLjIxNTYgOC43MDUzMyA5Ljc3NTg1IDguMjY1WiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-terminal: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0IiA+CiAgICA8cmVjdCBjbGFzcz0ianAtdGVybWluYWwtaWNvbi1iYWNrZ3JvdW5kLWNvbG9yIGpwLWljb24tc2VsZWN0YWJsZSIgd2lkdGg9IjIwIiBoZWlnaHQ9IjIwIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSgyIDIpIiBmaWxsPSIjMzMzMzMzIi8+CiAgICA8cGF0aCBjbGFzcz0ianAtdGVybWluYWwtaWNvbi1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUtaW52ZXJzZSIgZD0iTTUuMDU2NjQgOC43NjE3MkM1LjA1NjY0IDguNTk3NjYgNS4wMzEyNSA4LjQ1MzEyIDQuOTgwNDcgOC4zMjgxMkM0LjkzMzU5IDguMTk5MjIgNC44NTU0NyA4LjA4MjAzIDQuNzQ2MDkgNy45NzY1NkM0LjY0MDYyIDcuODcxMDkgNC41IDcuNzc1MzkgNC4zMjQyMiA3LjY4OTQ1QzQuMTUyMzQgNy41OTk2MSAzLjk0MzM2IDcuNTExNzIgMy42OTcyNyA3LjQyNTc4QzMuMzAyNzMgNy4yODUxNiAyLjk0MzM2IDcuMTM2NzIgMi42MTkxNCA2Ljk4MDQ3QzIuMjk0OTIgNi44MjQyMiAyLjAxNzU4IDYuNjQyNTggMS43ODcxMSA2LjQzNTU1QzEuNTYwNTUgNi4yMjg1MiAxLjM4NDc3IDUuOTg4MjggMS4yNTk3NyA1LjcxNDg0QzEuMTM0NzcgNS40Mzc1IDEuMDcyMjcgNS4xMDkzOCAxLjA3MjI3IDQuNzMwNDdDMS4wNzIyNyA0LjM5ODQ0IDEuMTI4OTEgNC4wOTU3IDEuMjQyMTkgMy44MjIyN0MxLjM1NTQ3IDMuNTQ0OTIgMS41MTU2MiAzLjMwNDY5IDEuNzIyNjYgMy4xMDE1NkMxLjkyOTY5IDIuODk4NDQgMi4xNzk2OSAyLjczNDM3IDIuNDcyNjYgMi42MDkzOEMyLjc2NTYyIDIuNDg0MzggMy4wOTE4IDIuNDA0MyAzLjQ1MTE3IDIuMzY5MTRWMS4xMDkzOEg0LjM4ODY3VjIuMzgwODZDNC43NDAyMyAyLjQyNzczIDUuMDU2NjQgMi41MjM0NCA1LjMzNzg5IDIuNjY3OTdDNS42MTkxNCAyLjgxMjUgNS44NTc0MiAzLjAwMTk1IDYuMDUyNzMgMy4yMzYzM0M2LjI1MTk1IDMuNDY2OCA2LjQwNDMgMy43NDAyMyA2LjUwOTc3IDQuMDU2NjRDNi42MTkxNCA0LjM2OTE0IDYuNjczODMgNC43MjA3IDYuNjczODMgNS4xMTEzM0g1LjA0NDkyQzUuMDQ0OTIgNC42Mzg2NyA0LjkzNzUgNC4yODEyNSA0LjcyMjY2IDQuMDM5MDZDNC41MDc4MSAzLjc5Mjk3IDQuMjE2OCAzLjY2OTkyIDMuODQ5NjEgMy42Njk5MkMzLjY1MDM5IDMuNjY5OTIgMy40NzY1NiAzLjY5NzI3IDMuMzI4MTIgMy43NTE5NUMzLjE4MzU5IDMuODAyNzMgMy4wNjQ0NSAzLjg3Njk1IDIuOTcwNyAzLjk3NDYxQzIuODc2OTUgNC4wNjgzNiAyLjgwNjY0IDQuMTc5NjkgMi43NTk3NyA0LjMwODU5QzIuNzE2OCA0LjQzNzUgMi42OTUzMSA0LjU3ODEyIDIuNjk1MzEgNC43MzA0N0MyLjY5NTMxIDQuODgyODEgMi43MTY4IDUuMDE5NTMgMi43NTk3NyA1LjE0MDYyQzIuODA2NjQgNS4yNTc4MSAyLjg4MjgxIDUuMzY3MTkgMi45ODgyOCA1LjQ2ODc1QzMuMDk3NjYgNS41NzAzMSAzLjI0MDIzIDUuNjY3OTcgMy40MTYwMiA1Ljc2MTcyQzMuNTkxOCA1Ljg1MTU2IDMuODEwNTUgNS45NDMzNiA0LjA3MjI3IDYuMDM3MTFDNC40NjY4IDYuMTg1NTUgNC44MjQyMiA2LjMzOTg0IDUuMTQ0NTMgNi41QzUuNDY0ODQgNi42NTYyNSA1LjczODI4IDYuODM5ODQgNS45NjQ4NCA3LjA1MDc4QzYuMTk1MzEgNy4yNTc4MSA2LjM3MTA5IDcuNSA2LjQ5MjE5IDcuNzc3MzRDNi42MTcxOSA4LjA1MDc4IDYuNjc5NjkgOC4zNzUgNi42Nzk2OSA4Ljc1QzYuNjc5NjkgOS4wOTM3NSA2LjYyMzA1IDkuNDA0MyA2LjUwOTc3IDkuNjgxNjRDNi4zOTY0OCA5Ljk1NTA4IDYuMjM0MzggMTAuMTkxNCA2LjAyMzQ0IDEwLjM5MDZDNS44MTI1IDEwLjU4OTggNS41NTg1OSAxMC43NSA1LjI2MTcyIDEwLjg3MTFDNC45NjQ4NCAxMC45ODgzIDQuNjMyODEgMTEuMDY0NSA0LjI2NTYyIDExLjA5OTZWMTIuMjQ4SDMuMzMzOThWMTEuMDk5NkMzLjAwMTk1IDExLjA2ODQgMi42Nzk2OSAxMC45OTYxIDIuMzY3MTkgMTAuODgyOEMyLjA1NDY5IDEwLjc2NTYgMS43NzczNCAxMC41OTc3IDEuNTM1MTYgMTAuMzc4OUMxLjI5Njg4IDEwLjE2MDIgMS4xMDU0NyA5Ljg4NDc3IDAuOTYwOTM4IDkuNTUyNzNDMC44MTY0MDYgOS4yMTY4IDAuNzQ0MTQxIDguODE0NDUgMC43NDQxNDEgOC4zNDU3SDIuMzc4OTFDMi4zNzg5MSA4LjYyNjk1IDIuNDE5OTIgOC44NjMyOCAyLjUwMTk1IDkuMDU0NjlDMi41ODM5OCA5LjI0MjE5IDIuNjg5NDUgOS4zOTI1OCAyLjgxODM2IDkuNTA1ODZDMi45NTExNyA5LjYxNTIzIDMuMTAxNTYgOS42OTMzNiAzLjI2OTUzIDkuNzQwMjNDMy40Mzc1IDkuNzg3MTEgMy42MDkzOCA5LjgxMDU1IDMuNzg1MTYgOS44MTA1NUM0LjIwMzEyIDkuODEwNTUgNC41MTk1MyA5LjcxMjg5IDQuNzM0MzggOS41MTc1OEM0Ljk0OTIyIDkuMzIyMjcgNS4wNTY2NCA5LjA3MDMxIDUuMDU2NjQgOC43NjE3MlpNMTMuNDE4IDEyLjI3MTVIOC4wNzQyMlYxMUgxMy40MThWMTIuMjcxNVoiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDMuOTUyNjQgNikiIGZpbGw9IndoaXRlIi8+Cjwvc3ZnPgo=);
  --jp-icon-text-editor: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtdGV4dC1lZGl0b3ItaWNvbi1jb2xvciBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xNSAxNUgzdjJoMTJ2LTJ6bTAtOEgzdjJoMTJWN3pNMyAxM2gxOHYtMkgzdjJ6bTAgOGgxOHYtMkgzdjJ6TTMgM3YyaDE4VjNIM3oiLz4KPC9zdmc+Cg==);
  --jp-icon-toc: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik03LDVIMjFWN0g3VjVNNywxM1YxMUgyMVYxM0g3TTQsNC41QTEuNSwxLjUgMCAwLDEgNS41LDZBMS41LDEuNSAwIDAsMSA0LDcuNUExLjUsMS41IDAgMCwxIDIuNSw2QTEuNSwxLjUgMCAwLDEgNCw0LjVNNCwxMC41QTEuNSwxLjUgMCAwLDEgNS41LDEyQTEuNSwxLjUgMCAwLDEgNCwxMy41QTEuNSwxLjUgMCAwLDEgMi41LDEyQTEuNSwxLjUgMCAwLDEgNCwxMC41TTcsMTlWMTdIMjFWMTlIN000LDE2LjVBMS41LDEuNSAwIDAsMSA1LjUsMThBMS41LDEuNSAwIDAsMSA0LDE5LjVBMS41LDEuNSAwIDAsMSAyLjUsMThBMS41LDEuNSAwIDAsMSA0LDE2LjVaIiAvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-tree-view: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik0yMiAxMVYzaC03djNIOVYzSDJ2OGg3VjhoMnYxMGg0djNoN3YtOGgtN3YzaC0yVjhoMnYzeiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-trusted: url(data:image/svg+xml;base64,PHN2ZyBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI1Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDIgMykiIGQ9Ik0xLjg2MDk0IDExLjQ0MDlDMC44MjY0NDggOC43NzAyNyAwLjg2Mzc3OSA2LjA1NzY0IDEuMjQ5MDcgNC4xOTkzMkMyLjQ4MjA2IDMuOTMzNDcgNC4wODA2OCAzLjQwMzQ3IDUuNjAxMDIgMi44NDQ5QzcuMjM1NDkgMi4yNDQ0IDguODU2NjYgMS41ODE1IDkuOTg3NiAxLjA5NTM5QzExLjA1OTcgMS41ODM0MSAxMi42MDk0IDIuMjQ0NCAxNC4yMTggMi44NDMzOUMxNS43NTAzIDMuNDEzOTQgMTcuMzk5NSAzLjk1MjU4IDE4Ljc1MzkgNC4yMTM4NUMxOS4xMzY0IDYuMDcxNzcgMTkuMTcwOSA4Ljc3NzIyIDE4LjEzOSAxMS40NDA5QzE3LjAzMDMgMTQuMzAzMiAxNC42NjY4IDE3LjE4NDQgOS45OTk5OSAxOC45MzU0QzUuMzMzMiAxNy4xODQ0IDIuOTY5NjggMTQuMzAzMiAxLjg2MDk0IDExLjQ0MDlaIi8+CiAgICA8cGF0aCBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiMzMzMzMzMiIHN0cm9rZT0iIzMzMzMzMyIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOCA5Ljg2NzE5KSIgZD0iTTIuODYwMTUgNC44NjUzNUwwLjcyNjU0OSAyLjk5OTU5TDAgMy42MzA0NUwyLjg2MDE1IDYuMTMxNTdMOCAwLjYzMDg3Mkw3LjI3ODU3IDBMMi44NjAxNSA0Ljg2NTM1WiIvPgo8L3N2Zz4K);
  --jp-icon-undo: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjUgOGMtMi42NSAwLTUuMDUuOTktNi45IDIuNkwyIDd2OWg5bC0zLjYyLTMuNjJjMS4zOS0xLjE2IDMuMTYtMS44OCA1LjEyLTEuODggMy41NCAwIDYuNTUgMi4zMSA3LjYgNS41bDIuMzctLjc4QzIxLjA4IDExLjAzIDE3LjE1IDggMTIuNSA4eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-user: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE2IDdhNCA0IDAgMTEtOCAwIDQgNCAwIDAxOCAwek0xMiAxNGE3IDcgMCAwMC03IDdoMTRhNyA3IDAgMDAtNy03eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-users: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZlcnNpb249IjEuMSIgdmlld0JveD0iMCAwIDM2IDI0IiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPgogPGcgY2xhc3M9ImpwLWljb24zIiB0cmFuc2Zvcm09Im1hdHJpeCgxLjczMjcgMCAwIDEuNzMyNyAtMy42MjgyIC4wOTk1NzcpIiBmaWxsPSIjNjE2MTYxIj4KICA8cGF0aCB0cmFuc2Zvcm09Im1hdHJpeCgxLjUsMCwwLDEuNSwwLC02KSIgZD0ibTEyLjE4NiA3LjUwOThjLTEuMDUzNSAwLTEuOTc1NyAwLjU2NjUtMi40Nzg1IDEuNDEwMiAwLjc1MDYxIDAuMzEyNzcgMS4zOTc0IDAuODI2NDggMS44NzMgMS40NzI3aDMuNDg2M2MwLTEuNTkyLTEuMjg4OS0yLjg4MjgtMi44ODA5LTIuODgyOHoiLz4KICA8cGF0aCBkPSJtMjAuNDY1IDIuMzg5NWEyLjE4ODUgMi4xODg1IDAgMCAxLTIuMTg4NCAyLjE4ODUgMi4xODg1IDIuMTg4NSAwIDAgMS0yLjE4ODUtMi4xODg1IDIuMTg4NSAyLjE4ODUgMCAwIDEgMi4xODg1LTIuMTg4NSAyLjE4ODUgMi4xODg1IDAgMCAxIDIuMTg4NCAyLjE4ODV6Ii8+CiAgPHBhdGggdHJhbnNmb3JtPSJtYXRyaXgoMS41LDAsMCwxLjUsMCwtNikiIGQ9Im0zLjU4OTggOC40MjE5Yy0xLjExMjYgMC0yLjAxMzcgMC45MDExMS0yLjAxMzcgMi4wMTM3aDIuODE0NWMwLjI2Nzk3LTAuMzczMDkgMC41OTA3LTAuNzA0MzUgMC45NTg5OC0wLjk3ODUyLTAuMzQ0MzMtMC42MTY4OC0xLjAwMzEtMS4wMzUyLTEuNzU5OC0xLjAzNTJ6Ii8+CiAgPHBhdGggZD0ibTYuOTE1NCA0LjYyM2ExLjUyOTQgMS41Mjk0IDAgMCAxLTEuNTI5NCAxLjUyOTQgMS41Mjk0IDEuNTI5NCAwIDAgMS0xLjUyOTQtMS41Mjk0IDEuNTI5NCAxLjUyOTQgMCAwIDEgMS41Mjk0LTEuNTI5NCAxLjUyOTQgMS41Mjk0IDAgMCAxIDEuNTI5NCAxLjUyOTR6Ii8+CiAgPHBhdGggZD0ibTYuMTM1IDEzLjUzNWMwLTMuMjM5MiAyLjYyNTktNS44NjUgNS44NjUtNS44NjUgMy4yMzkyIDAgNS44NjUgMi42MjU5IDUuODY1IDUuODY1eiIvPgogIDxjaXJjbGUgY3g9IjEyIiBjeT0iMy43Njg1IiByPSIyLjk2ODUiLz4KIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-vega: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbjEganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMjEyMTIxIj4KICAgIDxwYXRoIGQ9Ik0xMC42IDUuNGwyLjItMy4ySDIuMnY3LjNsNC02LjZ6Ii8+CiAgICA8cGF0aCBkPSJNMTUuOCAyLjJsLTQuNCA2LjZMNyA2LjNsLTQuOCA4djUuNWgxNy42VjIuMmgtNHptLTcgMTUuNEg1LjV2LTQuNGgzLjN2NC40em00LjQgMEg5LjhWOS44aDMuNHY3Ljh6bTQuNCAwaC0zLjRWNi41aDMuNHYxMS4xeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-word: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KIDxnIGNsYXNzPSJqcC1pY29uMiIgZmlsbD0iIzQxNDE0MSI+CiAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiA8L2c+CiA8ZyBjbGFzcz0ianAtaWNvbi1hY2NlbnQyIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSguNDMgLjA0MDEpIiBmaWxsPSIjZmZmIj4KICA8cGF0aCBkPSJtNC4xNCA4Ljc2cTAuMDY4Mi0xLjg5IDIuNDItMS44OSAxLjE2IDAgMS42OCAwLjQyIDAuNTY3IDAuNDEgMC41NjcgMS4xNnYzLjQ3cTAgMC40NjIgMC41MTQgMC40NjIgMC4xMDMgMCAwLjItMC4wMjMxdjAuNzE0cS0wLjM5OSAwLjEwMy0wLjY1MSAwLjEwMy0wLjQ1MiAwLTAuNjkzLTAuMjItMC4yMzEtMC4yLTAuMjg0LTAuNjYyLTAuOTU2IDAuODcyLTIgMC44NzItMC45MDMgMC0xLjQ3LTAuNDcyLTAuNTI1LTAuNDcyLTAuNTI1LTEuMjYgMC0wLjI2MiAwLjA0NTItMC40NzIgMC4wNTY3LTAuMjIgMC4xMTYtMC4zNzggMC4wNjgyLTAuMTY4IDAuMjMxLTAuMzA0IDAuMTU4LTAuMTQ3IDAuMjYyLTAuMjQyIDAuMTE2LTAuMDkxNCAwLjM2OC0wLjE2OCAwLjI2Mi0wLjA5MTQgMC4zOTktMC4xMjYgMC4xMzYtMC4wNDUyIDAuNDcyLTAuMTAzIDAuMzM2LTAuMDU3OCAwLjUwNC0wLjA3OTggMC4xNTgtMC4wMjMxIDAuNTY3LTAuMDc5OCAwLjU1Ni0wLjA2ODIgMC43NzctMC4yMjEgMC4yMi0wLjE1MiAwLjIyLTAuNDQxdi0wLjI1MnEwLTAuNDMtMC4zNTctMC42NjItMC4zMzYtMC4yMzEtMC45NzYtMC4yMzEtMC42NjIgMC0wLjk5OCAwLjI2Mi0wLjMzNiAwLjI1Mi0wLjM5OSAwLjc5OHptMS44OSAzLjY4cTAuNzg4IDAgMS4yNi0wLjQxIDAuNTA0LTAuNDIgMC41MDQtMC45MDN2LTEuMDVxLTAuMjg0IDAuMTM2LTAuODYxIDAuMjMxLTAuNTY3IDAuMDkxNC0wLjk4NyAwLjE1OC0wLjQyIDAuMDY4Mi0wLjc2NiAwLjMyNi0wLjMzNiAwLjI1Mi0wLjMzNiAwLjcwNHQwLjMwNCAwLjcwNCAwLjg2MSAwLjI1MnoiIHN0cm9rZS13aWR0aD0iMS4wNSIvPgogIDxwYXRoIGQ9Im0xMCA0LjU2aDAuOTQ1djMuMTVxMC42NTEtMC45NzYgMS44OS0wLjk3NiAxLjE2IDAgMS44OSAwLjg0IDAuNjgyIDAuODQgMC42ODIgMi4zMSAwIDEuNDctMC43MDQgMi40Mi0wLjcwNCAwLjg4Mi0xLjg5IDAuODgyLTEuMjYgMC0xLjg5LTEuMDJ2MC43NjZoLTAuODV6bTIuNjIgMy4wNHEtMC43NDYgMC0xLjE2IDAuNjQtMC40NTIgMC42My0wLjQ1MiAxLjY4IDAgMS4wNSAwLjQ1MiAxLjY4dDEuMTYgMC42M3EwLjc3NyAwIDEuMjYtMC42MyAwLjQ5NC0wLjY0IDAuNDk0LTEuNjggMC0xLjA1LTAuNDcyLTEuNjgtMC40NjItMC42NC0xLjI2LTAuNjR6IiBzdHJva2Utd2lkdGg9IjEuMDUiLz4KICA8cGF0aCBkPSJtMi43MyAxNS44IDEzLjYgMC4wMDgxYzAuMDA2OSAwIDAtMi42IDAtMi42IDAtMC4wMDc4LTEuMTUgMC0xLjE1IDAtMC4wMDY5IDAtMC4wMDgzIDEuNS0wLjAwODMgMS41LTJlLTMgLTAuMDAxNC0xMS4zLTAuMDAxNC0xMS4zLTAuMDAxNGwtMC4wMDU5Mi0xLjVjMC0wLjAwNzgtMS4xNyAwLjAwMTMtMS4xNyAwLjAwMTN6IiBzdHJva2Utd2lkdGg9Ii45NzUiLz4KIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-yaml: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1jb250cmFzdDIganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjRDgxQjYwIj4KICAgIDxwYXRoIGQ9Ik03LjIgMTguNnYtNS40TDMgNS42aDMuM2wxLjQgMy4xYy4zLjkuNiAxLjYgMSAyLjUuMy0uOC42LTEuNiAxLTIuNWwxLjQtMy4xaDMuNGwtNC40IDcuNnY1LjVsLTIuOS0uMXoiLz4KICAgIDxjaXJjbGUgY2xhc3M9InN0MCIgY3g9IjE3LjYiIGN5PSIxNi41IiByPSIyLjEiLz4KICAgIDxjaXJjbGUgY2xhc3M9InN0MCIgY3g9IjE3LjYiIGN5PSIxMSIgcj0iMi4xIi8+CiAgPC9nPgo8L3N2Zz4K);
}

/* Icon CSS class declarations */

.jp-AddAboveIcon {
  background-image: var(--jp-icon-add-above);
}

.jp-AddBelowIcon {
  background-image: var(--jp-icon-add-below);
}

.jp-AddIcon {
  background-image: var(--jp-icon-add);
}

.jp-BellIcon {
  background-image: var(--jp-icon-bell);
}

.jp-BugDotIcon {
  background-image: var(--jp-icon-bug-dot);
}

.jp-BugIcon {
  background-image: var(--jp-icon-bug);
}

.jp-BuildIcon {
  background-image: var(--jp-icon-build);
}

.jp-CaretDownEmptyIcon {
  background-image: var(--jp-icon-caret-down-empty);
}

.jp-CaretDownEmptyThinIcon {
  background-image: var(--jp-icon-caret-down-empty-thin);
}

.jp-CaretDownIcon {
  background-image: var(--jp-icon-caret-down);
}

.jp-CaretLeftIcon {
  background-image: var(--jp-icon-caret-left);
}

.jp-CaretRightIcon {
  background-image: var(--jp-icon-caret-right);
}

.jp-CaretUpEmptyThinIcon {
  background-image: var(--jp-icon-caret-up-empty-thin);
}

.jp-CaretUpIcon {
  background-image: var(--jp-icon-caret-up);
}

.jp-CaseSensitiveIcon {
  background-image: var(--jp-icon-case-sensitive);
}

.jp-CheckIcon {
  background-image: var(--jp-icon-check);
}

.jp-CircleEmptyIcon {
  background-image: var(--jp-icon-circle-empty);
}

.jp-CircleIcon {
  background-image: var(--jp-icon-circle);
}

.jp-ClearIcon {
  background-image: var(--jp-icon-clear);
}

.jp-CloseIcon {
  background-image: var(--jp-icon-close);
}

.jp-CodeCheckIcon {
  background-image: var(--jp-icon-code-check);
}

.jp-CodeIcon {
  background-image: var(--jp-icon-code);
}

.jp-CollapseAllIcon {
  background-image: var(--jp-icon-collapse-all);
}

.jp-ConsoleIcon {
  background-image: var(--jp-icon-console);
}

.jp-CopyIcon {
  background-image: var(--jp-icon-copy);
}

.jp-CopyrightIcon {
  background-image: var(--jp-icon-copyright);
}

.jp-CutIcon {
  background-image: var(--jp-icon-cut);
}

.jp-DeleteIcon {
  background-image: var(--jp-icon-delete);
}

.jp-DownloadIcon {
  background-image: var(--jp-icon-download);
}

.jp-DuplicateIcon {
  background-image: var(--jp-icon-duplicate);
}

.jp-EditIcon {
  background-image: var(--jp-icon-edit);
}

.jp-EllipsesIcon {
  background-image: var(--jp-icon-ellipses);
}

.jp-ErrorIcon {
  background-image: var(--jp-icon-error);
}

.jp-ExpandAllIcon {
  background-image: var(--jp-icon-expand-all);
}

.jp-ExtensionIcon {
  background-image: var(--jp-icon-extension);
}

.jp-FastForwardIcon {
  background-image: var(--jp-icon-fast-forward);
}

.jp-FileIcon {
  background-image: var(--jp-icon-file);
}

.jp-FileUploadIcon {
  background-image: var(--jp-icon-file-upload);
}

.jp-FilterDotIcon {
  background-image: var(--jp-icon-filter-dot);
}

.jp-FilterIcon {
  background-image: var(--jp-icon-filter);
}

.jp-FilterListIcon {
  background-image: var(--jp-icon-filter-list);
}

.jp-FolderFavoriteIcon {
  background-image: var(--jp-icon-folder-favorite);
}

.jp-FolderIcon {
  background-image: var(--jp-icon-folder);
}

.jp-HomeIcon {
  background-image: var(--jp-icon-home);
}

.jp-Html5Icon {
  background-image: var(--jp-icon-html5);
}

.jp-ImageIcon {
  background-image: var(--jp-icon-image);
}

.jp-InfoIcon {
  background-image: var(--jp-icon-info);
}

.jp-InspectorIcon {
  background-image: var(--jp-icon-inspector);
}

.jp-JsonIcon {
  background-image: var(--jp-icon-json);
}

.jp-JuliaIcon {
  background-image: var(--jp-icon-julia);
}

.jp-JupyterFaviconIcon {
  background-image: var(--jp-icon-jupyter-favicon);
}

.jp-JupyterIcon {
  background-image: var(--jp-icon-jupyter);
}

.jp-JupyterlabWordmarkIcon {
  background-image: var(--jp-icon-jupyterlab-wordmark);
}

.jp-KernelIcon {
  background-image: var(--jp-icon-kernel);
}

.jp-KeyboardIcon {
  background-image: var(--jp-icon-keyboard);
}

.jp-LaunchIcon {
  background-image: var(--jp-icon-launch);
}

.jp-LauncherIcon {
  background-image: var(--jp-icon-launcher);
}

.jp-LineFormIcon {
  background-image: var(--jp-icon-line-form);
}

.jp-LinkIcon {
  background-image: var(--jp-icon-link);
}

.jp-ListIcon {
  background-image: var(--jp-icon-list);
}

.jp-MarkdownIcon {
  background-image: var(--jp-icon-markdown);
}

.jp-MoveDownIcon {
  background-image: var(--jp-icon-move-down);
}

.jp-MoveUpIcon {
  background-image: var(--jp-icon-move-up);
}

.jp-NewFolderIcon {
  background-image: var(--jp-icon-new-folder);
}

.jp-NotTrustedIcon {
  background-image: var(--jp-icon-not-trusted);
}

.jp-NotebookIcon {
  background-image: var(--jp-icon-notebook);
}

.jp-NumberingIcon {
  background-image: var(--jp-icon-numbering);
}

.jp-OfflineBoltIcon {
  background-image: var(--jp-icon-offline-bolt);
}

.jp-PaletteIcon {
  background-image: var(--jp-icon-palette);
}

.jp-PasteIcon {
  background-image: var(--jp-icon-paste);
}

.jp-PdfIcon {
  background-image: var(--jp-icon-pdf);
}

.jp-PythonIcon {
  background-image: var(--jp-icon-python);
}

.jp-RKernelIcon {
  background-image: var(--jp-icon-r-kernel);
}

.jp-ReactIcon {
  background-image: var(--jp-icon-react);
}

.jp-RedoIcon {
  background-image: var(--jp-icon-redo);
}

.jp-RefreshIcon {
  background-image: var(--jp-icon-refresh);
}

.jp-RegexIcon {
  background-image: var(--jp-icon-regex);
}

.jp-RunIcon {
  background-image: var(--jp-icon-run);
}

.jp-RunningIcon {
  background-image: var(--jp-icon-running);
}

.jp-SaveIcon {
  background-image: var(--jp-icon-save);
}

.jp-SearchIcon {
  background-image: var(--jp-icon-search);
}

.jp-SettingsIcon {
  background-image: var(--jp-icon-settings);
}

.jp-ShareIcon {
  background-image: var(--jp-icon-share);
}

.jp-SpreadsheetIcon {
  background-image: var(--jp-icon-spreadsheet);
}

.jp-StopIcon {
  background-image: var(--jp-icon-stop);
}

.jp-TabIcon {
  background-image: var(--jp-icon-tab);
}

.jp-TableRowsIcon {
  background-image: var(--jp-icon-table-rows);
}

.jp-TagIcon {
  background-image: var(--jp-icon-tag);
}

.jp-TerminalIcon {
  background-image: var(--jp-icon-terminal);
}

.jp-TextEditorIcon {
  background-image: var(--jp-icon-text-editor);
}

.jp-TocIcon {
  background-image: var(--jp-icon-toc);
}

.jp-TreeViewIcon {
  background-image: var(--jp-icon-tree-view);
}

.jp-TrustedIcon {
  background-image: var(--jp-icon-trusted);
}

.jp-UndoIcon {
  background-image: var(--jp-icon-undo);
}

.jp-UserIcon {
  background-image: var(--jp-icon-user);
}

.jp-UsersIcon {
  background-image: var(--jp-icon-users);
}

.jp-VegaIcon {
  background-image: var(--jp-icon-vega);
}

.jp-WordIcon {
  background-image: var(--jp-icon-word);
}

.jp-YamlIcon {
  background-image: var(--jp-icon-yaml);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * (DEPRECATED) Support for consuming icons as CSS background images
 */

.jp-Icon,
.jp-MaterialIcon {
  background-position: center;
  background-repeat: no-repeat;
  background-size: 16px;
  min-width: 16px;
  min-height: 16px;
}

.jp-Icon-cover {
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

/**
 * (DEPRECATED) Support for specific CSS icon sizes
 */

.jp-Icon-16 {
  background-size: 16px;
  min-width: 16px;
  min-height: 16px;
}

.jp-Icon-18 {
  background-size: 18px;
  min-width: 18px;
  min-height: 18px;
}

.jp-Icon-20 {
  background-size: 20px;
  min-width: 20px;
  min-height: 20px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.lm-TabBar .lm-TabBar-addButton {
  align-items: center;
  display: flex;
  padding: 4px;
  padding-bottom: 5px;
  margin-right: 1px;
  background-color: var(--jp-layout-color2);
}

.lm-TabBar .lm-TabBar-addButton:hover {
  background-color: var(--jp-layout-color1);
}

.lm-DockPanel-tabBar .lm-TabBar-tab {
  width: var(--jp-private-horizontal-tab-width);
}

.lm-DockPanel-tabBar .lm-TabBar-content {
  flex: unset;
}

.lm-DockPanel-tabBar[data-orientation='horizontal'] {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * Support for icons as inline SVG HTMLElements
 */

/* recolor the primary elements of an icon */
.jp-icon0[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon1[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon2[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon3[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon4[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon0[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon1[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon2[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon3[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon4[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/* recolor the accent elements of an icon */
.jp-icon-accent0[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-accent1[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-accent2[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-accent3[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-accent4[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-accent0[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-accent1[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-accent2[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-accent3[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-accent4[stroke] {
  stroke: var(--jp-layout-color4);
}

/* set the color of an icon to transparent */
.jp-icon-none[fill] {
  fill: none;
}

.jp-icon-none[stroke] {
  stroke: none;
}

/* brand icon colors. Same for light and dark */
.jp-icon-brand0[fill] {
  fill: var(--jp-brand-color0);
}

.jp-icon-brand1[fill] {
  fill: var(--jp-brand-color1);
}

.jp-icon-brand2[fill] {
  fill: var(--jp-brand-color2);
}

.jp-icon-brand3[fill] {
  fill: var(--jp-brand-color3);
}

.jp-icon-brand4[fill] {
  fill: var(--jp-brand-color4);
}

.jp-icon-brand0[stroke] {
  stroke: var(--jp-brand-color0);
}

.jp-icon-brand1[stroke] {
  stroke: var(--jp-brand-color1);
}

.jp-icon-brand2[stroke] {
  stroke: var(--jp-brand-color2);
}

.jp-icon-brand3[stroke] {
  stroke: var(--jp-brand-color3);
}

.jp-icon-brand4[stroke] {
  stroke: var(--jp-brand-color4);
}

/* warn icon colors. Same for light and dark */
.jp-icon-warn0[fill] {
  fill: var(--jp-warn-color0);
}

.jp-icon-warn1[fill] {
  fill: var(--jp-warn-color1);
}

.jp-icon-warn2[fill] {
  fill: var(--jp-warn-color2);
}

.jp-icon-warn3[fill] {
  fill: var(--jp-warn-color3);
}

.jp-icon-warn0[stroke] {
  stroke: var(--jp-warn-color0);
}

.jp-icon-warn1[stroke] {
  stroke: var(--jp-warn-color1);
}

.jp-icon-warn2[stroke] {
  stroke: var(--jp-warn-color2);
}

.jp-icon-warn3[stroke] {
  stroke: var(--jp-warn-color3);
}

/* icon colors that contrast well with each other and most backgrounds */
.jp-icon-contrast0[fill] {
  fill: var(--jp-icon-contrast-color0);
}

.jp-icon-contrast1[fill] {
  fill: var(--jp-icon-contrast-color1);
}

.jp-icon-contrast2[fill] {
  fill: var(--jp-icon-contrast-color2);
}

.jp-icon-contrast3[fill] {
  fill: var(--jp-icon-contrast-color3);
}

.jp-icon-contrast0[stroke] {
  stroke: var(--jp-icon-contrast-color0);
}

.jp-icon-contrast1[stroke] {
  stroke: var(--jp-icon-contrast-color1);
}

.jp-icon-contrast2[stroke] {
  stroke: var(--jp-icon-contrast-color2);
}

.jp-icon-contrast3[stroke] {
  stroke: var(--jp-icon-contrast-color3);
}

.jp-icon-dot[fill] {
  fill: var(--jp-warn-color0);
}

.jp-jupyter-icon-color[fill] {
  fill: var(--jp-jupyter-icon-color, var(--jp-warn-color0));
}

.jp-notebook-icon-color[fill] {
  fill: var(--jp-notebook-icon-color, var(--jp-warn-color0));
}

.jp-json-icon-color[fill] {
  fill: var(--jp-json-icon-color, var(--jp-warn-color1));
}

.jp-console-icon-color[fill] {
  fill: var(--jp-console-icon-color, white);
}

.jp-console-icon-background-color[fill] {
  fill: var(--jp-console-icon-background-color, var(--jp-brand-color1));
}

.jp-terminal-icon-color[fill] {
  fill: var(--jp-terminal-icon-color, var(--jp-layout-color2));
}

.jp-terminal-icon-background-color[fill] {
  fill: var(
    --jp-terminal-icon-background-color,
    var(--jp-inverse-layout-color2)
  );
}

.jp-text-editor-icon-color[fill] {
  fill: var(--jp-text-editor-icon-color, var(--jp-inverse-layout-color3));
}

.jp-inspector-icon-color[fill] {
  fill: var(--jp-inspector-icon-color, var(--jp-inverse-layout-color3));
}

/* CSS for icons in selected filebrowser listing items */
.jp-DirListing-item.jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}

.jp-DirListing-item.jp-mod-selected .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}

/* stylelint-disable selector-max-class, selector-max-compound-selectors */

/**
* TODO: come up with non css-hack solution for showing the busy icon on top
*  of the close icon
* CSS for complex behavior of close icon of tabs in the main area tabbar
*/
.lm-DockPanel-tabBar
  .lm-TabBar-tab.lm-mod-closable.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon3[fill] {
  fill: none;
}

.lm-DockPanel-tabBar
  .lm-TabBar-tab.lm-mod-closable.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon-busy[fill] {
  fill: var(--jp-inverse-layout-color3);
}

/* stylelint-enable selector-max-class, selector-max-compound-selectors */

/* CSS for icons in status bar */
#jp-main-statusbar .jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}

#jp-main-statusbar .jp-mod-selected .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}

/* special handling for splash icon CSS. While the theme CSS reloads during
   splash, the splash icon can loose theming. To prevent that, we set a
   default for its color variable */
:root {
  --jp-warn-color0: var(--md-orange-700);
}

/* not sure what to do with this one, used in filebrowser listing */
.jp-DragIcon {
  margin-right: 4px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * Support for alt colors for icons as inline SVG HTMLElements
 */

/* alt recolor the primary elements of an icon */
.jp-icon-alt .jp-icon0[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-alt .jp-icon1[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-alt .jp-icon2[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-alt .jp-icon3[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-alt .jp-icon4[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-alt .jp-icon0[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-alt .jp-icon1[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-alt .jp-icon2[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-alt .jp-icon3[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-alt .jp-icon4[stroke] {
  stroke: var(--jp-layout-color4);
}

/* alt recolor the accent elements of an icon */
.jp-icon-alt .jp-icon-accent0[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon-alt .jp-icon-accent1[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon-alt .jp-icon-accent2[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon-alt .jp-icon-accent3[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon-alt .jp-icon-accent4[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-alt .jp-icon-accent0[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon-alt .jp-icon-accent1[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon-alt .jp-icon-accent2[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon-alt .jp-icon-accent3[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon-alt .jp-icon-accent4[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-icon-hoverShow:not(:hover) .jp-icon-hoverShow-content {
  display: none !important;
}

/**
 * Support for hover colors for icons as inline SVG HTMLElements
 */

/**
 * regular colors
 */

/* recolor the primary elements of an icon */
.jp-icon-hover :hover .jp-icon0-hover[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon-hover :hover .jp-icon1-hover[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon-hover :hover .jp-icon2-hover[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon-hover :hover .jp-icon3-hover[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon-hover :hover .jp-icon4-hover[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-hover :hover .jp-icon0-hover[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon-hover :hover .jp-icon1-hover[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon-hover :hover .jp-icon2-hover[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon-hover :hover .jp-icon3-hover[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon-hover :hover .jp-icon4-hover[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/* recolor the accent elements of an icon */
.jp-icon-hover :hover .jp-icon-accent0-hover[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-hover :hover .jp-icon-accent1-hover[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-hover :hover .jp-icon-accent2-hover[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-hover :hover .jp-icon-accent3-hover[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-hover :hover .jp-icon-accent4-hover[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-hover :hover .jp-icon-accent0-hover[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-hover :hover .jp-icon-accent1-hover[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-hover :hover .jp-icon-accent2-hover[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-hover :hover .jp-icon-accent3-hover[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-hover :hover .jp-icon-accent4-hover[stroke] {
  stroke: var(--jp-layout-color4);
}

/* set the color of an icon to transparent */
.jp-icon-hover :hover .jp-icon-none-hover[fill] {
  fill: none;
}

.jp-icon-hover :hover .jp-icon-none-hover[stroke] {
  stroke: none;
}

/**
 * inverse colors
 */

/* inverse recolor the primary elements of an icon */
.jp-icon-hover.jp-icon-alt :hover .jp-icon0-hover[fill] {
  fill: var(--jp-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon1-hover[fill] {
  fill: var(--jp-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon2-hover[fill] {
  fill: var(--jp-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon3-hover[fill] {
  fill: var(--jp-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon4-hover[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon0-hover[stroke] {
  stroke: var(--jp-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon1-hover[stroke] {
  stroke: var(--jp-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon2-hover[stroke] {
  stroke: var(--jp-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon3-hover[stroke] {
  stroke: var(--jp-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon4-hover[stroke] {
  stroke: var(--jp-layout-color4);
}

/* inverse recolor the accent elements of an icon */
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent0-hover[fill] {
  fill: var(--jp-inverse-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent1-hover[fill] {
  fill: var(--jp-inverse-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent2-hover[fill] {
  fill: var(--jp-inverse-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent3-hover[fill] {
  fill: var(--jp-inverse-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent4-hover[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent0-hover[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent1-hover[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent2-hover[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent3-hover[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent4-hover[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-IFrame {
  width: 100%;
  height: 100%;
}

.jp-IFrame > iframe {
  border: none;
}

/*
When drag events occur, `lm-mod-override-cursor` is added to the body.
Because iframes steal all cursor events, the following two rules are necessary
to suppress pointer events while resize drags are occurring. There may be a
better solution to this problem.
*/
body.lm-mod-override-cursor .jp-IFrame {
  position: relative;
}

body.lm-mod-override-cursor .jp-IFrame::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-HoverBox {
  position: fixed;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-FormGroup-content fieldset {
  border: none;
  padding: 0;
  min-width: 0;
  width: 100%;
}

/* stylelint-disable selector-max-type */

.jp-FormGroup-content fieldset .jp-inputFieldWrapper input,
.jp-FormGroup-content fieldset .jp-inputFieldWrapper select,
.jp-FormGroup-content fieldset .jp-inputFieldWrapper textarea {
  font-size: var(--jp-content-font-size2);
  border-color: var(--jp-input-border-color);
  border-style: solid;
  border-radius: var(--jp-border-radius);
  border-width: 1px;
  padding: 6px 8px;
  background: none;
  color: var(--jp-ui-font-color0);
  height: inherit;
}

.jp-FormGroup-content fieldset input[type='checkbox'] {
  position: relative;
  top: 2px;
  margin-left: 0;
}

.jp-FormGroup-content button.jp-mod-styled {
  cursor: pointer;
}

.jp-FormGroup-content .checkbox label {
  cursor: pointer;
  font-size: var(--jp-content-font-size1);
}

.jp-FormGroup-content .jp-root > fieldset > legend {
  display: none;
}

.jp-FormGroup-content .jp-root > fieldset > p {
  display: none;
}

/** copy of `input.jp-mod-styled:focus` style */
.jp-FormGroup-content fieldset input:focus,
.jp-FormGroup-content fieldset select:focus {
  -moz-outline-radius: unset;
  outline: var(--jp-border-width) solid var(--md-blue-500);
  outline-offset: -1px;
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-FormGroup-content fieldset input:hover:not(:focus),
.jp-FormGroup-content fieldset select:hover:not(:focus) {
  background-color: var(--jp-border-color2);
}

/* stylelint-enable selector-max-type */

.jp-FormGroup-content .checkbox .field-description {
  /* Disable default description field for checkbox:
   because other widgets do not have description fields,
   we add descriptions to each widget on the field level.
  */
  display: none;
}

.jp-FormGroup-content #root__description {
  display: none;
}

.jp-FormGroup-content .jp-modifiedIndicator {
  width: 5px;
  background-color: var(--jp-brand-color2);
  margin-top: 0;
  margin-left: calc(var(--jp-private-settingeditor-modifier-indent) * -1);
  flex-shrink: 0;
}

.jp-FormGroup-content .jp-modifiedIndicator.jp-errorIndicator {
  background-color: var(--jp-error-color0);
  margin-right: 0.5em;
}

/* RJSF ARRAY style */

.jp-arrayFieldWrapper legend {
  font-size: var(--jp-content-font-size2);
  color: var(--jp-ui-font-color0);
  flex-basis: 100%;
  padding: 4px 0;
  font-weight: var(--jp-content-heading-font-weight);
  border-bottom: 1px solid var(--jp-border-color2);
}

.jp-arrayFieldWrapper .field-description {
  padding: 4px 0;
  white-space: pre-wrap;
}

.jp-arrayFieldWrapper .array-item {
  width: 100%;
  border: 1px solid var(--jp-border-color2);
  border-radius: 4px;
  margin: 4px;
}

.jp-ArrayOperations {
  display: flex;
  margin-left: 8px;
}

.jp-ArrayOperationsButton {
  margin: 2px;
}

.jp-ArrayOperationsButton .jp-icon3[fill] {
  fill: var(--jp-ui-font-color0);
}

button.jp-ArrayOperationsButton.jp-mod-styled:disabled {
  cursor: not-allowed;
  opacity: 0.5;
}

/* RJSF form validation error */

.jp-FormGroup-content .validationErrors {
  color: var(--jp-error-color0);
}

/* Hide panel level error as duplicated the field level error */
.jp-FormGroup-content .panel.errors {
  display: none;
}

/* RJSF normal content (settings-editor) */

.jp-FormGroup-contentNormal {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}

.jp-FormGroup-contentNormal .jp-FormGroup-contentItem {
  margin-left: 7px;
  color: var(--jp-ui-font-color0);
}

.jp-FormGroup-contentNormal .jp-FormGroup-description {
  flex-basis: 100%;
  padding: 4px 7px;
}

.jp-FormGroup-contentNormal .jp-FormGroup-default {
  flex-basis: 100%;
  padding: 4px 7px;
}

.jp-FormGroup-contentNormal .jp-FormGroup-fieldLabel {
  font-size: var(--jp-content-font-size1);
  font-weight: normal;
  min-width: 120px;
}

.jp-FormGroup-contentNormal fieldset:not(:first-child) {
  margin-left: 7px;
}

.jp-FormGroup-contentNormal .field-array-of-string .array-item {
  /* Display `jp-ArrayOperations` buttons side-by-side with content except
    for small screens where flex-wrap will place them one below the other.
  */
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}

.jp-FormGroup-contentNormal .jp-objectFieldWrapper .form-group {
  padding: 2px 8px 2px var(--jp-private-settingeditor-modifier-indent);
  margin-top: 2px;
}

/* RJSF compact content (metadata-form) */

.jp-FormGroup-content.jp-FormGroup-contentCompact {
  width: 100%;
}

.jp-FormGroup-contentCompact .form-group {
  display: flex;
  padding: 0.5em 0.2em 0.5em 0;
}

.jp-FormGroup-contentCompact
  .jp-FormGroup-compactTitle
  .jp-FormGroup-description {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color2);
}

.jp-FormGroup-contentCompact .jp-FormGroup-fieldLabel {
  padding-bottom: 0.3em;
}

.jp-FormGroup-contentCompact .jp-inputFieldWrapper .form-control {
  width: 100%;
  box-sizing: border-box;
}

.jp-FormGroup-contentCompact .jp-arrayFieldWrapper .jp-FormGroup-compactTitle {
  padding-bottom: 7px;
}

.jp-FormGroup-contentCompact
  .jp-objectFieldWrapper
  .jp-objectFieldWrapper
  .form-group {
  padding: 2px 8px 2px var(--jp-private-settingeditor-modifier-indent);
  margin-top: 2px;
}

.jp-FormGroup-contentCompact ul.error-detail {
  margin-block-start: 0.5em;
  margin-block-end: 0.5em;
  padding-inline-start: 1em;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-SidePanel {
  display: flex;
  flex-direction: column;
  min-width: var(--jp-sidebar-min-width);
  overflow-y: auto;
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);
  font-size: var(--jp-ui-font-size1);
}

.jp-SidePanel-header {
  flex: 0 0 auto;
  display: flex;
  border-bottom: var(--jp-border-width) solid var(--jp-border-color2);
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  letter-spacing: 1px;
  margin: 0;
  padding: 2px;
  text-transform: uppercase;
}

.jp-SidePanel-toolbar {
  flex: 0 0 auto;
}

.jp-SidePanel-content {
  flex: 1 1 auto;
}

.jp-SidePanel-toolbar,
.jp-AccordionPanel-toolbar {
  height: var(--jp-private-toolbar-height);
}

.jp-SidePanel-toolbar.jp-Toolbar-micro {
  display: none;
}

.lm-AccordionPanel .jp-AccordionPanel-title {
  box-sizing: border-box;
  line-height: 25px;
  margin: 0;
  display: flex;
  align-items: center;
  background: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  font-size: var(--jp-ui-font-size0);
}

.jp-AccordionPanel-title {
  cursor: pointer;
  user-select: none;
  -moz-user-select: none;
  -webkit-user-select: none;
  text-transform: uppercase;
}

.lm-AccordionPanel[data-orientation='horizontal'] > .jp-AccordionPanel-title {
  /* Title is rotated for horizontal accordion panel using CSS */
  display: block;
  transform-origin: top left;
  transform: rotate(-90deg) translate(-100%);
}

.jp-AccordionPanel-title .lm-AccordionPanel-titleLabel {
  user-select: none;
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}

.jp-AccordionPanel-title .lm-AccordionPanel-titleCollapser {
  transform: rotate(-90deg);
  margin: auto 0;
  height: 16px;
}

.jp-AccordionPanel-title.lm-mod-expanded .lm-AccordionPanel-titleCollapser {
  transform: rotate(0deg);
}

.lm-AccordionPanel .jp-AccordionPanel-toolbar {
  background: none;
  box-shadow: none;
  border: none;
  margin-left: auto;
}

.lm-AccordionPanel .lm-SplitPanel-handle:hover {
  background: var(--jp-layout-color3);
}

.jp-text-truncated {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Spinner {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 10;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: var(--jp-layout-color0);
  outline: none;
}

.jp-SpinnerContent {
  font-size: 10px;
  margin: 50px auto;
  text-indent: -9999em;
  width: 3em;
  height: 3em;
  border-radius: 50%;
  background: var(--jp-brand-color3);
  background: linear-gradient(
    to right,
    #f37626 10%,
    rgba(255, 255, 255, 0) 42%
  );
  position: relative;
  animation: load3 1s infinite linear, fadeIn 1s;
}

.jp-SpinnerContent::before {
  width: 50%;
  height: 50%;
  background: #f37626;
  border-radius: 100% 0 0;
  position: absolute;
  top: 0;
  left: 0;
  content: '';
}

.jp-SpinnerContent::after {
  background: var(--jp-layout-color0);
  width: 75%;
  height: 75%;
  border-radius: 50%;
  content: '';
  margin: auto;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }

  100% {
    opacity: 1;
  }
}

@keyframes load3 {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

button.jp-mod-styled {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  border: none;
  box-sizing: border-box;
  text-align: center;
  line-height: 32px;
  height: 32px;
  padding: 0 12px;
  letter-spacing: 0.8px;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

input.jp-mod-styled {
  background: var(--jp-input-background);
  height: 28px;
  box-sizing: border-box;
  border: var(--jp-border-width) solid var(--jp-border-color1);
  padding-left: 7px;
  padding-right: 7px;
  font-size: var(--jp-ui-font-size2);
  color: var(--jp-ui-font-color0);
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

input[type='checkbox'].jp-mod-styled {
  appearance: checkbox;
  -webkit-appearance: checkbox;
  -moz-appearance: checkbox;
  height: auto;
}

input.jp-mod-styled:focus {
  border: var(--jp-border-width) solid var(--md-blue-500);
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-select-wrapper {
  display: flex;
  position: relative;
  flex-direction: column;
  padding: 1px;
  background-color: var(--jp-layout-color1);
  box-sizing: border-box;
  margin-bottom: 12px;
}

.jp-select-wrapper:not(.multiple) {
  height: 28px;
}

.jp-select-wrapper.jp-mod-focused select.jp-mod-styled {
  border: var(--jp-border-width) solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
  background-color: var(--jp-input-active-background);
}

select.jp-mod-styled:hover {
  cursor: pointer;
  color: var(--jp-ui-font-color0);
  background-color: var(--jp-input-hover-background);
  box-shadow: inset 0 0 1px rgba(0, 0, 0, 0.5);
}

select.jp-mod-styled {
  flex: 1 1 auto;
  width: 100%;
  font-size: var(--jp-ui-font-size2);
  background: var(--jp-input-background);
  color: var(--jp-ui-font-color0);
  padding: 0 25px 0 8px;
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  border-radius: 0;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

select.jp-mod-styled:not([multiple]) {
  height: 32px;
}

select.jp-mod-styled[multiple] {
  max-height: 200px;
  overflow-y: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-switch {
  display: flex;
  align-items: center;
  padding-left: 4px;
  padding-right: 4px;
  font-size: var(--jp-ui-font-size1);
  background-color: transparent;
  color: var(--jp-ui-font-color1);
  border: none;
  height: 20px;
}

.jp-switch:hover {
  background-color: var(--jp-layout-color2);
}

.jp-switch-label {
  margin-right: 5px;
  font-family: var(--jp-ui-font-family);
}

.jp-switch-track {
  cursor: pointer;
  background-color: var(--jp-switch-color, var(--jp-border-color1));
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 34px;
  height: 16px;
  width: 35px;
  position: relative;
}

.jp-switch-track::before {
  content: '';
  position: absolute;
  height: 10px;
  width: 10px;
  margin: 3px;
  left: 0;
  background-color: var(--jp-ui-inverse-font-color1);
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 50%;
}

.jp-switch[aria-checked='true'] .jp-switch-track {
  background-color: var(--jp-switch-true-position-color, var(--jp-warn-color0));
}

.jp-switch[aria-checked='true'] .jp-switch-track::before {
  /* track width (35) - margins (3 + 3) - thumb width (10) */
  left: 19px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

:root {
  --jp-private-toolbar-height: calc(
    28px + var(--jp-border-width)
  ); /* leave 28px for content */
}

.jp-Toolbar {
  color: var(--jp-ui-font-color1);
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  background: var(--jp-toolbar-background);
  min-height: var(--jp-toolbar-micro-height);
  padding: 2px;
  z-index: 8;
  overflow-x: hidden;
}

/* Toolbar items */

.jp-Toolbar > .jp-Toolbar-item.jp-Toolbar-spacer {
  flex-grow: 1;
  flex-shrink: 1;
}

.jp-Toolbar-item.jp-Toolbar-kernelStatus {
  display: inline-block;
  width: 32px;
  background-repeat: no-repeat;
  background-position: center;
  background-size: 16px;
}

.jp-Toolbar > .jp-Toolbar-item {
  flex: 0 0 auto;
  display: flex;
  padding-left: 1px;
  padding-right: 1px;
  font-size: var(--jp-ui-font-size1);
  line-height: var(--jp-private-toolbar-height);
  height: 100%;
}

/* Toolbar buttons */

/* This is the div we use to wrap the react component into a Widget */
div.jp-ToolbarButton {
  color: transparent;
  border: none;
  box-sizing: border-box;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  padding: 0;
  margin: 0;
}

button.jp-ToolbarButtonComponent {
  background: var(--jp-layout-color1);
  border: none;
  box-sizing: border-box;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  padding: 0 6px;
  margin: 0;
  height: 24px;
  border-radius: var(--jp-border-radius);
  display: flex;
  align-items: center;
  text-align: center;
  font-size: 14px;
  min-width: unset;
  min-height: unset;
}

button.jp-ToolbarButtonComponent:disabled {
  opacity: 0.4;
}

button.jp-ToolbarButtonComponent > span {
  padding: 0;
  flex: 0 0 auto;
}

button.jp-ToolbarButtonComponent .jp-ToolbarButtonComponent-label {
  font-size: var(--jp-ui-font-size1);
  line-height: 100%;
  padding-left: 2px;
  color: var(--jp-ui-font-color1);
  font-family: var(--jp-ui-font-family);
}

#jp-main-dock-panel[data-mode='single-document']
  .jp-MainAreaWidget
  > .jp-Toolbar.jp-Toolbar-micro {
  padding: 0;
  min-height: 0;
}

#jp-main-dock-panel[data-mode='single-document']
  .jp-MainAreaWidget
  > .jp-Toolbar {
  border: none;
  box-shadow: none;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-WindowedPanel-outer {
  position: relative;
  overflow-y: auto;
}

.jp-WindowedPanel-inner {
  position: relative;
}

.jp-WindowedPanel-window {
  position: absolute;
  left: 0;
  right: 0;
  overflow: visible;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* Sibling imports */

body {
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
}

/* Disable native link decoration styles everywhere outside of dialog boxes */
a {
  text-decoration: unset;
  color: unset;
}

a:hover {
  text-decoration: unset;
  color: unset;
}

/* Accessibility for links inside dialog box text */
.jp-Dialog-content a {
  text-decoration: revert;
  color: var(--jp-content-link-color);
}

.jp-Dialog-content a:hover {
  text-decoration: revert;
}

/* Styles for ui-components */
.jp-Button {
  color: var(--jp-ui-font-color2);
  border-radius: var(--jp-border-radius);
  padding: 0 12px;
  font-size: var(--jp-ui-font-size1);

  /* Copy from blueprint 3 */
  display: inline-flex;
  flex-direction: row;
  border: none;
  cursor: pointer;
  align-items: center;
  justify-content: center;
  text-align: left;
  vertical-align: middle;
  min-height: 30px;
  min-width: 30px;
}

.jp-Button:disabled {
  cursor: not-allowed;
}

.jp-Button:empty {
  padding: 0 !important;
}

.jp-Button.jp-mod-small {
  min-height: 24px;
  min-width: 24px;
  font-size: 12px;
  padding: 0 7px;
}

/* Use our own theme for hover styles */
.jp-Button.jp-mod-minimal:hover {
  background-color: var(--jp-layout-color2);
}

.jp-Button.jp-mod-minimal {
  background: none;
}

.jp-InputGroup {
  display: block;
  position: relative;
}

.jp-InputGroup input {
  box-sizing: border-box;
  border: none;
  border-radius: 0;
  background-color: transparent;
  color: var(--jp-ui-font-color0);
  box-shadow: inset 0 0 0 var(--jp-border-width) var(--jp-input-border-color);
  padding-bottom: 0;
  padding-top: 0;
  padding-left: 10px;
  padding-right: 28px;
  position: relative;
  width: 100%;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  font-size: 14px;
  font-weight: 400;
  height: 30px;
  line-height: 30px;
  outline: none;
  vertical-align: middle;
}

.jp-InputGroup input:focus {
  box-shadow: inset 0 0 0 var(--jp-border-width)
      var(--jp-input-active-box-shadow-color),
    inset 0 0 0 3px var(--jp-input-active-box-shadow-color);
}

.jp-InputGroup input:disabled {
  cursor: not-allowed;
  resize: block;
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color2);
}

.jp-InputGroup input:disabled ~ span {
  cursor: not-allowed;
  color: var(--jp-ui-font-color2);
}

.jp-InputGroup input::placeholder,
input::placeholder {
  color: var(--jp-ui-font-color2);
}

.jp-InputGroupAction {
  position: absolute;
  bottom: 1px;
  right: 0;
  padding: 6px;
}

.jp-HTMLSelect.jp-DefaultStyle select {
  background-color: initial;
  border: none;
  border-radius: 0;
  box-shadow: none;
  color: var(--jp-ui-font-color0);
  display: block;
  font-size: var(--jp-ui-font-size1);
  font-family: var(--jp-ui-font-family);
  height: 24px;
  line-height: 14px;
  padding: 0 25px 0 10px;
  text-align: left;
  -moz-appearance: none;
  -webkit-appearance: none;
}

.jp-HTMLSelect.jp-DefaultStyle select:disabled {
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color2);
  cursor: not-allowed;
  resize: block;
}

.jp-HTMLSelect.jp-DefaultStyle select:disabled ~ span {
  cursor: not-allowed;
}

/* Use our own theme for hover and option styles */
/* stylelint-disable-next-line selector-max-type */
.jp-HTMLSelect.jp-DefaultStyle select:hover,
.jp-HTMLSelect.jp-DefaultStyle select > option {
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color0);
}

select {
  box-sizing: border-box;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-StatusBar-Widget {
  display: flex;
  align-items: center;
  background: var(--jp-layout-color2);
  min-height: var(--jp-statusbar-height);
  justify-content: space-between;
  padding: 0 10px;
}

.jp-StatusBar-Left {
  display: flex;
  align-items: center;
  flex-direction: row;
}

.jp-StatusBar-Middle {
  display: flex;
  align-items: center;
}

.jp-StatusBar-Right {
  display: flex;
  align-items: center;
  flex-direction: row-reverse;
}

.jp-StatusBar-Item {
  max-height: var(--jp-statusbar-height);
  margin: 0 2px;
  height: var(--jp-statusbar-height);
  white-space: nowrap;
  text-overflow: ellipsis;
  color: var(--jp-ui-font-color1);
  padding: 0 6px;
}

.jp-mod-highlighted:hover {
  background-color: var(--jp-layout-color3);
}

.jp-mod-clicked {
  background-color: var(--jp-brand-color1);
}

.jp-mod-clicked:hover {
  background-color: var(--jp-brand-color0);
}

.jp-mod-clicked .jp-StatusBar-TextItem {
  color: var(--jp-ui-inverse-font-color1);
}

.jp-StatusBar-HoverItem {
  box-shadow: '0px 4px 4px rgba(0, 0, 0, 0.25)';
}

.jp-StatusBar-TextItem {
  font-size: var(--jp-ui-font-size1);
  font-family: var(--jp-ui-font-family);
  line-height: 24px;
  color: var(--jp-ui-font-color1);
}

.jp-StatusBar-GroupItem {
  display: flex;
  align-items: center;
  flex-direction: row;
}

.jp-Statusbar-ProgressCircle svg {
  display: block;
  margin: 0 auto;
  width: 16px;
  height: 24px;
  align-self: normal;
}

.jp-Statusbar-ProgressCircle path {
  fill: var(--jp-inverse-layout-color3);
}

.jp-Statusbar-ProgressBar-progress-bar {
  height: 10px;
  width: 100px;
  border: solid 0.25px var(--jp-brand-color2);
  border-radius: 3px;
  overflow: hidden;
  align-self: center;
}

.jp-Statusbar-ProgressBar-progress-bar > div {
  background-color: var(--jp-brand-color2);
  background-image: linear-gradient(
    -45deg,
    rgba(255, 255, 255, 0.2) 25%,
    transparent 25%,
    transparent 50%,
    rgba(255, 255, 255, 0.2) 50%,
    rgba(255, 255, 255, 0.2) 75%,
    transparent 75%,
    transparent
  );
  background-size: 40px 40px;
  float: left;
  width: 0%;
  height: 100%;
  font-size: 12px;
  line-height: 14px;
  color: #fff;
  text-align: center;
  animation: jp-Statusbar-ExecutionTime-progress-bar 2s linear infinite;
}

.jp-Statusbar-ProgressBar-progress-bar p {
  color: var(--jp-ui-font-color1);
  font-family: var(--jp-ui-font-family);
  font-size: var(--jp-ui-font-size1);
  line-height: 10px;
  width: 100px;
}

@keyframes jp-Statusbar-ExecutionTime-progress-bar {
  0% {
    background-position: 0 0;
  }

  100% {
    background-position: 40px 40px;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-commandpalette-search-height: 28px;
}

/*-----------------------------------------------------------------------------
| Overall styles
|----------------------------------------------------------------------------*/

.lm-CommandPalette {
  padding-bottom: 0;
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);

  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
}

/*-----------------------------------------------------------------------------
| Modal variant
|----------------------------------------------------------------------------*/

.jp-ModalCommandPalette {
  position: absolute;
  z-index: 10000;
  top: 38px;
  left: 30%;
  margin: 0;
  padding: 4px;
  width: 40%;
  box-shadow: var(--jp-elevation-z4);
  border-radius: 4px;
  background: var(--jp-layout-color0);
}

.jp-ModalCommandPalette .lm-CommandPalette {
  max-height: 40vh;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-close-icon::after {
  display: none;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-CommandPalette-header {
  display: none;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-CommandPalette-item {
  margin-left: 4px;
  margin-right: 4px;
}

.jp-ModalCommandPalette
  .lm-CommandPalette
  .lm-CommandPalette-item.lm-mod-disabled {
  display: none;
}

/*-----------------------------------------------------------------------------
| Search
|----------------------------------------------------------------------------*/

.lm-CommandPalette-search {
  padding: 4px;
  background-color: var(--jp-layout-color1);
  z-index: 2;
}

.lm-CommandPalette-wrapper {
  overflow: overlay;
  padding: 0 9px;
  background-color: var(--jp-input-active-background);
  height: 30px;
  box-shadow: inset 0 0 0 var(--jp-border-width) var(--jp-input-border-color);
}

.lm-CommandPalette.lm-mod-focused .lm-CommandPalette-wrapper {
  box-shadow: inset 0 0 0 1px var(--jp-input-active-box-shadow-color),
    inset 0 0 0 3px var(--jp-input-active-box-shadow-color);
}

.jp-SearchIconGroup {
  color: white;
  background-color: var(--jp-brand-color1);
  position: absolute;
  top: 4px;
  right: 4px;
  padding: 5px 5px 1px;
}

.jp-SearchIconGroup svg {
  height: 20px;
  width: 20px;
}

.jp-SearchIconGroup .jp-icon3[fill] {
  fill: var(--jp-layout-color0);
}

.lm-CommandPalette-input {
  background: transparent;
  width: calc(100% - 18px);
  float: left;
  border: none;
  outline: none;
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  line-height: var(--jp-private-commandpalette-search-height);
}

.lm-CommandPalette-input::-webkit-input-placeholder,
.lm-CommandPalette-input::-moz-placeholder,
.lm-CommandPalette-input:-ms-input-placeholder {
  color: var(--jp-ui-font-color2);
  font-size: var(--jp-ui-font-size1);
}

/*-----------------------------------------------------------------------------
| Results
|----------------------------------------------------------------------------*/

.lm-CommandPalette-header:first-child {
  margin-top: 0;
}

.lm-CommandPalette-header {
  border-bottom: solid var(--jp-border-width) var(--jp-border-color2);
  color: var(--jp-ui-font-color1);
  cursor: pointer;
  display: flex;
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  letter-spacing: 1px;
  margin-top: 8px;
  padding: 8px 0 8px 12px;
  text-transform: uppercase;
}

.lm-CommandPalette-header.lm-mod-active {
  background: var(--jp-layout-color2);
}

.lm-CommandPalette-header > mark {
  background-color: transparent;
  font-weight: bold;
  color: var(--jp-ui-font-color1);
}

.lm-CommandPalette-item {
  padding: 4px 12px 4px 4px;
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  font-weight: 400;
  display: flex;
}

.lm-CommandPalette-item.lm-mod-disabled {
  color: var(--jp-ui-font-color2);
}

.lm-CommandPalette-item.lm-mod-active {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.lm-CommandPalette-item.lm-mod-active .lm-CommandPalette-itemLabel > mark {
  color: var(--jp-ui-inverse-font-color0);
}

.lm-CommandPalette-item.lm-mod-active .jp-icon-selectable[fill] {
  fill: var(--jp-layout-color0);
}

.lm-CommandPalette-item.lm-mod-active:hover:not(.lm-mod-disabled) {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.lm-CommandPalette-item:hover:not(.lm-mod-active):not(.lm-mod-disabled) {
  background: var(--jp-layout-color2);
}

.lm-CommandPalette-itemContent {
  overflow: hidden;
}

.lm-CommandPalette-itemLabel > mark {
  color: var(--jp-ui-font-color0);
  background-color: transparent;
  font-weight: bold;
}

.lm-CommandPalette-item.lm-mod-disabled mark {
  color: var(--jp-ui-font-color2);
}

.lm-CommandPalette-item .lm-CommandPalette-itemIcon {
  margin: 0 4px 0 0;
  position: relative;
  width: 16px;
  top: 2px;
  flex: 0 0 auto;
}

.lm-CommandPalette-item.lm-mod-disabled .lm-CommandPalette-itemIcon {
  opacity: 0.6;
}

.lm-CommandPalette-item .lm-CommandPalette-itemShortcut {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemCaption {
  display: none;
}

.lm-CommandPalette-content {
  background-color: var(--jp-layout-color1);
}

.lm-CommandPalette-content:empty::after {
  content: 'No results';
  margin: auto;
  margin-top: 20px;
  width: 100px;
  display: block;
  font-size: var(--jp-ui-font-size2);
  font-family: var(--jp-ui-font-family);
  font-weight: lighter;
}

.lm-CommandPalette-emptyMessage {
  text-align: center;
  margin-top: 24px;
  line-height: 1.32;
  padding: 0 8px;
  color: var(--jp-content-font-color3);
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Dialog {
  position: absolute;
  z-index: 10000;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  top: 0;
  left: 0;
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  background: var(--jp-dialog-background);
}

.jp-Dialog-content {
  display: flex;
  flex-direction: column;
  margin-left: auto;
  margin-right: auto;
  background: var(--jp-layout-color1);
  padding: 24px 24px 12px;
  min-width: 300px;
  min-height: 150px;
  max-width: 1000px;
  max-height: 500px;
  box-sizing: border-box;
  box-shadow: var(--jp-elevation-z20);
  word-wrap: break-word;
  border-radius: var(--jp-border-radius);

  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color1);
  resize: both;
}

.jp-Dialog-content.jp-Dialog-content-small {
  max-width: 500px;
}

.jp-Dialog-button {
  overflow: visible;
}

button.jp-Dialog-button:focus {
  outline: 1px solid var(--jp-brand-color1);
  outline-offset: 4px;
  -moz-outline-radius: 0;
}

button.jp-Dialog-button:focus::-moz-focus-inner {
  border: 0;
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-accept:focus,
button.jp-Dialog-button.jp-mod-styled.jp-mod-warn:focus,
button.jp-Dialog-button.jp-mod-styled.jp-mod-reject:focus {
  outline-offset: 4px;
  -moz-outline-radius: 0;
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-accept:focus {
  outline: 1px solid var(--jp-accept-color-normal, var(--jp-brand-color1));
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-warn:focus {
  outline: 1px solid var(--jp-warn-color-normal, var(--jp-error-color1));
}

button.jp-Dialog-button.jp-mod-styled.jp-mod-reject:focus {
  outline: 1px solid var(--jp-reject-color-normal, var(--md-grey-600));
}

button.jp-Dialog-close-button {
  padding: 0;
  height: 100%;
  min-width: unset;
  min-height: unset;
}

.jp-Dialog-header {
  display: flex;
  justify-content: space-between;
  flex: 0 0 auto;
  padding-bottom: 12px;
  font-size: var(--jp-ui-font-size3);
  font-weight: 400;
  color: var(--jp-ui-font-color1);
}

.jp-Dialog-body {
  display: flex;
  flex-direction: column;
  flex: 1 1 auto;
  font-size: var(--jp-ui-font-size1);
  background: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  overflow: auto;
}

.jp-Dialog-footer {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  align-items: center;
  flex: 0 0 auto;
  margin-left: -12px;
  margin-right: -12px;
  padding: 12px;
}

.jp-Dialog-checkbox {
  padding-right: 5px;
}

.jp-Dialog-checkbox > input:focus-visible {
  outline: 1px solid var(--jp-input-active-border-color);
  outline-offset: 1px;
}

.jp-Dialog-spacer {
  flex: 1 1 auto;
}

.jp-Dialog-title {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.jp-Dialog-body > .jp-select-wrapper {
  width: 100%;
}

.jp-Dialog-body > button {
  padding: 0 16px;
}

.jp-Dialog-body > label {
  line-height: 1.4;
  color: var(--jp-ui-font-color0);
}

.jp-Dialog-button.jp-mod-styled:not(:last-child) {
  margin-right: 12px;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-Input-Boolean-Dialog {
  flex-direction: row-reverse;
  align-items: end;
  width: 100%;
}

.jp-Input-Boolean-Dialog > label {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-MainAreaWidget > :focus {
  outline: none;
}

.jp-MainAreaWidget .jp-MainAreaWidget-error {
  padding: 6px;
}

.jp-MainAreaWidget .jp-MainAreaWidget-error > pre {
  width: auto;
  padding: 10px;
  background: var(--jp-error-color3);
  border: var(--jp-border-width) solid var(--jp-error-color1);
  border-radius: var(--jp-border-radius);
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  white-space: pre-wrap;
  word-wrap: break-word;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/**
 * google-material-color v1.2.6
 * https://github.com/danlevan/google-material-color
 */
:root {
  --md-red-50: #ffebee;
  --md-red-100: #ffcdd2;
  --md-red-200: #ef9a9a;
  --md-red-300: #e57373;
  --md-red-400: #ef5350;
  --md-red-500: #f44336;
  --md-red-600: #e53935;
  --md-red-700: #d32f2f;
  --md-red-800: #c62828;
  --md-red-900: #b71c1c;
  --md-red-A100: #ff8a80;
  --md-red-A200: #ff5252;
  --md-red-A400: #ff1744;
  --md-red-A700: #d50000;
  --md-pink-50: #fce4ec;
  --md-pink-100: #f8bbd0;
  --md-pink-200: #f48fb1;
  --md-pink-300: #f06292;
  --md-pink-400: #ec407a;
  --md-pink-500: #e91e63;
  --md-pink-600: #d81b60;
  --md-pink-700: #c2185b;
  --md-pink-800: #ad1457;
  --md-pink-900: #880e4f;
  --md-pink-A100: #ff80ab;
  --md-pink-A200: #ff4081;
  --md-pink-A400: #f50057;
  --md-pink-A700: #c51162;
  --md-purple-50: #f3e5f5;
  --md-purple-100: #e1bee7;
  --md-purple-200: #ce93d8;
  --md-purple-300: #ba68c8;
  --md-purple-400: #ab47bc;
  --md-purple-500: #9c27b0;
  --md-purple-600: #8e24aa;
  --md-purple-700: #7b1fa2;
  --md-purple-800: #6a1b9a;
  --md-purple-900: #4a148c;
  --md-purple-A100: #ea80fc;
  --md-purple-A200: #e040fb;
  --md-purple-A400: #d500f9;
  --md-purple-A700: #a0f;
  --md-deep-purple-50: #ede7f6;
  --md-deep-purple-100: #d1c4e9;
  --md-deep-purple-200: #b39ddb;
  --md-deep-purple-300: #9575cd;
  --md-deep-purple-400: #7e57c2;
  --md-deep-purple-500: #673ab7;
  --md-deep-purple-600: #5e35b1;
  --md-deep-purple-700: #512da8;
  --md-deep-purple-800: #4527a0;
  --md-deep-purple-900: #311b92;
  --md-deep-purple-A100: #b388ff;
  --md-deep-purple-A200: #7c4dff;
  --md-deep-purple-A400: #651fff;
  --md-deep-purple-A700: #6200ea;
  --md-indigo-50: #e8eaf6;
  --md-indigo-100: #c5cae9;
  --md-indigo-200: #9fa8da;
  --md-indigo-300: #7986cb;
  --md-indigo-400: #5c6bc0;
  --md-indigo-500: #3f51b5;
  --md-indigo-600: #3949ab;
  --md-indigo-700: #303f9f;
  --md-indigo-800: #283593;
  --md-indigo-900: #1a237e;
  --md-indigo-A100: #8c9eff;
  --md-indigo-A200: #536dfe;
  --md-indigo-A400: #3d5afe;
  --md-indigo-A700: #304ffe;
  --md-blue-50: #e3f2fd;
  --md-blue-100: #bbdefb;
  --md-blue-200: #90caf9;
  --md-blue-300: #64b5f6;
  --md-blue-400: #42a5f5;
  --md-blue-500: #2196f3;
  --md-blue-600: #1e88e5;
  --md-blue-700: #1976d2;
  --md-blue-800: #1565c0;
  --md-blue-900: #0d47a1;
  --md-blue-A100: #82b1ff;
  --md-blue-A200: #448aff;
  --md-blue-A400: #2979ff;
  --md-blue-A700: #2962ff;
  --md-light-blue-50: #e1f5fe;
  --md-light-blue-100: #b3e5fc;
  --md-light-blue-200: #81d4fa;
  --md-light-blue-300: #4fc3f7;
  --md-light-blue-400: #29b6f6;
  --md-light-blue-500: #03a9f4;
  --md-light-blue-600: #039be5;
  --md-light-blue-700: #0288d1;
  --md-light-blue-800: #0277bd;
  --md-light-blue-900: #01579b;
  --md-light-blue-A100: #80d8ff;
  --md-light-blue-A200: #40c4ff;
  --md-light-blue-A400: #00b0ff;
  --md-light-blue-A700: #0091ea;
  --md-cyan-50: #e0f7fa;
  --md-cyan-100: #b2ebf2;
  --md-cyan-200: #80deea;
  --md-cyan-300: #4dd0e1;
  --md-cyan-400: #26c6da;
  --md-cyan-500: #00bcd4;
  --md-cyan-600: #00acc1;
  --md-cyan-700: #0097a7;
  --md-cyan-800: #00838f;
  --md-cyan-900: #006064;
  --md-cyan-A100: #84ffff;
  --md-cyan-A200: #18ffff;
  --md-cyan-A400: #00e5ff;
  --md-cyan-A700: #00b8d4;
  --md-teal-50: #e0f2f1;
  --md-teal-100: #b2dfdb;
  --md-teal-200: #80cbc4;
  --md-teal-300: #4db6ac;
  --md-teal-400: #26a69a;
  --md-teal-500: #009688;
  --md-teal-600: #00897b;
  --md-teal-700: #00796b;
  --md-teal-800: #00695c;
  --md-teal-900: #004d40;
  --md-teal-A100: #a7ffeb;
  --md-teal-A200: #64ffda;
  --md-teal-A400: #1de9b6;
  --md-teal-A700: #00bfa5;
  --md-green-50: #e8f5e9;
  --md-green-100: #c8e6c9;
  --md-green-200: #a5d6a7;
  --md-green-300: #81c784;
  --md-green-400: #66bb6a;
  --md-green-500: #4caf50;
  --md-green-600: #43a047;
  --md-green-700: #388e3c;
  --md-green-800: #2e7d32;
  --md-green-900: #1b5e20;
  --md-green-A100: #b9f6ca;
  --md-green-A200: #69f0ae;
  --md-green-A400: #00e676;
  --md-green-A700: #00c853;
  --md-light-green-50: #f1f8e9;
  --md-light-green-100: #dcedc8;
  --md-light-green-200: #c5e1a5;
  --md-light-green-300: #aed581;
  --md-light-green-400: #9ccc65;
  --md-light-green-500: #8bc34a;
  --md-light-green-600: #7cb342;
  --md-light-green-700: #689f38;
  --md-light-green-800: #558b2f;
  --md-light-green-900: #33691e;
  --md-light-green-A100: #ccff90;
  --md-light-green-A200: #b2ff59;
  --md-light-green-A400: #76ff03;
  --md-light-green-A700: #64dd17;
  --md-lime-50: #f9fbe7;
  --md-lime-100: #f0f4c3;
  --md-lime-200: #e6ee9c;
  --md-lime-300: #dce775;
  --md-lime-400: #d4e157;
  --md-lime-500: #cddc39;
  --md-lime-600: #c0ca33;
  --md-lime-700: #afb42b;
  --md-lime-800: #9e9d24;
  --md-lime-900: #827717;
  --md-lime-A100: #f4ff81;
  --md-lime-A200: #eeff41;
  --md-lime-A400: #c6ff00;
  --md-lime-A700: #aeea00;
  --md-yellow-50: #fffde7;
  --md-yellow-100: #fff9c4;
  --md-yellow-200: #fff59d;
  --md-yellow-300: #fff176;
  --md-yellow-400: #ffee58;
  --md-yellow-500: #ffeb3b;
  --md-yellow-600: #fdd835;
  --md-yellow-700: #fbc02d;
  --md-yellow-800: #f9a825;
  --md-yellow-900: #f57f17;
  --md-yellow-A100: #ffff8d;
  --md-yellow-A200: #ff0;
  --md-yellow-A400: #ffea00;
  --md-yellow-A700: #ffd600;
  --md-amber-50: #fff8e1;
  --md-amber-100: #ffecb3;
  --md-amber-200: #ffe082;
  --md-amber-300: #ffd54f;
  --md-amber-400: #ffca28;
  --md-amber-500: #ffc107;
  --md-amber-600: #ffb300;
  --md-amber-700: #ffa000;
  --md-amber-800: #ff8f00;
  --md-amber-900: #ff6f00;
  --md-amber-A100: #ffe57f;
  --md-amber-A200: #ffd740;
  --md-amber-A400: #ffc400;
  --md-amber-A700: #ffab00;
  --md-orange-50: #fff3e0;
  --md-orange-100: #ffe0b2;
  --md-orange-200: #ffcc80;
  --md-orange-300: #ffb74d;
  --md-orange-400: #ffa726;
  --md-orange-500: #ff9800;
  --md-orange-600: #fb8c00;
  --md-orange-700: #f57c00;
  --md-orange-800: #ef6c00;
  --md-orange-900: #e65100;
  --md-orange-A100: #ffd180;
  --md-orange-A200: #ffab40;
  --md-orange-A400: #ff9100;
  --md-orange-A700: #ff6d00;
  --md-deep-orange-50: #fbe9e7;
  --md-deep-orange-100: #ffccbc;
  --md-deep-orange-200: #ffab91;
  --md-deep-orange-300: #ff8a65;
  --md-deep-orange-400: #ff7043;
  --md-deep-orange-500: #ff5722;
  --md-deep-orange-600: #f4511e;
  --md-deep-orange-700: #e64a19;
  --md-deep-orange-800: #d84315;
  --md-deep-orange-900: #bf360c;
  --md-deep-orange-A100: #ff9e80;
  --md-deep-orange-A200: #ff6e40;
  --md-deep-orange-A400: #ff3d00;
  --md-deep-orange-A700: #dd2c00;
  --md-brown-50: #efebe9;
  --md-brown-100: #d7ccc8;
  --md-brown-200: #bcaaa4;
  --md-brown-300: #a1887f;
  --md-brown-400: #8d6e63;
  --md-brown-500: #795548;
  --md-brown-600: #6d4c41;
  --md-brown-700: #5d4037;
  --md-brown-800: #4e342e;
  --md-brown-900: #3e2723;
  --md-grey-50: #fafafa;
  --md-grey-100: #f5f5f5;
  --md-grey-200: #eee;
  --md-grey-300: #e0e0e0;
  --md-grey-400: #bdbdbd;
  --md-grey-500: #9e9e9e;
  --md-grey-600: #757575;
  --md-grey-700: #616161;
  --md-grey-800: #424242;
  --md-grey-900: #212121;
  --md-blue-grey-50: #eceff1;
  --md-blue-grey-100: #cfd8dc;
  --md-blue-grey-200: #b0bec5;
  --md-blue-grey-300: #90a4ae;
  --md-blue-grey-400: #78909c;
  --md-blue-grey-500: #607d8b;
  --md-blue-grey-600: #546e7a;
  --md-blue-grey-700: #455a64;
  --md-blue-grey-800: #37474f;
  --md-blue-grey-900: #263238;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| RenderedText
|----------------------------------------------------------------------------*/

:root {
  /* This is the padding value to fill the gaps between lines containing spans with background color. */
  --jp-private-code-span-padding: calc(
    (var(--jp-code-line-height) - 1) * var(--jp-code-font-size) / 2
  );
}

.jp-RenderedText {
  text-align: left;
  padding-left: var(--jp-code-padding);
  line-height: var(--jp-code-line-height);
  font-family: var(--jp-code-font-family);
}

.jp-RenderedText pre,
.jp-RenderedJavaScript pre,
.jp-RenderedHTMLCommon pre {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-code-font-size);
  border: none;
  margin: 0;
  padding: 0;
}

.jp-RenderedText pre a:link {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

.jp-RenderedText pre a:hover {
  text-decoration: underline;
  color: var(--jp-content-link-color);
}

.jp-RenderedText pre a:visited {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

/* console foregrounds and backgrounds */
.jp-RenderedText pre .ansi-black-fg {
  color: #3e424d;
}

.jp-RenderedText pre .ansi-red-fg {
  color: #e75c58;
}

.jp-RenderedText pre .ansi-green-fg {
  color: #00a250;
}

.jp-RenderedText pre .ansi-yellow-fg {
  color: #ddb62b;
}

.jp-RenderedText pre .ansi-blue-fg {
  color: #208ffb;
}

.jp-RenderedText pre .ansi-magenta-fg {
  color: #d160c4;
}

.jp-RenderedText pre .ansi-cyan-fg {
  color: #60c6c8;
}

.jp-RenderedText pre .ansi-white-fg {
  color: #c5c1b4;
}

.jp-RenderedText pre .ansi-black-bg {
  background-color: #3e424d;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-red-bg {
  background-color: #e75c58;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-green-bg {
  background-color: #00a250;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-yellow-bg {
  background-color: #ddb62b;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-blue-bg {
  background-color: #208ffb;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-magenta-bg {
  background-color: #d160c4;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-cyan-bg {
  background-color: #60c6c8;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-white-bg {
  background-color: #c5c1b4;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-black-intense-fg {
  color: #282c36;
}

.jp-RenderedText pre .ansi-red-intense-fg {
  color: #b22b31;
}

.jp-RenderedText pre .ansi-green-intense-fg {
  color: #007427;
}

.jp-RenderedText pre .ansi-yellow-intense-fg {
  color: #b27d12;
}

.jp-RenderedText pre .ansi-blue-intense-fg {
  color: #0065ca;
}

.jp-RenderedText pre .ansi-magenta-intense-fg {
  color: #a03196;
}

.jp-RenderedText pre .ansi-cyan-intense-fg {
  color: #258f8f;
}

.jp-RenderedText pre .ansi-white-intense-fg {
  color: #a1a6b2;
}

.jp-RenderedText pre .ansi-black-intense-bg {
  background-color: #282c36;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-red-intense-bg {
  background-color: #b22b31;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-green-intense-bg {
  background-color: #007427;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-yellow-intense-bg {
  background-color: #b27d12;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-blue-intense-bg {
  background-color: #0065ca;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-magenta-intense-bg {
  background-color: #a03196;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-cyan-intense-bg {
  background-color: #258f8f;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-white-intense-bg {
  background-color: #a1a6b2;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-default-inverse-fg {
  color: var(--jp-ui-inverse-font-color0);
}

.jp-RenderedText pre .ansi-default-inverse-bg {
  background-color: var(--jp-inverse-layout-color0);
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-bold {
  font-weight: bold;
}

.jp-RenderedText pre .ansi-underline {
  text-decoration: underline;
}

.jp-RenderedText[data-mime-type='application/vnd.jupyter.stderr'] {
  background: var(--jp-rendermime-error-background);
  padding-top: var(--jp-code-padding);
}

/*-----------------------------------------------------------------------------
| RenderedLatex
|----------------------------------------------------------------------------*/

.jp-RenderedLatex {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-content-font-size1);
  line-height: var(--jp-content-line-height);
}

/* Left-justify outputs.*/
.jp-OutputArea-output.jp-RenderedLatex {
  padding: var(--jp-code-padding);
  text-align: left;
}

/*-----------------------------------------------------------------------------
| RenderedHTML
|----------------------------------------------------------------------------*/

.jp-RenderedHTMLCommon {
  color: var(--jp-content-font-color1);
  font-family: var(--jp-content-font-family);
  font-size: var(--jp-content-font-size1);
  line-height: var(--jp-content-line-height);

  /* Give a bit more R padding on Markdown text to keep line lengths reasonable */
  padding-right: 20px;
}

.jp-RenderedHTMLCommon em {
  font-style: italic;
}

.jp-RenderedHTMLCommon strong {
  font-weight: bold;
}

.jp-RenderedHTMLCommon u {
  text-decoration: underline;
}

.jp-RenderedHTMLCommon a:link {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

.jp-RenderedHTMLCommon a:hover {
  text-decoration: underline;
  color: var(--jp-content-link-color);
}

.jp-RenderedHTMLCommon a:visited {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

/* Headings */

.jp-RenderedHTMLCommon h1,
.jp-RenderedHTMLCommon h2,
.jp-RenderedHTMLCommon h3,
.jp-RenderedHTMLCommon h4,
.jp-RenderedHTMLCommon h5,
.jp-RenderedHTMLCommon h6 {
  line-height: var(--jp-content-heading-line-height);
  font-weight: var(--jp-content-heading-font-weight);
  font-style: normal;
  margin: var(--jp-content-heading-margin-top) 0
    var(--jp-content-heading-margin-bottom) 0;
}

.jp-RenderedHTMLCommon h1:first-child,
.jp-RenderedHTMLCommon h2:first-child,
.jp-RenderedHTMLCommon h3:first-child,
.jp-RenderedHTMLCommon h4:first-child,
.jp-RenderedHTMLCommon h5:first-child,
.jp-RenderedHTMLCommon h6:first-child {
  margin-top: calc(0.5 * var(--jp-content-heading-margin-top));
}

.jp-RenderedHTMLCommon h1:last-child,
.jp-RenderedHTMLCommon h2:last-child,
.jp-RenderedHTMLCommon h3:last-child,
.jp-RenderedHTMLCommon h4:last-child,
.jp-RenderedHTMLCommon h5:last-child,
.jp-RenderedHTMLCommon h6:last-child {
  margin-bottom: calc(0.5 * var(--jp-content-heading-margin-bottom));
}

.jp-RenderedHTMLCommon h1 {
  font-size: var(--jp-content-font-size5);
}

.jp-RenderedHTMLCommon h2 {
  font-size: var(--jp-content-font-size4);
}

.jp-RenderedHTMLCommon h3 {
  font-size: var(--jp-content-font-size3);
}

.jp-RenderedHTMLCommon h4 {
  font-size: var(--jp-content-font-size2);
}

.jp-RenderedHTMLCommon h5 {
  font-size: var(--jp-content-font-size1);
}

.jp-RenderedHTMLCommon h6 {
  font-size: var(--jp-content-font-size0);
}

/* Lists */

/* stylelint-disable selector-max-type, selector-max-compound-selectors */

.jp-RenderedHTMLCommon ul:not(.list-inline),
.jp-RenderedHTMLCommon ol:not(.list-inline) {
  padding-left: 2em;
}

.jp-RenderedHTMLCommon ul {
  list-style: disc;
}

.jp-RenderedHTMLCommon ul ul {
  list-style: square;
}

.jp-RenderedHTMLCommon ul ul ul {
  list-style: circle;
}

.jp-RenderedHTMLCommon ol {
  list-style: decimal;
}

.jp-RenderedHTMLCommon ol ol {
  list-style: upper-alpha;
}

.jp-RenderedHTMLCommon ol ol ol {
  list-style: lower-alpha;
}

.jp-RenderedHTMLCommon ol ol ol ol {
  list-style: lower-roman;
}

.jp-RenderedHTMLCommon ol ol ol ol ol {
  list-style: decimal;
}

.jp-RenderedHTMLCommon ol,
.jp-RenderedHTMLCommon ul {
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon ul ul,
.jp-RenderedHTMLCommon ul ol,
.jp-RenderedHTMLCommon ol ul,
.jp-RenderedHTMLCommon ol ol {
  margin-bottom: 0;
}

/* stylelint-enable selector-max-type, selector-max-compound-selectors */

.jp-RenderedHTMLCommon hr {
  color: var(--jp-border-color2);
  background-color: var(--jp-border-color1);
  margin-top: 1em;
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon > pre {
  margin: 1.5em 2em;
}

.jp-RenderedHTMLCommon pre,
.jp-RenderedHTMLCommon code {
  border: 0;
  background-color: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
  font-family: var(--jp-code-font-family);
  font-size: inherit;
  line-height: var(--jp-code-line-height);
  padding: 0;
  white-space: pre-wrap;
}

.jp-RenderedHTMLCommon :not(pre) > code {
  background-color: var(--jp-layout-color2);
  padding: 1px 5px;
}

/* Tables */

.jp-RenderedHTMLCommon table {
  border-collapse: collapse;
  border-spacing: 0;
  border: none;
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  table-layout: fixed;
  margin-left: auto;
  margin-bottom: 1em;
  margin-right: auto;
}

.jp-RenderedHTMLCommon thead {
  border-bottom: var(--jp-border-width) solid var(--jp-border-color1);
  vertical-align: bottom;
}

.jp-RenderedHTMLCommon td,
.jp-RenderedHTMLCommon th,
.jp-RenderedHTMLCommon tr {
  vertical-align: middle;
  padding: 0.5em;
  line-height: normal;
  white-space: normal;
  max-width: none;
  border: none;
}

.jp-RenderedMarkdown.jp-RenderedHTMLCommon td,
.jp-RenderedMarkdown.jp-RenderedHTMLCommon th {
  max-width: none;
}

:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon td,
:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon th,
:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon tr {
  text-align: right;
}

.jp-RenderedHTMLCommon th {
  font-weight: bold;
}

.jp-RenderedHTMLCommon tbody tr:nth-child(odd) {
  background: var(--jp-layout-color0);
}

.jp-RenderedHTMLCommon tbody tr:nth-child(even) {
  background: var(--jp-rendermime-table-row-background);
}

.jp-RenderedHTMLCommon tbody tr:hover {
  background: var(--jp-rendermime-table-row-hover-background);
}

.jp-RenderedHTMLCommon p {
  text-align: left;
  margin: 0;
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon img {
  -moz-force-broken-image-icon: 1;
}

/* Restrict to direct children as other images could be nested in other content. */
.jp-RenderedHTMLCommon > img {
  display: block;
  margin-left: 0;
  margin-right: 0;
  margin-bottom: 1em;
}

/* Change color behind transparent images if they need it... */
[data-jp-theme-light='false'] .jp-RenderedImage img.jp-needs-light-background {
  background-color: var(--jp-inverse-layout-color1);
}

[data-jp-theme-light='true'] .jp-RenderedImage img.jp-needs-dark-background {
  background-color: var(--jp-inverse-layout-color1);
}

.jp-RenderedHTMLCommon img,
.jp-RenderedImage img,
.jp-RenderedHTMLCommon svg,
.jp-RenderedSVG svg {
  max-width: 100%;
  height: auto;
}

.jp-RenderedHTMLCommon img.jp-mod-unconfined,
.jp-RenderedImage img.jp-mod-unconfined,
.jp-RenderedHTMLCommon svg.jp-mod-unconfined,
.jp-RenderedSVG svg.jp-mod-unconfined {
  max-width: none;
}

.jp-RenderedHTMLCommon .alert {
  padding: var(--jp-notebook-padding);
  border: var(--jp-border-width) solid transparent;
  border-radius: var(--jp-border-radius);
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon .alert-info {
  color: var(--jp-info-color0);
  background-color: var(--jp-info-color3);
  border-color: var(--jp-info-color2);
}

.jp-RenderedHTMLCommon .alert-info hr {
  border-color: var(--jp-info-color3);
}

.jp-RenderedHTMLCommon .alert-info > p:last-child,
.jp-RenderedHTMLCommon .alert-info > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-warning {
  color: var(--jp-warn-color0);
  background-color: var(--jp-warn-color3);
  border-color: var(--jp-warn-color2);
}

.jp-RenderedHTMLCommon .alert-warning hr {
  border-color: var(--jp-warn-color3);
}

.jp-RenderedHTMLCommon .alert-warning > p:last-child,
.jp-RenderedHTMLCommon .alert-warning > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-success {
  color: var(--jp-success-color0);
  background-color: var(--jp-success-color3);
  border-color: var(--jp-success-color2);
}

.jp-RenderedHTMLCommon .alert-success hr {
  border-color: var(--jp-success-color3);
}

.jp-RenderedHTMLCommon .alert-success > p:last-child,
.jp-RenderedHTMLCommon .alert-success > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-danger {
  color: var(--jp-error-color0);
  background-color: var(--jp-error-color3);
  border-color: var(--jp-error-color2);
}

.jp-RenderedHTMLCommon .alert-danger hr {
  border-color: var(--jp-error-color3);
}

.jp-RenderedHTMLCommon .alert-danger > p:last-child,
.jp-RenderedHTMLCommon .alert-danger > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon blockquote {
  margin: 1em 2em;
  padding: 0 1em;
  border-left: 5px solid var(--jp-border-color2);
}

a.jp-InternalAnchorLink {
  visibility: hidden;
  margin-left: 8px;
  color: var(--md-blue-800);
}

h1:hover .jp-InternalAnchorLink,
h2:hover .jp-InternalAnchorLink,
h3:hover .jp-InternalAnchorLink,
h4:hover .jp-InternalAnchorLink,
h5:hover .jp-InternalAnchorLink,
h6:hover .jp-InternalAnchorLink {
  visibility: visible;
}

.jp-RenderedHTMLCommon kbd {
  background-color: var(--jp-rendermime-table-row-background);
  border: 1px solid var(--jp-border-color0);
  border-bottom-color: var(--jp-border-color2);
  border-radius: 3px;
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.25);
  display: inline-block;
  font-size: var(--jp-ui-font-size0);
  line-height: 1em;
  padding: 0.2em 0.5em;
}

/* Most direct children of .jp-RenderedHTMLCommon have a margin-bottom of 1.0.
 * At the bottom of cells this is a bit too much as there is also spacing
 * between cells. Going all the way to 0 gets too tight between markdown and
 * code cells.
 */
.jp-RenderedHTMLCommon > *:last-child {
  margin-bottom: 0.5em;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

.lm-cursor-backdrop {
  position: fixed;
  width: 200px;
  height: 200px;
  margin-top: -100px;
  margin-left: -100px;
  will-change: transform;
  z-index: 100;
}

.lm-mod-drag-image {
  will-change: transform;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-lineFormSearch {
  padding: 4px 12px;
  background-color: var(--jp-layout-color2);
  box-shadow: var(--jp-toolbar-box-shadow);
  z-index: 2;
  font-size: var(--jp-ui-font-size1);
}

.jp-lineFormCaption {
  font-size: var(--jp-ui-font-size0);
  line-height: var(--jp-ui-font-size1);
  margin-top: 4px;
  color: var(--jp-ui-font-color0);
}

.jp-baseLineForm {
  border: none;
  border-radius: 0;
  position: absolute;
  background-size: 16px;
  background-repeat: no-repeat;
  background-position: center;
  outline: none;
}

.jp-lineFormButtonContainer {
  top: 4px;
  right: 8px;
  height: 24px;
  padding: 0 12px;
  width: 12px;
}

.jp-lineFormButtonIcon {
  top: 0;
  right: 0;
  background-color: var(--jp-brand-color1);
  height: 100%;
  width: 100%;
  box-sizing: border-box;
  padding: 4px 6px;
}

.jp-lineFormButton {
  top: 0;
  right: 0;
  background-color: transparent;
  height: 100%;
  width: 100%;
  box-sizing: border-box;
}

.jp-lineFormWrapper {
  overflow: hidden;
  padding: 0 8px;
  border: 1px solid var(--jp-border-color0);
  background-color: var(--jp-input-active-background);
  height: 22px;
}

.jp-lineFormWrapperFocusWithin {
  border: var(--jp-border-width) solid var(--md-blue-500);
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-lineFormInput {
  background: transparent;
  width: 200px;
  height: 100%;
  border: none;
  outline: none;
  color: var(--jp-ui-font-color0);
  line-height: 28px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-JSONEditor {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.jp-JSONEditor-host {
  flex: 1 1 auto;
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  border-radius: 0;
  background: var(--jp-layout-color0);
  min-height: 50px;
  padding: 1px;
}

.jp-JSONEditor.jp-mod-error .jp-JSONEditor-host {
  border-color: red;
  outline-color: red;
}

.jp-JSONEditor-header {
  display: flex;
  flex: 1 0 auto;
  padding: 0 0 0 12px;
}

.jp-JSONEditor-header label {
  flex: 0 0 auto;
}

.jp-JSONEditor-commitButton {
  height: 16px;
  width: 16px;
  background-size: 18px;
  background-repeat: no-repeat;
  background-position: center;
}

.jp-JSONEditor-host.jp-mod-focused {
  background-color: var(--jp-input-active-background);
  border: 1px solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
}

.jp-Editor.jp-mod-dropTarget {
  border: var(--jp-border-width) solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/
.jp-DocumentSearch-input {
  border: none;
  outline: none;
  color: var(--jp-ui-font-color0);
  font-size: var(--jp-ui-font-size1);
  background-color: var(--jp-layout-color0);
  font-family: var(--jp-ui-font-family);
  padding: 2px 1px;
  resize: none;
}

.jp-DocumentSearch-overlay {
  position: absolute;
  background-color: var(--jp-toolbar-background);
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  border-left: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  top: 0;
  right: 0;
  z-index: 7;
  min-width: 405px;
  padding: 2px;
  font-size: var(--jp-ui-font-size1);

  --jp-private-document-search-button-height: 20px;
}

.jp-DocumentSearch-overlay button {
  background-color: var(--jp-toolbar-background);
  outline: 0;
}

.jp-DocumentSearch-overlay button:hover {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-overlay button:active {
  background-color: var(--jp-layout-color3);
}

.jp-DocumentSearch-overlay-row {
  display: flex;
  align-items: center;
  margin-bottom: 2px;
}

.jp-DocumentSearch-button-content {
  display: inline-block;
  cursor: pointer;
  box-sizing: border-box;
  width: 100%;
  height: 100%;
}

.jp-DocumentSearch-button-content svg {
  width: 100%;
  height: 100%;
}

.jp-DocumentSearch-input-wrapper {
  border: var(--jp-border-width) solid var(--jp-border-color0);
  display: flex;
  background-color: var(--jp-layout-color0);
  margin: 2px;
}

.jp-DocumentSearch-input-wrapper:focus-within {
  border-color: var(--jp-cell-editor-active-border-color);
}

.jp-DocumentSearch-toggle-wrapper,
.jp-DocumentSearch-button-wrapper {
  all: initial;
  overflow: hidden;
  display: inline-block;
  border: none;
  box-sizing: border-box;
}

.jp-DocumentSearch-toggle-wrapper {
  width: 14px;
  height: 14px;
}

.jp-DocumentSearch-button-wrapper {
  width: var(--jp-private-document-search-button-height);
  height: var(--jp-private-document-search-button-height);
}

.jp-DocumentSearch-toggle-wrapper:focus,
.jp-DocumentSearch-button-wrapper:focus {
  outline: var(--jp-border-width) solid
    var(--jp-cell-editor-active-border-color);
  outline-offset: -1px;
}

.jp-DocumentSearch-toggle-wrapper,
.jp-DocumentSearch-button-wrapper,
.jp-DocumentSearch-button-content:focus {
  outline: none;
}

.jp-DocumentSearch-toggle-placeholder {
  width: 5px;
}

.jp-DocumentSearch-input-button::before {
  display: block;
  padding-top: 100%;
}

.jp-DocumentSearch-input-button-off {
  opacity: var(--jp-search-toggle-off-opacity);
}

.jp-DocumentSearch-input-button-off:hover {
  opacity: var(--jp-search-toggle-hover-opacity);
}

.jp-DocumentSearch-input-button-on {
  opacity: var(--jp-search-toggle-on-opacity);
}

.jp-DocumentSearch-index-counter {
  padding-left: 10px;
  padding-right: 10px;
  user-select: none;
  min-width: 35px;
  display: inline-block;
}

.jp-DocumentSearch-up-down-wrapper {
  display: inline-block;
  padding-right: 2px;
  margin-left: auto;
  white-space: nowrap;
}

.jp-DocumentSearch-spacer {
  margin-left: auto;
}

.jp-DocumentSearch-up-down-wrapper button {
  outline: 0;
  border: none;
  width: var(--jp-private-document-search-button-height);
  height: var(--jp-private-document-search-button-height);
  vertical-align: middle;
  margin: 1px 5px 2px;
}

.jp-DocumentSearch-up-down-button:hover {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-up-down-button:active {
  background-color: var(--jp-layout-color3);
}

.jp-DocumentSearch-filter-button {
  border-radius: var(--jp-border-radius);
}

.jp-DocumentSearch-filter-button:hover {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-filter-button-enabled {
  background-color: var(--jp-layout-color2);
}

.jp-DocumentSearch-filter-button-enabled:hover {
  background-color: var(--jp-layout-color3);
}

.jp-DocumentSearch-search-options {
  padding: 0 8px;
  margin-left: 3px;
  width: 100%;
  display: grid;
  justify-content: start;
  grid-template-columns: 1fr 1fr;
  align-items: center;
  justify-items: stretch;
}

.jp-DocumentSearch-search-filter-disabled {
  color: var(--jp-ui-font-color2);
}

.jp-DocumentSearch-search-filter {
  display: flex;
  align-items: center;
  user-select: none;
}

.jp-DocumentSearch-regex-error {
  color: var(--jp-error-color0);
}

.jp-DocumentSearch-replace-button-wrapper {
  overflow: hidden;
  display: inline-block;
  box-sizing: border-box;
  border: var(--jp-border-width) solid var(--jp-border-color0);
  margin: auto 2px;
  padding: 1px 4px;
  height: calc(var(--jp-private-document-search-button-height) + 2px);
}

.jp-DocumentSearch-replace-button-wrapper:focus {
  border: var(--jp-border-width) solid var(--jp-cell-editor-active-border-color);
}

.jp-DocumentSearch-replace-button {
  display: inline-block;
  text-align: center;
  cursor: pointer;
  box-sizing: border-box;
  color: var(--jp-ui-font-color1);

  /* height - 2 * (padding of wrapper) */
  line-height: calc(var(--jp-private-document-search-button-height) - 2px);
  width: 100%;
  height: 100%;
}

.jp-DocumentSearch-replace-button:focus {
  outline: none;
}

.jp-DocumentSearch-replace-wrapper-class {
  margin-left: 14px;
  display: flex;
}

.jp-DocumentSearch-replace-toggle {
  border: none;
  background-color: var(--jp-toolbar-background);
  border-radius: var(--jp-border-radius);
}

.jp-DocumentSearch-replace-toggle:hover {
  background-color: var(--jp-layout-color2);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.cm-editor {
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  font-family: var(--jp-code-font-family);
  border: 0;
  border-radius: 0;
  height: auto;

  /* Changed to auto to autogrow */
}

.cm-editor pre {
  padding: 0 var(--jp-code-padding);
}

.jp-CodeMirrorEditor[data-type='inline'] .cm-dialog {
  background-color: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
}

.jp-CodeMirrorEditor {
  cursor: text;
}

/* When zoomed out 67% and 33% on a screen of 1440 width x 900 height */
@media screen and (min-width: 2138px) and (max-width: 4319px) {
  .jp-CodeMirrorEditor[data-type='inline'] .cm-cursor {
    border-left: var(--jp-code-cursor-width1) solid
      var(--jp-editor-cursor-color);
  }
}

/* When zoomed out less than 33% */
@media screen and (min-width: 4320px) {
  .jp-CodeMirrorEditor[data-type='inline'] .cm-cursor {
    border-left: var(--jp-code-cursor-width2) solid
      var(--jp-editor-cursor-color);
  }
}

.cm-editor.jp-mod-readOnly .cm-cursor {
  display: none;
}

.jp-CollaboratorCursor {
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: none;
  border-bottom: 3px solid;
  background-clip: content-box;
  margin-left: -5px;
  margin-right: -5px;
}

.cm-searching,
.cm-searching span {
  /* `.cm-searching span`: we need to override syntax highlighting */
  background-color: var(--jp-search-unselected-match-background-color);
  color: var(--jp-search-unselected-match-color);
}

.cm-searching::selection,
.cm-searching span::selection {
  background-color: var(--jp-search-unselected-match-background-color);
  color: var(--jp-search-unselected-match-color);
}

.jp-current-match > .cm-searching,
.jp-current-match > .cm-searching span,
.cm-searching > .jp-current-match,
.cm-searching > .jp-current-match span {
  background-color: var(--jp-search-selected-match-background-color);
  color: var(--jp-search-selected-match-color);
}

.jp-current-match > .cm-searching::selection,
.cm-searching > .jp-current-match::selection,
.jp-current-match > .cm-searching span::selection {
  background-color: var(--jp-search-selected-match-background-color);
  color: var(--jp-search-selected-match-color);
}

.cm-trailingspace {
  background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAFCAYAAAB4ka1VAAAAsElEQVQIHQGlAFr/AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA7+r3zKmT0/+pk9P/7+r3zAAAAAAAAAAABAAAAAAAAAAA6OPzM+/q9wAAAAAA6OPzMwAAAAAAAAAAAgAAAAAAAAAAGR8NiRQaCgAZIA0AGR8NiQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQyoYJ/SY80UAAAAASUVORK5CYII=);
  background-position: center left;
  background-repeat: repeat-x;
}

.jp-CollaboratorCursor-hover {
  position: absolute;
  z-index: 1;
  transform: translateX(-50%);
  color: white;
  border-radius: 3px;
  padding-left: 4px;
  padding-right: 4px;
  padding-top: 1px;
  padding-bottom: 1px;
  text-align: center;
  font-size: var(--jp-ui-font-size1);
  white-space: nowrap;
}

.jp-CodeMirror-ruler {
  border-left: 1px dashed var(--jp-border-color2);
}

/* Styles for shared cursors (remote cursor locations and selected ranges) */
.jp-CodeMirrorEditor .cm-ySelectionCaret {
  position: relative;
  border-left: 1px solid black;
  margin-left: -1px;
  margin-right: -1px;
  box-sizing: border-box;
}

.jp-CodeMirrorEditor .cm-ySelectionCaret > .cm-ySelectionInfo {
  white-space: nowrap;
  position: absolute;
  top: -1.15em;
  padding-bottom: 0.05em;
  left: -1px;
  font-size: 0.95em;
  font-family: var(--jp-ui-font-family);
  font-weight: bold;
  line-height: normal;
  user-select: none;
  color: white;
  padding-left: 2px;
  padding-right: 2px;
  z-index: 101;
  transition: opacity 0.3s ease-in-out;
}

.jp-CodeMirrorEditor .cm-ySelectionInfo {
  transition-delay: 0.7s;
  opacity: 0;
}

.jp-CodeMirrorEditor .cm-ySelectionCaret:hover > .cm-ySelectionInfo {
  opacity: 1;
  transition-delay: 0s;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-MimeDocument {
  outline: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-filebrowser-button-height: 28px;
  --jp-private-filebrowser-button-width: 48px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-FileBrowser .jp-SidePanel-content {
  display: flex;
  flex-direction: column;
}

.jp-FileBrowser-toolbar.jp-Toolbar {
  flex-wrap: wrap;
  row-gap: 12px;
  border-bottom: none;
  height: auto;
  margin: 8px 12px 0;
  box-shadow: none;
  padding: 0;
  justify-content: flex-start;
}

.jp-FileBrowser-Panel {
  flex: 1 1 auto;
  display: flex;
  flex-direction: column;
}

.jp-BreadCrumbs {
  flex: 0 0 auto;
  margin: 8px 12px;
}

.jp-BreadCrumbs-item {
  margin: 0 2px;
  padding: 0 2px;
  border-radius: var(--jp-border-radius);
  cursor: pointer;
}

.jp-BreadCrumbs-item:hover {
  background-color: var(--jp-layout-color2);
}

.jp-BreadCrumbs-item:first-child {
  margin-left: 0;
}

.jp-BreadCrumbs-item.jp-mod-dropTarget {
  background-color: var(--jp-brand-color2);
  opacity: 0.7;
}

/*-----------------------------------------------------------------------------
| Buttons
|----------------------------------------------------------------------------*/

.jp-FileBrowser-toolbar > .jp-Toolbar-item {
  flex: 0 0 auto;
  padding-left: 0;
  padding-right: 2px;
  align-items: center;
  height: unset;
}

.jp-FileBrowser-toolbar > .jp-Toolbar-item .jp-ToolbarButtonComponent {
  width: 40px;
}

/*-----------------------------------------------------------------------------
| Other styles
|----------------------------------------------------------------------------*/

.jp-FileDialog.jp-mod-conflict input {
  color: var(--jp-error-color1);
}

.jp-FileDialog .jp-new-name-title {
  margin-top: 12px;
}

.jp-LastModified-hidden {
  display: none;
}

.jp-FileSize-hidden {
  display: none;
}

.jp-FileBrowser .lm-AccordionPanel > h3:first-child {
  display: none;
}

/*-----------------------------------------------------------------------------
| DirListing
|----------------------------------------------------------------------------*/

.jp-DirListing {
  flex: 1 1 auto;
  display: flex;
  flex-direction: column;
  outline: 0;
}

.jp-DirListing-header {
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  align-items: center;
  overflow: hidden;
  border-top: var(--jp-border-width) solid var(--jp-border-color2);
  border-bottom: var(--jp-border-width) solid var(--jp-border-color1);
  box-shadow: var(--jp-toolbar-box-shadow);
  z-index: 2;
}

.jp-DirListing-headerItem {
  padding: 4px 12px 2px;
  font-weight: 500;
}

.jp-DirListing-headerItem:hover {
  background: var(--jp-layout-color2);
}

.jp-DirListing-headerItem.jp-id-name {
  flex: 1 0 84px;
}

.jp-DirListing-headerItem.jp-id-modified {
  flex: 0 0 112px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
}

.jp-DirListing-headerItem.jp-id-filesize {
  flex: 0 0 75px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
}

.jp-id-narrow {
  display: none;
  flex: 0 0 5px;
  padding: 4px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
  color: var(--jp-border-color2);
}

.jp-DirListing-narrow .jp-id-narrow {
  display: block;
}

.jp-DirListing-narrow .jp-id-modified,
.jp-DirListing-narrow .jp-DirListing-itemModified {
  display: none;
}

.jp-DirListing-headerItem.jp-mod-selected {
  font-weight: 600;
}

/* increase specificity to override bundled default */
.jp-DirListing-content {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  list-style-type: none;
  overflow: auto;
  background-color: var(--jp-layout-color1);
}

.jp-DirListing-content mark {
  color: var(--jp-ui-font-color0);
  background-color: transparent;
  font-weight: bold;
}

.jp-DirListing-content .jp-DirListing-item.jp-mod-selected mark {
  color: var(--jp-ui-inverse-font-color0);
}

/* Style the directory listing content when a user drops a file to upload */
.jp-DirListing.jp-mod-native-drop .jp-DirListing-content {
  outline: 5px dashed rgba(128, 128, 128, 0.5);
  outline-offset: -10px;
  cursor: copy;
}

.jp-DirListing-item {
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 4px 12px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-DirListing-checkboxWrapper {
  /* Increases hit area of checkbox. */
  padding: 4px;
}

.jp-DirListing-header
  .jp-DirListing-checkboxWrapper
  + .jp-DirListing-headerItem {
  padding-left: 4px;
}

.jp-DirListing-content .jp-DirListing-checkboxWrapper {
  position: relative;
  left: -4px;
  margin: -4px 0 -4px -8px;
}

.jp-DirListing-checkboxWrapper.jp-mod-visible {
  visibility: visible;
}

/* For devices that support hovering, hide checkboxes until hovered, selected...
*/
@media (hover: hover) {
  .jp-DirListing-checkboxWrapper {
    visibility: hidden;
  }

  .jp-DirListing-item:hover .jp-DirListing-checkboxWrapper,
  .jp-DirListing-item.jp-mod-selected .jp-DirListing-checkboxWrapper {
    visibility: visible;
  }
}

.jp-DirListing-item[data-is-dot] {
  opacity: 75%;
}

.jp-DirListing-item.jp-mod-selected {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.jp-DirListing-item.jp-mod-dropTarget {
  background: var(--jp-brand-color3);
}

.jp-DirListing-item:hover:not(.jp-mod-selected) {
  background: var(--jp-layout-color2);
}

.jp-DirListing-itemIcon {
  flex: 0 0 20px;
  margin-right: 4px;
}

.jp-DirListing-itemText {
  flex: 1 0 64px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  user-select: none;
}

.jp-DirListing-itemText:focus {
  outline-width: 2px;
  outline-color: var(--jp-inverse-layout-color1);
  outline-style: solid;
  outline-offset: 1px;
}

.jp-DirListing-item.jp-mod-selected .jp-DirListing-itemText:focus {
  outline-color: var(--jp-layout-color1);
}

.jp-DirListing-itemModified {
  flex: 0 0 125px;
  text-align: right;
}

.jp-DirListing-itemFileSize {
  flex: 0 0 90px;
  text-align: right;
}

.jp-DirListing-editor {
  flex: 1 0 64px;
  outline: none;
  border: none;
  color: var(--jp-ui-font-color1);
  background-color: var(--jp-layout-color1);
}

.jp-DirListing-item.jp-mod-running .jp-DirListing-itemIcon::before {
  color: var(--jp-success-color1);
  content: '\25CF';
  font-size: 8px;
  position: absolute;
  left: -8px;
}

.jp-DirListing-item.jp-mod-running.jp-mod-selected
  .jp-DirListing-itemIcon::before {
  color: var(--jp-ui-inverse-font-color1);
}

.jp-DirListing-item.lm-mod-drag-image,
.jp-DirListing-item.jp-mod-selected.lm-mod-drag-image {
  font-size: var(--jp-ui-font-size1);
  padding-left: 4px;
  margin-left: 4px;
  width: 160px;
  background-color: var(--jp-ui-inverse-font-color2);
  box-shadow: var(--jp-elevation-z2);
  border-radius: 0;
  color: var(--jp-ui-font-color1);
  transform: translateX(-40%) translateY(-58%);
}

.jp-Document {
  min-width: 120px;
  min-height: 120px;
  outline: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Main OutputArea
| OutputArea has a list of Outputs
|----------------------------------------------------------------------------*/

.jp-OutputArea {
  overflow-y: auto;
}

.jp-OutputArea-child {
  display: table;
  table-layout: fixed;
  width: 100%;
  overflow: hidden;
}

.jp-OutputPrompt {
  width: var(--jp-cell-prompt-width);
  color: var(--jp-cell-outprompt-font-color);
  font-family: var(--jp-cell-prompt-font-family);
  padding: var(--jp-code-padding);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
  opacity: var(--jp-cell-prompt-opacity);

  /* Right align prompt text, don't wrap to handle large prompt numbers */
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;

  /* Disable text selection */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-OutputArea-prompt {
  display: table-cell;
  vertical-align: top;
}

.jp-OutputArea-output {
  display: table-cell;
  width: 100%;
  height: auto;
  overflow: auto;
  user-select: text;
  -moz-user-select: text;
  -webkit-user-select: text;
  -ms-user-select: text;
}

.jp-OutputArea .jp-RenderedText {
  padding-left: 1ch;
}

/**
 * Prompt overlay.
 */

.jp-OutputArea-promptOverlay {
  position: absolute;
  top: 0;
  width: var(--jp-cell-prompt-width);
  height: 100%;
  opacity: 0.5;
}

.jp-OutputArea-promptOverlay:hover {
  background: var(--jp-layout-color2);
  box-shadow: inset 0 0 1px var(--jp-inverse-layout-color0);
  cursor: zoom-out;
}

.jp-mod-outputsScrolled .jp-OutputArea-promptOverlay:hover {
  cursor: zoom-in;
}

/**
 * Isolated output.
 */
.jp-OutputArea-output.jp-mod-isolated {
  width: 100%;
  display: block;
}

/*
When drag events occur, `lm-mod-override-cursor` is added to the body.
Because iframes steal all cursor events, the following two rules are necessary
to suppress pointer events while resize drags are occurring. There may be a
better solution to this problem.
*/
body.lm-mod-override-cursor .jp-OutputArea-output.jp-mod-isolated {
  position: relative;
}

body.lm-mod-override-cursor .jp-OutputArea-output.jp-mod-isolated::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

/* pre */

.jp-OutputArea-output pre {
  border: none;
  margin: 0;
  padding: 0;
  overflow-x: auto;
  overflow-y: auto;
  word-break: break-all;
  word-wrap: break-word;
  white-space: pre-wrap;
}

/* tables */

.jp-OutputArea-output.jp-RenderedHTMLCommon table {
  margin-left: 0;
  margin-right: 0;
}

/* description lists */

.jp-OutputArea-output dl,
.jp-OutputArea-output dt,
.jp-OutputArea-output dd {
  display: block;
}

.jp-OutputArea-output dl {
  width: 100%;
  overflow: hidden;
  padding: 0;
  margin: 0;
}

.jp-OutputArea-output dt {
  font-weight: bold;
  float: left;
  width: 20%;
  padding: 0;
  margin: 0;
}

.jp-OutputArea-output dd {
  float: left;
  width: 80%;
  padding: 0;
  margin: 0;
}

.jp-TrimmedOutputs pre {
  background: var(--jp-layout-color3);
  font-size: calc(var(--jp-code-font-size) * 1.4);
  text-align: center;
  text-transform: uppercase;
}

/* Hide the gutter in case of
 *  - nested output areas (e.g. in the case of output widgets)
 *  - mirrored output areas
 */
.jp-OutputArea .jp-OutputArea .jp-OutputArea-prompt {
  display: none;
}

/* Hide empty lines in the output area, for instance due to cleared widgets */
.jp-OutputArea-prompt:empty {
  padding: 0;
  border: 0;
}

/*-----------------------------------------------------------------------------
| executeResult is added to any Output-result for the display of the object
| returned by a cell
|----------------------------------------------------------------------------*/

.jp-OutputArea-output.jp-OutputArea-executeResult {
  margin-left: 0;
  width: 100%;
}

/* Text output with the Out[] prompt needs a top padding to match the
 * alignment of the Out[] prompt itself.
 */
.jp-OutputArea-executeResult .jp-RenderedText.jp-OutputArea-output {
  padding-top: var(--jp-code-padding);
  border-top: var(--jp-border-width) solid transparent;
}

/*-----------------------------------------------------------------------------
| The Stdin output
|----------------------------------------------------------------------------*/

.jp-Stdin-prompt {
  color: var(--jp-content-font-color0);
  padding-right: var(--jp-code-padding);
  vertical-align: baseline;
  flex: 0 0 auto;
}

.jp-Stdin-input {
  font-family: var(--jp-code-font-family);
  font-size: inherit;
  color: inherit;
  background-color: inherit;
  width: 42%;
  min-width: 200px;

  /* make sure input baseline aligns with prompt */
  vertical-align: baseline;

  /* padding + margin = 0.5em between prompt and cursor */
  padding: 0 0.25em;
  margin: 0 0.25em;
  flex: 0 0 70%;
}

.jp-Stdin-input::placeholder {
  opacity: 0;
}

.jp-Stdin-input:focus {
  box-shadow: none;
}

.jp-Stdin-input:focus::placeholder {
  opacity: 1;
}

/*-----------------------------------------------------------------------------
| Output Area View
|----------------------------------------------------------------------------*/

.jp-LinkedOutputView .jp-OutputArea {
  height: 100%;
  display: block;
}

.jp-LinkedOutputView .jp-OutputArea-output:only-child {
  height: 100%;
}

/*-----------------------------------------------------------------------------
| Printing
|----------------------------------------------------------------------------*/

@media print {
  .jp-OutputArea-child {
    break-inside: avoid-page;
  }
}

/*-----------------------------------------------------------------------------
| Mobile
|----------------------------------------------------------------------------*/
@media only screen and (max-width: 760px) {
  .jp-OutputPrompt {
    display: table-row;
    text-align: left;
  }

  .jp-OutputArea-child .jp-OutputArea-output {
    display: table-row;
    margin-left: var(--jp-notebook-padding);
  }
}

/* Trimmed outputs warning */
.jp-TrimmedOutputs > a {
  margin: 10px;
  text-decoration: none;
  cursor: pointer;
}

.jp-TrimmedOutputs > a:hover {
  text-decoration: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Table of Contents
|----------------------------------------------------------------------------*/

:root {
  --jp-private-toc-active-width: 4px;
}

.jp-TableOfContents {
  display: flex;
  flex-direction: column;
  background: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  height: 100%;
}

.jp-TableOfContents-placeholder {
  text-align: center;
}

.jp-TableOfContents-placeholderContent {
  color: var(--jp-content-font-color2);
  padding: 8px;
}

.jp-TableOfContents-placeholderContent > h3 {
  margin-bottom: var(--jp-content-heading-margin-bottom);
}

.jp-TableOfContents .jp-SidePanel-content {
  overflow-y: auto;
}

.jp-TableOfContents-tree {
  margin: 4px;
}

.jp-TableOfContents ol {
  list-style-type: none;
}

/* stylelint-disable-next-line selector-max-type */
.jp-TableOfContents li > ol {
  /* Align left border with triangle icon center */
  padding-left: 11px;
}

.jp-TableOfContents-content {
  /* left margin for the active heading indicator */
  margin: 0 0 0 var(--jp-private-toc-active-width);
  padding: 0;
  background-color: var(--jp-layout-color1);
}

.jp-tocItem {
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-tocItem-heading {
  display: flex;
  cursor: pointer;
}

.jp-tocItem-heading:hover {
  background-color: var(--jp-layout-color2);
}

.jp-tocItem-content {
  display: block;
  padding: 4px 0;
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow-x: hidden;
}

.jp-tocItem-collapser {
  height: 20px;
  margin: 2px 2px 0;
  padding: 0;
  background: none;
  border: none;
  cursor: pointer;
}

.jp-tocItem-collapser:hover {
  background-color: var(--jp-layout-color3);
}

/* Active heading indicator */

.jp-tocItem-heading::before {
  content: ' ';
  background: transparent;
  width: var(--jp-private-toc-active-width);
  height: 24px;
  position: absolute;
  left: 0;
  border-radius: var(--jp-border-radius);
}

.jp-tocItem-heading.jp-tocItem-active::before {
  background-color: var(--jp-brand-color1);
}

.jp-tocItem-heading:hover.jp-tocItem-active::before {
  background: var(--jp-brand-color0);
  opacity: 1;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Collapser {
  flex: 0 0 var(--jp-cell-collapser-width);
  padding: 0;
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
  border-radius: var(--jp-border-radius);
  opacity: 1;
}

.jp-Collapser-child {
  display: block;
  width: 100%;
  box-sizing: border-box;

  /* height: 100% doesn't work because the height of its parent is computed from content */
  position: absolute;
  top: 0;
  bottom: 0;
}

/*-----------------------------------------------------------------------------
| Printing
|----------------------------------------------------------------------------*/

/*
Hiding collapsers in print mode.

Note: input and output wrappers have "display: block" propery in print mode.
*/

@media print {
  .jp-Collapser {
    display: none;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Header/Footer
|----------------------------------------------------------------------------*/

/* Hidden by zero height by default */
.jp-CellHeader,
.jp-CellFooter {
  height: 0;
  width: 100%;
  padding: 0;
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Input
|----------------------------------------------------------------------------*/

/* All input areas */
.jp-InputArea {
  display: table;
  table-layout: fixed;
  width: 100%;
  overflow: hidden;
}

.jp-InputArea-editor {
  display: table-cell;
  overflow: hidden;
  vertical-align: top;

  /* This is the non-active, default styling */
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  border-radius: 0;
  background: var(--jp-cell-editor-background);
}

.jp-InputPrompt {
  display: table-cell;
  vertical-align: top;
  width: var(--jp-cell-prompt-width);
  color: var(--jp-cell-inprompt-font-color);
  font-family: var(--jp-cell-prompt-font-family);
  padding: var(--jp-code-padding);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  opacity: var(--jp-cell-prompt-opacity);
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;

  /* Right align prompt text, don't wrap to handle large prompt numbers */
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;

  /* Disable text selection */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/*-----------------------------------------------------------------------------
| Mobile
|----------------------------------------------------------------------------*/
@media only screen and (max-width: 760px) {
  .jp-InputArea-editor {
    display: table-row;
    margin-left: var(--jp-notebook-padding);
  }

  .jp-InputPrompt {
    display: table-row;
    text-align: left;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Placeholder
|----------------------------------------------------------------------------*/

.jp-Placeholder {
  display: table;
  table-layout: fixed;
  width: 100%;
}

.jp-Placeholder-prompt {
  display: table-cell;
  box-sizing: border-box;
}

.jp-Placeholder-content {
  display: table-cell;
  padding: 4px 6px;
  border: 1px solid transparent;
  border-radius: 0;
  background: none;
  box-sizing: border-box;
  cursor: pointer;
}

.jp-Placeholder-contentContainer {
  display: flex;
}

.jp-Placeholder-content:hover,
.jp-InputPlaceholder > .jp-Placeholder-content:hover {
  border-color: var(--jp-layout-color3);
}

.jp-Placeholder-content .jp-MoreHorizIcon {
  width: 32px;
  height: 16px;
  border: 1px solid transparent;
  border-radius: var(--jp-border-radius);
}

.jp-Placeholder-content .jp-MoreHorizIcon:hover {
  border: 1px solid var(--jp-border-color1);
  box-shadow: 0 0 2px 0 rgba(0, 0, 0, 0.25);
  background-color: var(--jp-layout-color0);
}

.jp-PlaceholderText {
  white-space: nowrap;
  overflow-x: hidden;
  color: var(--jp-inverse-layout-color3);
  font-family: var(--jp-code-font-family);
}

.jp-InputPlaceholder > .jp-Placeholder-content {
  border-color: var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Private CSS variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-cell-scrolling-output-offset: 5px;
}

/*-----------------------------------------------------------------------------
| Cell
|----------------------------------------------------------------------------*/

.jp-Cell {
  padding: var(--jp-cell-padding);
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Common input/output
|----------------------------------------------------------------------------*/

.jp-Cell-inputWrapper,
.jp-Cell-outputWrapper {
  display: flex;
  flex-direction: row;
  padding: 0;
  margin: 0;

  /* Added to reveal the box-shadow on the input and output collapsers. */
  overflow: visible;
}

/* Only input/output areas inside cells */
.jp-Cell-inputArea,
.jp-Cell-outputArea {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Collapser
|----------------------------------------------------------------------------*/

/* Make the output collapser disappear when there is not output, but do so
 * in a manner that leaves it in the layout and preserves its width.
 */
.jp-Cell.jp-mod-noOutputs .jp-Cell-outputCollapser {
  border: none !important;
  background: transparent !important;
}

.jp-Cell:not(.jp-mod-noOutputs) .jp-Cell-outputCollapser {
  min-height: var(--jp-cell-collapser-min-height);
}

/*-----------------------------------------------------------------------------
| Output
|----------------------------------------------------------------------------*/

/* Put a space between input and output when there IS output */
.jp-Cell:not(.jp-mod-noOutputs) .jp-Cell-outputWrapper {
  margin-top: 5px;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea {
  overflow-y: auto;
  max-height: 24em;
  margin-left: var(--jp-private-cell-scrolling-output-offset);
  resize: vertical;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea[style*='height'] {
  max-height: unset;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea::after {
  content: ' ';
  box-shadow: inset 0 0 6px 2px rgb(0 0 0 / 30%);
  width: 100%;
  height: 100%;
  position: sticky;
  bottom: 0;
  top: 0;
  margin-top: -50%;
  float: left;
  display: block;
  pointer-events: none;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-child {
  padding-top: 6px;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-prompt {
  width: calc(
    var(--jp-cell-prompt-width) - var(--jp-private-cell-scrolling-output-offset)
  );
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-promptOverlay {
  left: calc(-1 * var(--jp-private-cell-scrolling-output-offset));
}

/*-----------------------------------------------------------------------------
| CodeCell
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| MarkdownCell
|----------------------------------------------------------------------------*/

.jp-MarkdownOutput {
  display: table-cell;
  width: 100%;
  margin-top: 0;
  margin-bottom: 0;
  padding-left: var(--jp-code-padding);
}

.jp-MarkdownOutput.jp-RenderedHTMLCommon {
  overflow: auto;
}

/* collapseHeadingButton (show always if hiddenCellsButton is _not_ shown) */
.jp-collapseHeadingButton {
  display: flex;
  min-height: var(--jp-cell-collapser-min-height);
  font-size: var(--jp-code-font-size);
  position: absolute;
  background-color: transparent;
  background-size: 25px;
  background-repeat: no-repeat;
  background-position-x: center;
  background-position-y: top;
  background-image: var(--jp-icon-caret-down);
  right: 0;
  top: 0;
  bottom: 0;
}

.jp-collapseHeadingButton.jp-mod-collapsed {
  background-image: var(--jp-icon-caret-right);
}

/*
 set the container font size to match that of content
 so that the nested collapse buttons have the right size
*/
.jp-MarkdownCell .jp-InputPrompt {
  font-size: var(--jp-content-font-size1);
}

/*
  Align collapseHeadingButton with cell top header
  The font sizes are identical to the ones in packages/rendermime/style/base.css
*/
.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='1'] {
  font-size: var(--jp-content-font-size5);
  background-position-y: calc(0.3 * var(--jp-content-font-size5));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='2'] {
  font-size: var(--jp-content-font-size4);
  background-position-y: calc(0.3 * var(--jp-content-font-size4));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='3'] {
  font-size: var(--jp-content-font-size3);
  background-position-y: calc(0.3 * var(--jp-content-font-size3));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='4'] {
  font-size: var(--jp-content-font-size2);
  background-position-y: calc(0.3 * var(--jp-content-font-size2));
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='5'] {
  font-size: var(--jp-content-font-size1);
  background-position-y: top;
}

.jp-mod-rendered .jp-collapseHeadingButton[data-heading-level='6'] {
  font-size: var(--jp-content-font-size0);
  background-position-y: top;
}

/* collapseHeadingButton (show only on (hover,active) if hiddenCellsButton is shown) */
.jp-Notebook.jp-mod-showHiddenCellsButton .jp-collapseHeadingButton {
  display: none;
}

.jp-Notebook.jp-mod-showHiddenCellsButton
  :is(.jp-MarkdownCell:hover, .jp-mod-active)
  .jp-collapseHeadingButton {
  display: flex;
}

/* showHiddenCellsButton (only show if jp-mod-showHiddenCellsButton is set, which
is a consequence of the showHiddenCellsButton option in Notebook Settings)*/
.jp-Notebook.jp-mod-showHiddenCellsButton .jp-showHiddenCellsButton {
  margin-left: calc(var(--jp-cell-prompt-width) + 2 * var(--jp-code-padding));
  margin-top: var(--jp-code-padding);
  border: 1px solid var(--jp-border-color2);
  background-color: var(--jp-border-color3) !important;
  color: var(--jp-content-font-color0) !important;
  display: flex;
}

.jp-Notebook.jp-mod-showHiddenCellsButton .jp-showHiddenCellsButton:hover {
  background-color: var(--jp-border-color2) !important;
}

.jp-showHiddenCellsButton {
  display: none;
}

/*-----------------------------------------------------------------------------
| Printing
|----------------------------------------------------------------------------*/

/*
Using block instead of flex to allow the use of the break-inside CSS property for
cell outputs.
*/

@media print {
  .jp-Cell-inputWrapper,
  .jp-Cell-outputWrapper {
    display: block;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-notebook-toolbar-padding: 2px 5px 2px 2px;
}

/*-----------------------------------------------------------------------------

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-NotebookPanel-toolbar {
  padding: var(--jp-notebook-toolbar-padding);

  /* disable paint containment from lumino 2.0 default strict CSS containment */
  contain: style size !important;
}

.jp-Toolbar-item.jp-Notebook-toolbarCellType .jp-select-wrapper.jp-mod-focused {
  border: none;
  box-shadow: none;
}

.jp-Notebook-toolbarCellTypeDropdown select {
  height: 24px;
  font-size: var(--jp-ui-font-size1);
  line-height: 14px;
  border-radius: 0;
  display: block;
}

.jp-Notebook-toolbarCellTypeDropdown span {
  top: 5px !important;
}

.jp-Toolbar-responsive-popup {
  position: absolute;
  height: fit-content;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-end;
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  background: var(--jp-toolbar-background);
  min-height: var(--jp-toolbar-micro-height);
  padding: var(--jp-notebook-toolbar-padding);
  z-index: 1;
  right: 0;
  top: 0;
}

.jp-Toolbar > .jp-Toolbar-responsive-opener {
  margin-left: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-Notebook-ExecutionIndicator {
  position: relative;
  display: inline-block;
  height: 100%;
  z-index: 9997;
}

.jp-Notebook-ExecutionIndicator-tooltip {
  visibility: hidden;
  height: auto;
  width: max-content;
  width: -moz-max-content;
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color1);
  text-align: justify;
  border-radius: 6px;
  padding: 0 5px;
  position: fixed;
  display: table;
}

.jp-Notebook-ExecutionIndicator-tooltip.up {
  transform: translateX(-50%) translateY(-100%) translateY(-32px);
}

.jp-Notebook-ExecutionIndicator-tooltip.down {
  transform: translateX(calc(-100% + 16px)) translateY(5px);
}

.jp-Notebook-ExecutionIndicator-tooltip.hidden {
  display: none;
}

.jp-Notebook-ExecutionIndicator:hover .jp-Notebook-ExecutionIndicator-tooltip {
  visibility: visible;
}

.jp-Notebook-ExecutionIndicator span {
  font-size: var(--jp-ui-font-size1);
  font-family: var(--jp-ui-font-family);
  color: var(--jp-ui-font-color1);
  line-height: 24px;
  display: block;
}

.jp-Notebook-ExecutionIndicator-progress-bar {
  display: flex;
  justify-content: center;
  height: 100%;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/*
 * Execution indicator
 */
.jp-tocItem-content::after {
  content: '';

  /* Must be identical to form a circle */
  width: 12px;
  height: 12px;
  background: none;
  border: none;
  position: absolute;
  right: 0;
}

.jp-tocItem-content[data-running='0']::after {
  border-radius: 50%;
  border: var(--jp-border-width) solid var(--jp-inverse-layout-color3);
  background: none;
}

.jp-tocItem-content[data-running='1']::after {
  border-radius: 50%;
  border: var(--jp-border-width) solid var(--jp-inverse-layout-color3);
  background-color: var(--jp-inverse-layout-color3);
}

.jp-tocItem-content[data-running='0'],
.jp-tocItem-content[data-running='1'] {
  margin-right: 12px;
}

/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

.jp-Notebook-footer {
  height: 27px;
  margin-left: calc(
    var(--jp-cell-prompt-width) + var(--jp-cell-collapser-width) +
      var(--jp-cell-padding)
  );
  width: calc(
    100% -
      (
        var(--jp-cell-prompt-width) + var(--jp-cell-collapser-width) +
          var(--jp-cell-padding) + var(--jp-cell-padding)
      )
  );
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  color: var(--jp-ui-font-color3);
  margin-top: 6px;
  background: none;
  cursor: pointer;
}

.jp-Notebook-footer:focus {
  border-color: var(--jp-cell-editor-active-border-color);
}

/* For devices that support hovering, hide footer until hover */
@media (hover: hover) {
  .jp-Notebook-footer {
    opacity: 0;
  }

  .jp-Notebook-footer:focus,
  .jp-Notebook-footer:hover {
    opacity: 1;
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Imports
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| CSS variables
|----------------------------------------------------------------------------*/

:root {
  --jp-side-by-side-output-size: 1fr;
  --jp-side-by-side-resized-cell: var(--jp-side-by-side-output-size);
  --jp-private-notebook-dragImage-width: 304px;
  --jp-private-notebook-dragImage-height: 36px;
  --jp-private-notebook-selected-color: var(--md-blue-400);
  --jp-private-notebook-active-color: var(--md-green-400);
}

/*-----------------------------------------------------------------------------
| Notebook
|----------------------------------------------------------------------------*/

/* stylelint-disable selector-max-class */

.jp-NotebookPanel {
  display: block;
  height: 100%;
}

.jp-NotebookPanel.jp-Document {
  min-width: 240px;
  min-height: 120px;
}

.jp-Notebook {
  padding: var(--jp-notebook-padding);
  outline: none;
  overflow: auto;
  background: var(--jp-layout-color0);
}

.jp-Notebook.jp-mod-scrollPastEnd::after {
  display: block;
  content: '';
  min-height: var(--jp-notebook-scroll-padding);
}

.jp-MainAreaWidget-ContainStrict .jp-Notebook * {
  contain: strict;
}

.jp-Notebook .jp-Cell {
  overflow: visible;
}

.jp-Notebook .jp-Cell .jp-InputPrompt {
  cursor: move;
}

/*-----------------------------------------------------------------------------
| Notebook state related styling
|
| The notebook and cells each have states, here are the possibilities:
|
| - Notebook
|   - Command
|   - Edit
| - Cell
|   - None
|   - Active (only one can be active)
|   - Selected (the cells actions are applied to)
|   - Multiselected (when multiple selected, the cursor)
|   - No outputs
|----------------------------------------------------------------------------*/

/* Command or edit modes */

.jp-Notebook .jp-Cell:not(.jp-mod-active) .jp-InputPrompt {
  opacity: var(--jp-cell-prompt-not-active-opacity);
  color: var(--jp-cell-prompt-not-active-font-color);
}

.jp-Notebook .jp-Cell:not(.jp-mod-active) .jp-OutputPrompt {
  opacity: var(--jp-cell-prompt-not-active-opacity);
  color: var(--jp-cell-prompt-not-active-font-color);
}

/* cell is active */
.jp-Notebook .jp-Cell.jp-mod-active .jp-Collapser {
  background: var(--jp-brand-color1);
}

/* cell is dirty */
.jp-Notebook .jp-Cell.jp-mod-dirty .jp-InputPrompt {
  color: var(--jp-warn-color1);
}

.jp-Notebook .jp-Cell.jp-mod-dirty .jp-InputPrompt::before {
  color: var(--jp-warn-color1);
  content: '•';
}

.jp-Notebook .jp-Cell.jp-mod-active.jp-mod-dirty .jp-Collapser {
  background: var(--jp-warn-color1);
}

/* collapser is hovered */
.jp-Notebook .jp-Cell .jp-Collapser:hover {
  box-shadow: var(--jp-elevation-z2);
  background: var(--jp-brand-color1);
  opacity: var(--jp-cell-collapser-not-active-hover-opacity);
}

/* cell is active and collapser is hovered */
.jp-Notebook .jp-Cell.jp-mod-active .jp-Collapser:hover {
  background: var(--jp-brand-color0);
  opacity: 1;
}

/* Command mode */

.jp-Notebook.jp-mod-commandMode .jp-Cell.jp-mod-selected {
  background: var(--jp-notebook-multiselected-color);
}

.jp-Notebook.jp-mod-commandMode
  .jp-Cell.jp-mod-active.jp-mod-selected:not(.jp-mod-multiSelected) {
  background: transparent;
}

/* Edit mode */

.jp-Notebook.jp-mod-editMode .jp-Cell.jp-mod-active .jp-InputArea-editor {
  border: var(--jp-border-width) solid var(--jp-cell-editor-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
  background-color: var(--jp-cell-editor-active-background);
}

/*-----------------------------------------------------------------------------
| Notebook drag and drop
|----------------------------------------------------------------------------*/

.jp-Notebook-cell.jp-mod-dropSource {
  opacity: 0.5;
}

.jp-Notebook-cell.jp-mod-dropTarget,
.jp-Notebook.jp-mod-commandMode
  .jp-Notebook-cell.jp-mod-active.jp-mod-selected.jp-mod-dropTarget {
  border-top-color: var(--jp-private-notebook-selected-color);
  border-top-style: solid;
  border-top-width: 2px;
}

.jp-dragImage {
  display: block;
  flex-direction: row;
  width: var(--jp-private-notebook-dragImage-width);
  height: var(--jp-private-notebook-dragImage-height);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background);
  overflow: visible;
}

.jp-dragImage-singlePrompt {
  box-shadow: 2px 2px 4px 0 rgba(0, 0, 0, 0.12);
}

.jp-dragImage .jp-dragImage-content {
  flex: 1 1 auto;
  z-index: 2;
  font-size: var(--jp-code-font-size);
  font-family: var(--jp-code-font-family);
  line-height: var(--jp-code-line-height);
  padding: var(--jp-code-padding);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background-color);
  color: var(--jp-content-font-color3);
  text-align: left;
  margin: 4px 4px 4px 0;
}

.jp-dragImage .jp-dragImage-prompt {
  flex: 0 0 auto;
  min-width: 36px;
  color: var(--jp-cell-inprompt-font-color);
  padding: var(--jp-code-padding);
  padding-left: 12px;
  font-family: var(--jp-cell-prompt-font-family);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  line-height: 1.9;
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
}

.jp-dragImage-multipleBack {
  z-index: -1;
  position: absolute;
  height: 32px;
  width: 300px;
  top: 8px;
  left: 8px;
  background: var(--jp-layout-color2);
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  box-shadow: 2px 2px 4px 0 rgba(0, 0, 0, 0.12);
}

/*-----------------------------------------------------------------------------
| Cell toolbar
|----------------------------------------------------------------------------*/

.jp-NotebookTools {
  display: block;
  min-width: var(--jp-sidebar-min-width);
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);

  /* This is needed so that all font sizing of children done in ems is
    * relative to this base size */
  font-size: var(--jp-ui-font-size1);
  overflow: auto;
}

.jp-ActiveCellTool {
  padding: 12px 0;
  display: flex;
}

.jp-ActiveCellTool-Content {
  flex: 1 1 auto;
}

.jp-ActiveCellTool .jp-ActiveCellTool-CellContent {
  background: var(--jp-cell-editor-background);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  border-radius: 0;
  min-height: 29px;
}

.jp-ActiveCellTool .jp-InputPrompt {
  min-width: calc(var(--jp-cell-prompt-width) * 0.75);
}

.jp-ActiveCellTool-CellContent > pre {
  padding: 5px 4px;
  margin: 0;
  white-space: normal;
}

.jp-MetadataEditorTool {
  flex-direction: column;
  padding: 12px 0;
}

.jp-RankedPanel > :not(:first-child) {
  margin-top: 12px;
}

.jp-KeySelector select.jp-mod-styled {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  border: var(--jp-border-width) solid var(--jp-border-color1);
}

.jp-KeySelector label,
.jp-MetadataEditorTool label,
.jp-NumberSetter label {
  line-height: 1.4;
}

.jp-NotebookTools .jp-select-wrapper {
  margin-top: 4px;
  margin-bottom: 0;
}

.jp-NumberSetter input {
  width: 100%;
  margin-top: 4px;
}

.jp-NotebookTools .jp-Collapse {
  margin-top: 16px;
}

/*-----------------------------------------------------------------------------
| Presentation Mode (.jp-mod-presentationMode)
|----------------------------------------------------------------------------*/

.jp-mod-presentationMode .jp-Notebook {
  --jp-content-font-size1: var(--jp-content-presentation-font-size1);
  --jp-code-font-size: var(--jp-code-presentation-font-size);
}

.jp-mod-presentationMode .jp-Notebook .jp-Cell .jp-InputPrompt,
.jp-mod-presentationMode .jp-Notebook .jp-Cell .jp-OutputPrompt {
  flex: 0 0 110px;
}

/*-----------------------------------------------------------------------------
| Side-by-side Mode (.jp-mod-sideBySide)
|----------------------------------------------------------------------------*/
.jp-mod-sideBySide.jp-Notebook .jp-Notebook-cell {
  margin-top: 3em;
  margin-bottom: 3em;
  margin-left: 5%;
  margin-right: 5%;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell {
  display: grid;
  grid-template-columns: minmax(0, 1fr) min-content minmax(
      0,
      var(--jp-side-by-side-output-size)
    );
  grid-template-rows: auto minmax(0, 1fr) auto;
  grid-template-areas:
    'header header header'
    'input handle output'
    'footer footer footer';
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell.jp-mod-resizedCell {
  grid-template-columns: minmax(0, 1fr) min-content minmax(
      0,
      var(--jp-side-by-side-resized-cell)
    );
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellHeader {
  grid-area: header;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-Cell-inputWrapper {
  grid-area: input;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-Cell-outputWrapper {
  /* overwrite the default margin (no vertical separation needed in side by side move */
  margin-top: 0;
  grid-area: output;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellFooter {
  grid-area: footer;
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellResizeHandle {
  grid-area: handle;
  user-select: none;
  display: block;
  height: 100%;
  cursor: ew-resize;
  padding: 0 var(--jp-cell-padding);
}

.jp-mod-sideBySide.jp-Notebook .jp-CodeCell .jp-CellResizeHandle::after {
  content: '';
  display: block;
  background: var(--jp-border-color2);
  height: 100%;
  width: 5px;
}

.jp-mod-sideBySide.jp-Notebook
  .jp-CodeCell.jp-mod-resizedCell
  .jp-CellResizeHandle::after {
  background: var(--jp-border-color0);
}

.jp-CellResizeHandle {
  display: none;
}

/*-----------------------------------------------------------------------------
| Placeholder
|----------------------------------------------------------------------------*/

.jp-Cell-Placeholder {
  padding-left: 55px;
}

.jp-Cell-Placeholder-wrapper {
  background: #fff;
  border: 1px solid;
  border-color: #e5e6e9 #dfe0e4 #d0d1d5;
  border-radius: 4px;
  -webkit-border-radius: 4px;
  margin: 10px 15px;
}

.jp-Cell-Placeholder-wrapper-inner {
  padding: 15px;
  position: relative;
}

.jp-Cell-Placeholder-wrapper-body {
  background-repeat: repeat;
  background-size: 50% auto;
}

.jp-Cell-Placeholder-wrapper-body div {
  background: #f6f7f8;
  background-image: -webkit-linear-gradient(
    left,
    #f6f7f8 0%,
    #edeef1 20%,
    #f6f7f8 40%,
    #f6f7f8 100%
  );
  background-repeat: no-repeat;
  background-size: 800px 104px;
  height: 104px;
  position: absolute;
  right: 15px;
  left: 15px;
  top: 15px;
}

div.jp-Cell-Placeholder-h1 {
  top: 20px;
  height: 20px;
  left: 15px;
  width: 150px;
}

div.jp-Cell-Placeholder-h2 {
  left: 15px;
  top: 50px;
  height: 10px;
  width: 100px;
}

div.jp-Cell-Placeholder-content-1,
div.jp-Cell-Placeholder-content-2,
div.jp-Cell-Placeholder-content-3 {
  left: 15px;
  right: 15px;
  height: 10px;
}

div.jp-Cell-Placeholder-content-1 {
  top: 100px;
}

div.jp-Cell-Placeholder-content-2 {
  top: 120px;
}

div.jp-Cell-Placeholder-content-3 {
  top: 140px;
}

</style>
<style type="text/css">
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*
The following CSS variables define the main, public API for styling JupyterLab.
These variables should be used by all plugins wherever possible. In other
words, plugins should not define custom colors, sizes, etc unless absolutely
necessary. This enables users to change the visual theme of JupyterLab
by changing these variables.

Many variables appear in an ordered sequence (0,1,2,3). These sequences
are designed to work well together, so for example, `--jp-border-color1` should
be used with `--jp-layout-color1`. The numbers have the following meanings:

* 0: super-primary, reserved for special emphasis
* 1: primary, most important under normal situations
* 2: secondary, next most important under normal situations
* 3: tertiary, next most important under normal situations

Throughout JupyterLab, we are mostly following principles from Google's
Material Design when selecting colors. We are not, however, following
all of MD as it is not optimized for dense, information rich UIs.
*/

:root {
  /* Elevation
   *
   * We style box-shadows using Material Design's idea of elevation. These particular numbers are taken from here:
   *
   * https://github.com/material-components/material-components-web
   * https://material-components-web.appspot.com/elevation.html
   */

  --jp-shadow-base-lightness: 0;
  --jp-shadow-umbra-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.2
  );
  --jp-shadow-penumbra-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.14
  );
  --jp-shadow-ambient-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.12
  );
  --jp-elevation-z0: none;
  --jp-elevation-z1: 0 2px 1px -1px var(--jp-shadow-umbra-color),
    0 1px 1px 0 var(--jp-shadow-penumbra-color),
    0 1px 3px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z2: 0 3px 1px -2px var(--jp-shadow-umbra-color),
    0 2px 2px 0 var(--jp-shadow-penumbra-color),
    0 1px 5px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z4: 0 2px 4px -1px var(--jp-shadow-umbra-color),
    0 4px 5px 0 var(--jp-shadow-penumbra-color),
    0 1px 10px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z6: 0 3px 5px -1px var(--jp-shadow-umbra-color),
    0 6px 10px 0 var(--jp-shadow-penumbra-color),
    0 1px 18px 0 var(--jp-shadow-ambient-color);
  --jp-elevation-z8: 0 5px 5px -3px var(--jp-shadow-umbra-color),
    0 8px 10px 1px var(--jp-shadow-penumbra-color),
    0 3px 14px 2px var(--jp-shadow-ambient-color);
  --jp-elevation-z12: 0 7px 8px -4px var(--jp-shadow-umbra-color),
    0 12px 17px 2px var(--jp-shadow-penumbra-color),
    0 5px 22px 4px var(--jp-shadow-ambient-color);
  --jp-elevation-z16: 0 8px 10px -5px var(--jp-shadow-umbra-color),
    0 16px 24px 2px var(--jp-shadow-penumbra-color),
    0 6px 30px 5px var(--jp-shadow-ambient-color);
  --jp-elevation-z20: 0 10px 13px -6px var(--jp-shadow-umbra-color),
    0 20px 31px 3px var(--jp-shadow-penumbra-color),
    0 8px 38px 7px var(--jp-shadow-ambient-color);
  --jp-elevation-z24: 0 11px 15px -7px var(--jp-shadow-umbra-color),
    0 24px 38px 3px var(--jp-shadow-penumbra-color),
    0 9px 46px 8px var(--jp-shadow-ambient-color);

  /* Borders
   *
   * The following variables, specify the visual styling of borders in JupyterLab.
   */

  --jp-border-width: 1px;
  --jp-border-color0: var(--md-grey-400);
  --jp-border-color1: var(--md-grey-400);
  --jp-border-color2: var(--md-grey-300);
  --jp-border-color3: var(--md-grey-200);
  --jp-inverse-border-color: var(--md-grey-600);
  --jp-border-radius: 2px;

  /* UI Fonts
   *
   * The UI font CSS variables are used for the typography all of the JupyterLab
   * user interface elements that are not directly user generated content.
   *
   * The font sizing here is done assuming that the body font size of --jp-ui-font-size1
   * is applied to a parent element. When children elements, such as headings, are sized
   * in em all things will be computed relative to that body size.
   */

  --jp-ui-font-scale-factor: 1.2;
  --jp-ui-font-size0: 0.83333em;
  --jp-ui-font-size1: 13px; /* Base font size */
  --jp-ui-font-size2: 1.2em;
  --jp-ui-font-size3: 1.44em;
  --jp-ui-font-family: system-ui, -apple-system, blinkmacsystemfont, 'Segoe UI',
    helvetica, arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji',
    'Segoe UI Symbol';

  /*
   * Use these font colors against the corresponding main layout colors.
   * In a light theme, these go from dark to light.
   */

  /* Defaults use Material Design specification */
  --jp-ui-font-color0: rgba(0, 0, 0, 1);
  --jp-ui-font-color1: rgba(0, 0, 0, 0.87);
  --jp-ui-font-color2: rgba(0, 0, 0, 0.54);
  --jp-ui-font-color3: rgba(0, 0, 0, 0.38);

  /*
   * Use these against the brand/accent/warn/error colors.
   * These will typically go from light to darker, in both a dark and light theme.
   */

  --jp-ui-inverse-font-color0: rgba(255, 255, 255, 1);
  --jp-ui-inverse-font-color1: rgba(255, 255, 255, 1);
  --jp-ui-inverse-font-color2: rgba(255, 255, 255, 0.7);
  --jp-ui-inverse-font-color3: rgba(255, 255, 255, 0.5);

  /* Content Fonts
   *
   * Content font variables are used for typography of user generated content.
   *
   * The font sizing here is done assuming that the body font size of --jp-content-font-size1
   * is applied to a parent element. When children elements, such as headings, are sized
   * in em all things will be computed relative to that body size.
   */

  --jp-content-line-height: 1.6;
  --jp-content-font-scale-factor: 1.2;
  --jp-content-font-size0: 0.83333em;
  --jp-content-font-size1: 14px; /* Base font size */
  --jp-content-font-size2: 1.2em;
  --jp-content-font-size3: 1.44em;
  --jp-content-font-size4: 1.728em;
  --jp-content-font-size5: 2.0736em;

  /* This gives a magnification of about 125% in presentation mode over normal. */
  --jp-content-presentation-font-size1: 17px;
  --jp-content-heading-line-height: 1;
  --jp-content-heading-margin-top: 1.2em;
  --jp-content-heading-margin-bottom: 0.8em;
  --jp-content-heading-font-weight: 500;

  /* Defaults use Material Design specification */
  --jp-content-font-color0: rgba(0, 0, 0, 1);
  --jp-content-font-color1: rgba(0, 0, 0, 0.87);
  --jp-content-font-color2: rgba(0, 0, 0, 0.54);
  --jp-content-font-color3: rgba(0, 0, 0, 0.38);
  --jp-content-link-color: var(--md-blue-900);
  --jp-content-font-family: system-ui, -apple-system, blinkmacsystemfont,
    'Segoe UI', helvetica, arial, sans-serif, 'Apple Color Emoji',
    'Segoe UI Emoji', 'Segoe UI Symbol';

  /*
   * Code Fonts
   *
   * Code font variables are used for typography of code and other monospaces content.
   */

  --jp-code-font-size: 13px;
  --jp-code-line-height: 1.3077; /* 17px for 13px base */
  --jp-code-padding: 5px; /* 5px for 13px base, codemirror highlighting needs integer px value */
  --jp-code-font-family-default: menlo, consolas, 'DejaVu Sans Mono', monospace;
  --jp-code-font-family: var(--jp-code-font-family-default);

  /* This gives a magnification of about 125% in presentation mode over normal. */
  --jp-code-presentation-font-size: 16px;

  /* may need to tweak cursor width if you change font size */
  --jp-code-cursor-width0: 1.4px;
  --jp-code-cursor-width1: 2px;
  --jp-code-cursor-width2: 4px;

  /* Layout
   *
   * The following are the main layout colors use in JupyterLab. In a light
   * theme these would go from light to dark.
   */

  --jp-layout-color0: white;
  --jp-layout-color1: white;
  --jp-layout-color2: var(--md-grey-200);
  --jp-layout-color3: var(--md-grey-400);
  --jp-layout-color4: var(--md-grey-600);

  /* Inverse Layout
   *
   * The following are the inverse layout colors use in JupyterLab. In a light
   * theme these would go from dark to light.
   */

  --jp-inverse-layout-color0: #111;
  --jp-inverse-layout-color1: var(--md-grey-900);
  --jp-inverse-layout-color2: var(--md-grey-800);
  --jp-inverse-layout-color3: var(--md-grey-700);
  --jp-inverse-layout-color4: var(--md-grey-600);

  /* Brand/accent */

  --jp-brand-color0: var(--md-blue-900);
  --jp-brand-color1: var(--md-blue-700);
  --jp-brand-color2: var(--md-blue-300);
  --jp-brand-color3: var(--md-blue-100);
  --jp-brand-color4: var(--md-blue-50);
  --jp-accent-color0: var(--md-green-900);
  --jp-accent-color1: var(--md-green-700);
  --jp-accent-color2: var(--md-green-300);
  --jp-accent-color3: var(--md-green-100);

  /* State colors (warn, error, success, info) */

  --jp-warn-color0: var(--md-orange-900);
  --jp-warn-color1: var(--md-orange-700);
  --jp-warn-color2: var(--md-orange-300);
  --jp-warn-color3: var(--md-orange-100);
  --jp-error-color0: var(--md-red-900);
  --jp-error-color1: var(--md-red-700);
  --jp-error-color2: var(--md-red-300);
  --jp-error-color3: var(--md-red-100);
  --jp-success-color0: var(--md-green-900);
  --jp-success-color1: var(--md-green-700);
  --jp-success-color2: var(--md-green-300);
  --jp-success-color3: var(--md-green-100);
  --jp-info-color0: var(--md-cyan-900);
  --jp-info-color1: var(--md-cyan-700);
  --jp-info-color2: var(--md-cyan-300);
  --jp-info-color3: var(--md-cyan-100);

  /* Cell specific styles */

  --jp-cell-padding: 5px;
  --jp-cell-collapser-width: 8px;
  --jp-cell-collapser-min-height: 20px;
  --jp-cell-collapser-not-active-hover-opacity: 0.6;
  --jp-cell-editor-background: var(--md-grey-100);
  --jp-cell-editor-border-color: var(--md-grey-300);
  --jp-cell-editor-box-shadow: inset 0 0 2px var(--md-blue-300);
  --jp-cell-editor-active-background: var(--jp-layout-color0);
  --jp-cell-editor-active-border-color: var(--jp-brand-color1);
  --jp-cell-prompt-width: 64px;
  --jp-cell-prompt-font-family: var(--jp-code-font-family-default);
  --jp-cell-prompt-letter-spacing: 0;
  --jp-cell-prompt-opacity: 1;
  --jp-cell-prompt-not-active-opacity: 0.5;
  --jp-cell-prompt-not-active-font-color: var(--md-grey-700);

  /* A custom blend of MD grey and blue 600
   * See https://meyerweb.com/eric/tools/color-blend/#546E7A:1E88E5:5:hex */
  --jp-cell-inprompt-font-color: #307fc1;

  /* A custom blend of MD grey and orange 600
   * https://meyerweb.com/eric/tools/color-blend/#546E7A:F4511E:5:hex */
  --jp-cell-outprompt-font-color: #bf5b3d;

  /* Notebook specific styles */

  --jp-notebook-padding: 10px;
  --jp-notebook-select-background: var(--jp-layout-color1);
  --jp-notebook-multiselected-color: var(--md-blue-50);

  /* The scroll padding is calculated to fill enough space at the bottom of the
  notebook to show one single-line cell (with appropriate padding) at the top
  when the notebook is scrolled all the way to the bottom. We also subtract one
  pixel so that no scrollbar appears if we have just one single-line cell in the
  notebook. This padding is to enable a 'scroll past end' feature in a notebook.
  */
  --jp-notebook-scroll-padding: calc(
    100% - var(--jp-code-font-size) * var(--jp-code-line-height) -
      var(--jp-code-padding) - var(--jp-cell-padding) - 1px
  );

  /* Rendermime styles */

  --jp-rendermime-error-background: #fdd;
  --jp-rendermime-table-row-background: var(--md-grey-100);
  --jp-rendermime-table-row-hover-background: var(--md-light-blue-50);

  /* Dialog specific styles */

  --jp-dialog-background: rgba(0, 0, 0, 0.25);

  /* Console specific styles */

  --jp-console-padding: 10px;

  /* Toolbar specific styles */

  --jp-toolbar-border-color: var(--jp-border-color1);
  --jp-toolbar-micro-height: 8px;
  --jp-toolbar-background: var(--jp-layout-color1);
  --jp-toolbar-box-shadow: 0 0 2px 0 rgba(0, 0, 0, 0.24);
  --jp-toolbar-header-margin: 4px 4px 0 4px;
  --jp-toolbar-active-background: var(--md-grey-300);

  /* Statusbar specific styles */

  --jp-statusbar-height: 24px;

  /* Input field styles */

  --jp-input-box-shadow: inset 0 0 2px var(--md-blue-300);
  --jp-input-active-background: var(--jp-layout-color1);
  --jp-input-hover-background: var(--jp-layout-color1);
  --jp-input-background: var(--md-grey-100);
  --jp-input-border-color: var(--jp-inverse-border-color);
  --jp-input-active-border-color: var(--jp-brand-color1);
  --jp-input-active-box-shadow-color: rgba(19, 124, 189, 0.3);

  /* General editor styles */

  --jp-editor-selected-background: #d9d9d9;
  --jp-editor-selected-focused-background: #d7d4f0;
  --jp-editor-cursor-color: var(--jp-ui-font-color0);

  /* Code mirror specific styles */

  --jp-mirror-editor-keyword-color: #008000;
  --jp-mirror-editor-atom-color: #88f;
  --jp-mirror-editor-number-color: #080;
  --jp-mirror-editor-def-color: #00f;
  --jp-mirror-editor-variable-color: var(--md-grey-900);
  --jp-mirror-editor-variable-2-color: rgb(0, 54, 109);
  --jp-mirror-editor-variable-3-color: #085;
  --jp-mirror-editor-punctuation-color: #05a;
  --jp-mirror-editor-property-color: #05a;
  --jp-mirror-editor-operator-color: #a2f;
  --jp-mirror-editor-comment-color: #408080;
  --jp-mirror-editor-string-color: #ba2121;
  --jp-mirror-editor-string-2-color: #708;
  --jp-mirror-editor-meta-color: #a2f;
  --jp-mirror-editor-qualifier-color: #555;
  --jp-mirror-editor-builtin-color: #008000;
  --jp-mirror-editor-bracket-color: #997;
  --jp-mirror-editor-tag-color: #170;
  --jp-mirror-editor-attribute-color: #00c;
  --jp-mirror-editor-header-color: blue;
  --jp-mirror-editor-quote-color: #090;
  --jp-mirror-editor-link-color: #00c;
  --jp-mirror-editor-error-color: #f00;
  --jp-mirror-editor-hr-color: #999;

  /*
    RTC user specific colors.
    These colors are used for the cursor, username in the editor,
    and the icon of the user.
  */

  --jp-collaborator-color1: #ffad8e;
  --jp-collaborator-color2: #dac83d;
  --jp-collaborator-color3: #72dd76;
  --jp-collaborator-color4: #00e4d0;
  --jp-collaborator-color5: #45d4ff;
  --jp-collaborator-color6: #e2b1ff;
  --jp-collaborator-color7: #ff9de6;

  /* Vega extension styles */

  --jp-vega-background: white;

  /* Sidebar-related styles */

  --jp-sidebar-min-width: 250px;

  /* Search-related styles */

  --jp-search-toggle-off-opacity: 0.5;
  --jp-search-toggle-hover-opacity: 0.8;
  --jp-search-toggle-on-opacity: 1;
  --jp-search-selected-match-background-color: rgb(245, 200, 0);
  --jp-search-selected-match-color: black;
  --jp-search-unselected-match-background-color: var(
    --jp-inverse-layout-color0
  );
  --jp-search-unselected-match-color: var(--jp-ui-inverse-font-color0);

  /* Icon colors that work well with light or dark backgrounds */
  --jp-icon-contrast-color0: var(--md-purple-600);
  --jp-icon-contrast-color1: var(--md-green-600);
  --jp-icon-contrast-color2: var(--md-pink-600);
  --jp-icon-contrast-color3: var(--md-blue-600);

  /* Button colors */
  --jp-accept-color-normal: var(--md-blue-700);
  --jp-accept-color-hover: var(--md-blue-800);
  --jp-accept-color-active: var(--md-blue-900);
  --jp-warn-color-normal: var(--md-red-700);
  --jp-warn-color-hover: var(--md-red-800);
  --jp-warn-color-active: var(--md-red-900);
  --jp-reject-color-normal: var(--md-grey-600);
  --jp-reject-color-hover: var(--md-grey-700);
  --jp-reject-color-active: var(--md-grey-800);

  /* File or activity icons and switch semantic variables */
  --jp-jupyter-icon-color: #f37626;
  --jp-notebook-icon-color: #f37626;
  --jp-json-icon-color: var(--md-orange-700);
  --jp-console-icon-background-color: var(--md-blue-700);
  --jp-console-icon-color: white;
  --jp-terminal-icon-background-color: var(--md-grey-800);
  --jp-terminal-icon-color: var(--md-grey-200);
  --jp-text-editor-icon-color: var(--md-grey-700);
  --jp-inspector-icon-color: var(--md-grey-700);
  --jp-switch-color: var(--md-grey-400);
  --jp-switch-true-position-color: var(--md-orange-900);
}
</style>
<style type="text/css">
/* Force rendering true colors when outputing to pdf */
* {
  -webkit-print-color-adjust: exact;
}

/* Misc */
a.anchor-link {
  display: none;
}

/* Input area styling */
.jp-InputArea {
  overflow: hidden;
}

.jp-InputArea-editor {
  overflow: hidden;
}

.cm-editor.cm-s-jupyter .highlight pre {
/* weird, but --jp-code-padding defined to be 5px but 4px horizontal padding is hardcoded for pre.cm-line */
  padding: var(--jp-code-padding) 4px;
  margin: 0;

  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
  color: inherit;

}

.jp-OutputArea-output pre {
  line-height: inherit;
  font-family: inherit;
}

.jp-RenderedText pre {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-code-font-size);
}

/* Hiding the collapser by default */
.jp-Collapser {
  display: none;
}

@page {
    margin: 0.5in; /* Margin for each printed piece of paper */
}

@media print {
  .jp-Cell-inputWrapper,
  .jp-Cell-outputWrapper {
    display: block;
  }
}
</style>
<!-- Load mathjax -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/latest.js?config=TeX-AMS_CHTML-full,Safe"> </script>
<!-- MathJax configuration -->
<script type="text/x-mathjax-config">
    init_mathjax = function() {
        if (window.MathJax) {
        // MathJax loaded
            MathJax.Hub.Config({
                TeX: {
                    equationNumbers: {
                    autoNumber: "AMS",
                    useLabelIds: true
                    }
                },
                tex2jax: {
                    inlineMath: [ ['$','$'], ["\\(","\\)"] ],
                    displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
                    processEscapes: true,
                    processEnvironments: true
                },
                displayAlign: 'center',
                CommonHTML: {
                    linebreaks: {
                    automatic: true
                    }
                }
            });

            MathJax.Hub.Queue(["Typeset", MathJax.Hub]);
        }
    }
    init_mathjax();
    </script>
<!-- End of mathjax configuration --><script type="module">
  document.addEventListener("DOMContentLoaded", async () => {
    const diagrams = document.querySelectorAll(".jp-Mermaid > pre.mermaid");
    // do not load mermaidjs if not needed
    if (!diagrams.length) {
      return;
    }
    const mermaid = (await import("https://cdnjs.cloudflare.com/ajax/libs/mermaid/10.7.0/mermaid.esm.min.mjs")).default;
    const parser = new DOMParser();

    mermaid.initialize({
      maxTextSize: 100000,
      maxEdges: 100000,
      startOnLoad: false,
      fontFamily: window
        .getComputedStyle(document.body)
        .getPropertyValue("--jp-ui-font-family"),
      theme: document.querySelector("body[data-jp-theme-light='true']")
        ? "default"
        : "dark",
    });

    let _nextMermaidId = 0;

    function makeMermaidImage(svg) {
      const img = document.createElement("img");
      const doc = parser.parseFromString(svg, "image/svg+xml");
      const svgEl = doc.querySelector("svg");
      const { maxWidth } = svgEl?.style || {};
      const firstTitle = doc.querySelector("title");
      const firstDesc = doc.querySelector("desc");

      img.setAttribute("src", `data:image/svg+xml,${encodeURIComponent(svg)}`);
      if (maxWidth) {
        img.width = parseInt(maxWidth);
      }
      if (firstTitle) {
        img.setAttribute("alt", firstTitle.textContent);
      }
      if (firstDesc) {
        const caption = document.createElement("figcaption");
        caption.className = "sr-only";
        caption.textContent = firstDesc.textContent;
        return [img, caption];
      }
      return [img];
    }

    async function makeMermaidError(text) {
      let errorMessage = "";
      try {
        await mermaid.parse(text);
      } catch (err) {
        errorMessage = `${err}`;
      }

      const result = document.createElement("details");
      result.className = 'jp-RenderedMermaid-Details';
      const summary = document.createElement("summary");
      summary.className = 'jp-RenderedMermaid-Summary';
      const pre = document.createElement("pre");
      const code = document.createElement("code");
      code.innerText = text;
      pre.appendChild(code);
      summary.appendChild(pre);
      result.appendChild(summary);

      const warning = document.createElement("pre");
      warning.innerText = errorMessage;
      result.appendChild(warning);
      return [result];
    }

    async function renderOneMarmaid(src) {
      const id = `jp-mermaid-${_nextMermaidId++}`;
      const parent = src.parentNode;
      let raw = src.textContent.trim();
      const el = document.createElement("div");
      el.style.visibility = "hidden";
      document.body.appendChild(el);
      let results = null;
      let output = null;
      try {
        let { svg } = await mermaid.render(id, raw, el);
        svg = cleanMermaidSvg(svg);
        results = makeMermaidImage(svg);
        output = document.createElement("figure");
        results.map(output.appendChild, output);
      } catch (err) {
        parent.classList.add("jp-mod-warning");
        results = await makeMermaidError(raw);
        output = results[0];
      } finally {
        el.remove();
      }
      parent.classList.add("jp-RenderedMermaid");
      parent.appendChild(output);
    }


    /**
     * Post-process to ensure mermaid diagrams contain only valid SVG and XHTML.
     */
    function cleanMermaidSvg(svg) {
      return svg.replace(RE_VOID_ELEMENT, replaceVoidElement);
    }


    /**
     * A regular expression for all void elements, which may include attributes and
     * a slash.
     *
     * @see https://developer.mozilla.org/en-US/docs/Glossary/Void_element
     *
     * Of these, only `<br>` is generated by Mermaid in place of `\n`,
     * but _any_ "malformed" tag will break the SVG rendering entirely.
     */
    const RE_VOID_ELEMENT =
      /<\s*(area|base|br|col|embed|hr|img|input|link|meta|param|source|track|wbr)\s*([^>]*?)\s*>/gi;

    /**
     * Ensure a void element is closed with a slash, preserving any attributes.
     */
    function replaceVoidElement(match, tag, rest) {
      rest = rest.trim();
      if (!rest.endsWith('/')) {
        rest = `${rest} /`;
      }
      return `<${tag} ${rest}>`;
    }

    void Promise.all([...diagrams].map(renderOneMarmaid));
  });
</script>
<style>
  .jp-Mermaid:not(.jp-RenderedMermaid) {
    display: none;
  }

  .jp-RenderedMermaid {
    overflow: auto;
    display: flex;
  }

  .jp-RenderedMermaid.jp-mod-warning {
    width: auto;
    padding: 0.5em;
    margin-top: 0.5em;
    border: var(--jp-border-width) solid var(--jp-warn-color2);
    border-radius: var(--jp-border-radius);
    color: var(--jp-ui-font-color1);
    font-size: var(--jp-ui-font-size1);
    white-space: pre-wrap;
    word-wrap: break-word;
  }

  .jp-RenderedMermaid figure {
    margin: 0;
    overflow: auto;
    max-width: 100%;
  }

  .jp-RenderedMermaid img {
    max-width: 100%;
  }

  .jp-RenderedMermaid-Details > pre {
    margin-top: 1em;
  }

  .jp-RenderedMermaid-Summary {
    color: var(--jp-warn-color2);
  }

  .jp-RenderedMermaid:not(.jp-mod-warning) pre {
    display: none;
  }

  .jp-RenderedMermaid-Summary > pre {
    display: inline-block;
    white-space: normal;
  }
</style>
<!-- End of mermaid configuration --></head>
<body class="jp-Notebook" data-jp-theme-light="true" data-jp-theme-name="JupyterLab Light">
<main>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h1 id="TMDB-Movie-Analysis">TMDB Movie Analysis<a class="anchor-link" href="#TMDB-Movie-Analysis">¶</a></h1><h2 id="Table-of-Contents">Table of Contents<a class="anchor-link" href="#Table-of-Contents">¶</a></h2><ul>
<li><a href="#intro">Introduction</a></li>
<li><a href="#wrangling">Data Wrangling</a></li>
<li><a href="#eda">Exploratory Data Analysis</a></li>
<li><a href="#conclusions">Conclusions</a></li>
</ul>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p><a id="intro"></a></p>
<h2 id="Introduction">Introduction<a class="anchor-link" href="#Introduction">¶</a></h2><h3 id="Dataset-Description">Dataset Description<a class="anchor-link" href="#Dataset-Description">¶</a></h3><p>This dataset is from Kaggle: 5000 Movie Dataset and contains information about 10,000 movies collected from The Movie Database (TMDb), including user ratings and revenue.
The primary goal of this project is to practice pandas, Numpy, and Matplotlib data analysis techniques.</p>
<h3 id="Questions-for-Analysis">Questions for Analysis<a class="anchor-link" href="#Questions-for-Analysis">¶</a></h3><ol>
<li>Which genres are most popular from year to year?</li>
<li>How did film budgets change from each decade?</li>
<li>What kinds of properties are associated with movies that have high revenues?</li>
</ol>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p><a id="wrangling"></a></p>
<h2 id="Data-Wrangling">Data Wrangling<a class="anchor-link" href="#Data-Wrangling">¶</a></h2><p>We will prepare the environment, load and assess dataset.</p>
<h3 id="General-Properties">General Properties<a class="anchor-link" href="#General-Properties">¶</a></h3>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [1]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#import necessary libraries</span>

<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [2]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#import and inspect data</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">'tmdb-movies.csv'</span><span class="p">)</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">3</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[2]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>id</th>
<th>imdb_id</th>
<th>popularity</th>
<th>budget</th>
<th>revenue</th>
<th>original_title</th>
<th>cast</th>
<th>homepage</th>
<th>director</th>
<th>tagline</th>
<th>...</th>
<th>overview</th>
<th>runtime</th>
<th>genres</th>
<th>production_companies</th>
<th>release_date</th>
<th>vote_count</th>
<th>vote_average</th>
<th>release_year</th>
<th>budget_adj</th>
<th>revenue_adj</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>135397</td>
<td>tt0369610</td>
<td>32.985763</td>
<td>150000000</td>
<td>1513528810</td>
<td>Jurassic World</td>
<td>Chris Pratt|Bryce Dallas Howard|Irrfan Khan|Vi...</td>
<td>http://www.jurassicworld.com/</td>
<td>Colin Trevorrow</td>
<td>The park is open.</td>
<td>...</td>
<td>Twenty-two years after the events of Jurassic ...</td>
<td>124</td>
<td>Action|Adventure|Science Fiction|Thriller</td>
<td>Universal Studios|Amblin Entertainment|Legenda...</td>
<td>6/9/15</td>
<td>5562</td>
<td>6.5</td>
<td>2015</td>
<td>1.379999e+08</td>
<td>1.392446e+09</td>
</tr>
<tr>
<th>1</th>
<td>76341</td>
<td>tt1392190</td>
<td>28.419936</td>
<td>150000000</td>
<td>378436354</td>
<td>Mad Max: Fury Road</td>
<td>Tom Hardy|Charlize Theron|Hugh Keays-Byrne|Nic...</td>
<td>http://www.madmaxmovie.com/</td>
<td>George Miller</td>
<td>What a Lovely Day.</td>
<td>...</td>
<td>An apocalyptic story set in the furthest reach...</td>
<td>120</td>
<td>Action|Adventure|Science Fiction|Thriller</td>
<td>Village Roadshow Pictures|Kennedy Miller Produ...</td>
<td>5/13/15</td>
<td>6185</td>
<td>7.1</td>
<td>2015</td>
<td>1.379999e+08</td>
<td>3.481613e+08</td>
</tr>
<tr>
<th>2</th>
<td>262500</td>
<td>tt2908446</td>
<td>13.112507</td>
<td>110000000</td>
<td>295238201</td>
<td>Insurgent</td>
<td>Shailene Woodley|Theo James|Kate Winslet|Ansel...</td>
<td>http://www.thedivergentseries.movie/#insurgent</td>
<td>Robert Schwentke</td>
<td>One Choice Can Destroy You</td>
<td>...</td>
<td>Beatrice Prior must confront her inner demons ...</td>
<td>119</td>
<td>Adventure|Science Fiction|Thriller</td>
<td>Summit Entertainment|Mandeville Films|Red Wago...</td>
<td>3/18/15</td>
<td>2480</td>
<td>6.3</td>
<td>2015</td>
<td>1.012000e+08</td>
<td>2.716190e+08</td>
</tr>
</tbody>
</table>
<p>3 rows × 21 columns</p>
</div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [3]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#check how many rows and columns</span>
<span class="n">df</span><span class="o">.</span><span class="n">shape</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[3]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>(10866, 21)</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [4]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Basic information of dataset</span>
<span class="n">df</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>&lt;class 'pandas.core.frame.DataFrame'&gt;
RangeIndex: 10866 entries, 0 to 10865
Data columns (total 21 columns):
 #   Column                Non-Null Count  Dtype  
---  ------                --------------  -----  
 0   id                    10866 non-null  int64  
 1   imdb_id               10856 non-null  object 
 2   popularity            10866 non-null  float64
 3   budget                10866 non-null  int64  
 4   revenue               10866 non-null  int64  
 5   original_title        10866 non-null  object 
 6   cast                  10790 non-null  object 
 7   homepage              2936 non-null   object 
 8   director              10822 non-null  object 
 9   tagline               8042 non-null   object 
 10  keywords              9373 non-null   object 
 11  overview              10862 non-null  object 
 12  runtime               10866 non-null  int64  
 13  genres                10843 non-null  object 
 14  production_companies  9836 non-null   object 
 15  release_date          10866 non-null  object 
 16  vote_count            10866 non-null  int64  
 17  vote_average          10866 non-null  float64
 18  release_year          10866 non-null  int64  
 19  budget_adj            10866 non-null  float64
 20  revenue_adj           10866 non-null  float64
dtypes: float64(4), int64(6), object(11)
memory usage: 1.7+ MB
</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [5]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#how many missing values </span>
<span class="n">df</span><span class="o">.</span><span class="n">isnull</span><span class="p">()</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[5]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>id                         0
imdb_id                   10
popularity                 0
budget                     0
revenue                    0
original_title             0
cast                      76
homepage                7930
director                  44
tagline                 2824
keywords                1493
overview                   4
runtime                    0
genres                    23
production_companies    1030
release_date               0
vote_count                 0
vote_average               0
release_year               0
budget_adj                 0
revenue_adj                0
dtype: int64</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [6]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#how many duplicated rows</span>
<span class="n">df</span><span class="o">.</span><span class="n">duplicated</span><span class="p">()</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[6]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>1</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [7]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># checking descriptive statistics</span>
<span class="n">df</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[7]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>id</th>
<th>popularity</th>
<th>budget</th>
<th>revenue</th>
<th>runtime</th>
<th>vote_count</th>
<th>vote_average</th>
<th>release_year</th>
<th>budget_adj</th>
<th>revenue_adj</th>
</tr>
</thead>
<tbody>
<tr>
<th>count</th>
<td>10866.000000</td>
<td>10866.000000</td>
<td>1.086600e+04</td>
<td>1.086600e+04</td>
<td>10866.000000</td>
<td>10866.000000</td>
<td>10866.000000</td>
<td>10866.000000</td>
<td>1.086600e+04</td>
<td>1.086600e+04</td>
</tr>
<tr>
<th>mean</th>
<td>66064.177434</td>
<td>0.646441</td>
<td>1.462570e+07</td>
<td>3.982332e+07</td>
<td>102.070863</td>
<td>217.389748</td>
<td>5.974922</td>
<td>2001.322658</td>
<td>1.755104e+07</td>
<td>5.136436e+07</td>
</tr>
<tr>
<th>std</th>
<td>92130.136561</td>
<td>1.000185</td>
<td>3.091321e+07</td>
<td>1.170035e+08</td>
<td>31.381405</td>
<td>575.619058</td>
<td>0.935142</td>
<td>12.812941</td>
<td>3.430616e+07</td>
<td>1.446325e+08</td>
</tr>
<tr>
<th>min</th>
<td>5.000000</td>
<td>0.000065</td>
<td>0.000000e+00</td>
<td>0.000000e+00</td>
<td>0.000000</td>
<td>10.000000</td>
<td>1.500000</td>
<td>1960.000000</td>
<td>0.000000e+00</td>
<td>0.000000e+00</td>
</tr>
<tr>
<th>25%</th>
<td>10596.250000</td>
<td>0.207583</td>
<td>0.000000e+00</td>
<td>0.000000e+00</td>
<td>90.000000</td>
<td>17.000000</td>
<td>5.400000</td>
<td>1995.000000</td>
<td>0.000000e+00</td>
<td>0.000000e+00</td>
</tr>
<tr>
<th>50%</th>
<td>20669.000000</td>
<td>0.383856</td>
<td>0.000000e+00</td>
<td>0.000000e+00</td>
<td>99.000000</td>
<td>38.000000</td>
<td>6.000000</td>
<td>2006.000000</td>
<td>0.000000e+00</td>
<td>0.000000e+00</td>
</tr>
<tr>
<th>75%</th>
<td>75610.000000</td>
<td>0.713817</td>
<td>1.500000e+07</td>
<td>2.400000e+07</td>
<td>111.000000</td>
<td>145.750000</td>
<td>6.600000</td>
<td>2011.000000</td>
<td>2.085325e+07</td>
<td>3.369710e+07</td>
</tr>
<tr>
<th>max</th>
<td>417859.000000</td>
<td>32.985763</td>
<td>4.250000e+08</td>
<td>2.781506e+09</td>
<td>900.000000</td>
<td>9767.000000</td>
<td>9.200000</td>
<td>2015.000000</td>
<td>4.250000e+08</td>
<td>2.827124e+09</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [8]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#lets see different genres and their counts</span>
<span class="n">df</span><span class="p">[</span><span class="s1">'genres'</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[8]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>Comedy                                      712
Drama                                       712
Documentary                                 312
Drama|Romance                               289
Comedy|Drama                                280
                                           ... 
Adventure|Animation|Romance                   1
Family|Animation|Drama                        1
Action|Adventure|Animation|Comedy|Family      1
Action|Adventure|Animation|Fantasy            1
Mystery|Science Fiction|Thriller|Drama        1
Name: genres, Length: 2039, dtype: int64</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="Data-Cleaning">Data Cleaning<a class="anchor-link" href="#Data-Cleaning">¶</a></h3>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [9]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#make a copy of the original dataframe</span>
<span class="n">df1</span><span class="o">=</span><span class="n">df</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [10]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#drop duplicated rows</span>
<span class="n">df1</span><span class="o">.</span><span class="n">drop_duplicates</span><span class="p">(</span><span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [11]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#drop unnecessary columns</span>
<span class="n">col</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'id'</span><span class="p">,</span><span class="s1">'imdb_id'</span><span class="p">,</span> <span class="s1">'homepage'</span><span class="p">,</span> <span class="s1">'tagline'</span><span class="p">,</span> <span class="s1">'overview'</span><span class="p">,</span><span class="s1">'original_title'</span><span class="p">,</span><span class="s1">'cast'</span><span class="p">,</span>
       <span class="s1">'keywords'</span><span class="p">,</span><span class="s1">'overview'</span><span class="p">,</span><span class="s1">'production_companies'</span><span class="p">,</span><span class="s1">'release_date'</span><span class="p">,</span><span class="s1">'budget_adj'</span><span class="p">,</span> <span class="s1">'revenue_adj'</span><span class="p">]</span>
<span class="n">df1</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">col</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [12]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#confirm that columns are dropped</span>
<span class="n">df1</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[12]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>popularity</th>
<th>budget</th>
<th>revenue</th>
<th>director</th>
<th>runtime</th>
<th>genres</th>
<th>vote_count</th>
<th>vote_average</th>
<th>release_year</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>32.985763</td>
<td>150000000</td>
<td>1513528810</td>
<td>Colin Trevorrow</td>
<td>124</td>
<td>Action|Adventure|Science Fiction|Thriller</td>
<td>5562</td>
<td>6.5</td>
<td>2015</td>
</tr>
<tr>
<th>1</th>
<td>28.419936</td>
<td>150000000</td>
<td>378436354</td>
<td>George Miller</td>
<td>120</td>
<td>Action|Adventure|Science Fiction|Thriller</td>
<td>6185</td>
<td>7.1</td>
<td>2015</td>
</tr>
<tr>
<th>2</th>
<td>13.112507</td>
<td>110000000</td>
<td>295238201</td>
<td>Robert Schwentke</td>
<td>119</td>
<td>Adventure|Science Fiction|Thriller</td>
<td>2480</td>
<td>6.3</td>
<td>2015</td>
</tr>
<tr>
<th>3</th>
<td>11.173104</td>
<td>200000000</td>
<td>2068178225</td>
<td>J.J. Abrams</td>
<td>136</td>
<td>Action|Adventure|Science Fiction|Fantasy</td>
<td>5292</td>
<td>7.5</td>
<td>2015</td>
</tr>
<tr>
<th>4</th>
<td>9.335014</td>
<td>190000000</td>
<td>1506249360</td>
<td>James Wan</td>
<td>137</td>
<td>Action|Crime|Thriller</td>
<td>2947</td>
<td>7.3</td>
<td>2015</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [13]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#drop null values in genres column</span>
<span class="n">drop</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'genres'</span><span class="p">]</span>
<span class="n">df1</span><span class="o">.</span><span class="n">dropna</span><span class="p">(</span><span class="n">subset</span><span class="o">=</span><span class="n">drop</span><span class="p">,</span><span class="n">how</span><span class="o">=</span><span class="s1">'any'</span><span class="p">,</span><span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [14]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#use str.split to split genres</span>
<span class="n">genre_split</span> <span class="o">=</span> <span class="n">df1</span><span class="p">[</span><span class="s1">'genres'</span><span class="p">]</span><span class="o">.</span><span class="n">str</span><span class="o">.</span><span class="n">split</span><span class="p">(</span><span class="s1">'|'</span><span class="p">)</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">,</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">stack</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">(</span><span class="n">level</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">drop</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [15]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#name the new column </span>
<span class="n">genre_split</span><span class="o">.</span><span class="n">name</span> <span class="o">=</span> <span class="s1">'genre'</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [16]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#use join to combine columns</span>
<span class="n">df1</span> <span class="o">=</span> <span class="n">df1</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s1">'genres'</span><span class="p">],</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">genre_split</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [17]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#check data to see genres are separated</span>
<span class="n">df1</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">3</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[17]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>popularity</th>
<th>budget</th>
<th>revenue</th>
<th>director</th>
<th>runtime</th>
<th>vote_count</th>
<th>vote_average</th>
<th>release_year</th>
<th>genre</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>32.985763</td>
<td>150000000</td>
<td>1513528810</td>
<td>Colin Trevorrow</td>
<td>124</td>
<td>5562</td>
<td>6.5</td>
<td>2015</td>
<td>Action</td>
</tr>
<tr>
<th>0</th>
<td>32.985763</td>
<td>150000000</td>
<td>1513528810</td>
<td>Colin Trevorrow</td>
<td>124</td>
<td>5562</td>
<td>6.5</td>
<td>2015</td>
<td>Adventure</td>
</tr>
<tr>
<th>0</th>
<td>32.985763</td>
<td>150000000</td>
<td>1513528810</td>
<td>Colin Trevorrow</td>
<td>124</td>
<td>5562</td>
<td>6.5</td>
<td>2015</td>
<td>Science Fiction</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [18]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#check for genre categories and their total count</span>
<span class="n">df1</span><span class="p">[</span><span class="s1">'genre'</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[18]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>Drama              4760
Comedy             3793
Thriller           2907
Action             2384
Romance            1712
Horror             1637
Adventure          1471
Crime              1354
Family             1231
Science Fiction    1229
Fantasy             916
Mystery             810
Animation           699
Documentary         520
Music               408
History             334
War                 270
Foreign             188
TV Movie            167
Western             165
Name: genre, dtype: int64</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [19]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#above shows that there are 20 genres </span>
<span class="c1">#use unique function to double check </span>
<span class="n">df1</span><span class="p">[</span><span class="s1">'genre'</span><span class="p">]</span><span class="o">.</span><span class="n">unique</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[19]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>array(['Action', 'Adventure', 'Science Fiction', 'Thriller', 'Fantasy',
       'Crime', 'Western', 'Drama', 'Family', 'Animation', 'Comedy',
       'Mystery', 'Romance', 'War', 'History', 'Music', 'Horror',
       'Documentary', 'TV Movie', 'Foreign'], dtype=object)</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [20]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#create decade column for the df1 </span>
<span class="n">edges</span> <span class="o">=</span> <span class="p">[</span><span class="mi">1959</span><span class="p">,</span> <span class="mi">1970</span><span class="p">,</span> <span class="mi">1980</span><span class="p">,</span> <span class="mi">1990</span><span class="p">,</span> <span class="mi">2000</span><span class="p">,</span> <span class="mi">2010</span><span class="p">,</span> <span class="mi">2016</span><span class="p">]</span>

<span class="c1">#values that fall within the edges will be placed under these names accordingly </span>
<span class="n">names</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'1960'</span><span class="p">,</span> <span class="s1">'1970'</span><span class="p">,</span> <span class="s1">'1980'</span><span class="p">,</span> <span class="s1">'1990'</span><span class="p">,</span> <span class="s1">'2000'</span><span class="p">,</span> <span class="s1">'2010'</span><span class="p">]</span>

<span class="c1">#use cut to categorize bin values into discrete intervals </span>
<span class="n">df1</span><span class="p">[</span><span class="s1">'decade'</span><span class="p">]</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">cut</span><span class="p">(</span><span class="n">df1</span><span class="p">[</span><span class="s1">'release_year'</span><span class="p">],</span> <span class="n">edges</span><span class="p">,</span> <span class="n">labels</span><span class="o">=</span><span class="n">names</span><span class="p">)</span>
<span class="n">df1</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[20]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>popularity</th>
<th>budget</th>
<th>revenue</th>
<th>director</th>
<th>runtime</th>
<th>vote_count</th>
<th>vote_average</th>
<th>release_year</th>
<th>genre</th>
<th>decade</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>32.985763</td>
<td>150000000</td>
<td>1513528810</td>
<td>Colin Trevorrow</td>
<td>124</td>
<td>5562</td>
<td>6.5</td>
<td>2015</td>
<td>Action</td>
<td>2010</td>
</tr>
<tr>
<th>0</th>
<td>32.985763</td>
<td>150000000</td>
<td>1513528810</td>
<td>Colin Trevorrow</td>
<td>124</td>
<td>5562</td>
<td>6.5</td>
<td>2015</td>
<td>Adventure</td>
<td>2010</td>
</tr>
<tr>
<th>0</th>
<td>32.985763</td>
<td>150000000</td>
<td>1513528810</td>
<td>Colin Trevorrow</td>
<td>124</td>
<td>5562</td>
<td>6.5</td>
<td>2015</td>
<td>Science Fiction</td>
<td>2010</td>
</tr>
<tr>
<th>0</th>
<td>32.985763</td>
<td>150000000</td>
<td>1513528810</td>
<td>Colin Trevorrow</td>
<td>124</td>
<td>5562</td>
<td>6.5</td>
<td>2015</td>
<td>Thriller</td>
<td>2010</td>
</tr>
<tr>
<th>1</th>
<td>28.419936</td>
<td>150000000</td>
<td>378436354</td>
<td>George Miller</td>
<td>120</td>
<td>6185</td>
<td>7.1</td>
<td>2015</td>
<td>Action</td>
<td>2010</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [21]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df1</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>&lt;class 'pandas.core.frame.DataFrame'&gt;
Int64Index: 26955 entries, 0 to 10865
Data columns (total 10 columns):
 #   Column        Non-Null Count  Dtype   
---  ------        --------------  -----   
 0   popularity    26955 non-null  float64 
 1   budget        26955 non-null  int64   
 2   revenue       26955 non-null  int64   
 3   director      26864 non-null  object  
 4   runtime       26955 non-null  int64   
 5   vote_count    26955 non-null  int64   
 6   vote_average  26955 non-null  float64 
 7   release_year  26955 non-null  int64   
 8   genre         26955 non-null  object  
 9   decade        26955 non-null  category
dtypes: category(1), float64(2), int64(5), object(2)
memory usage: 2.1+ MB
</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p><a id="eda"></a></p>
<h2 id="Exploratory-Data-Analysis">Exploratory Data Analysis<a class="anchor-link" href="#Exploratory-Data-Analysis">¶</a></h2><h3 id="Question-1:-Which-genres-are-most-popular-from-year-to-year?">Question 1: Which genres are most popular from year to year?<a class="anchor-link" href="#Question-1:-Which-genres-are-most-popular-from-year-to-year?">¶</a></h3>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [22]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#make a copy of the df1/cleaned data frame</span>
<span class="n">genre</span><span class="o">=</span><span class="n">df1</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [23]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#use groupby where first grouping is based on 'release year' and within each release year, group based on 'genre'</span>

<span class="n">genre</span><span class="o">=</span><span class="n">genre</span><span class="o">.</span><span class="n">groupby</span><span class="p">([</span><span class="s1">'release_year'</span><span class="p">,</span> <span class="s1">'genre'</span><span class="p">])</span><span class="o">.</span><span class="n">size</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">(</span><span class="n">name</span><span class="o">=</span><span class="s1">'count'</span><span class="p">)</span>
<span class="n">genre</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">10</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[23]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>release_year</th>
<th>genre</th>
<th>count</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>1960</td>
<td>Action</td>
<td>8</td>
</tr>
<tr>
<th>1</th>
<td>1960</td>
<td>Adventure</td>
<td>5</td>
</tr>
<tr>
<th>2</th>
<td>1960</td>
<td>Comedy</td>
<td>8</td>
</tr>
<tr>
<th>3</th>
<td>1960</td>
<td>Crime</td>
<td>2</td>
</tr>
<tr>
<th>4</th>
<td>1960</td>
<td>Drama</td>
<td>13</td>
</tr>
<tr>
<th>5</th>
<td>1960</td>
<td>Family</td>
<td>3</td>
</tr>
<tr>
<th>6</th>
<td>1960</td>
<td>Fantasy</td>
<td>2</td>
</tr>
<tr>
<th>7</th>
<td>1960</td>
<td>Foreign</td>
<td>1</td>
</tr>
<tr>
<th>8</th>
<td>1960</td>
<td>History</td>
<td>5</td>
</tr>
<tr>
<th>9</th>
<td>1960</td>
<td>Horror</td>
<td>7</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [24]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">genre</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>&lt;class 'pandas.core.frame.DataFrame'&gt;
RangeIndex: 1049 entries, 0 to 1048
Data columns (total 3 columns):
 #   Column        Non-Null Count  Dtype 
---  ------        --------------  ----- 
 0   release_year  1049 non-null   int64 
 1   genre         1049 non-null   object
 2   count         1049 non-null   int64 
dtypes: int64(2), object(1)
memory usage: 24.7+ KB
</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [25]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#group based on 'release year' but not as new index   </span>
<span class="c1">#use apply to accompany the following function; lambda </span>
<span class="c1">#lambda function sorts data frame from the column 'count', minimum being 1 count</span>
<span class="c1">#reset_index(drop=True) is used to drop the current index of the df and replace it with index of increaseing integer</span>
<span class="n">popular</span><span class="o">=</span><span class="n">genre</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="n">by</span><span class="o">=</span><span class="s1">'release_year'</span><span class="p">,</span> <span class="n">as_index</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="n">x</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="s1">'count'</span><span class="p">)</span><span class="o">.</span><span class="n">tail</span><span class="p">(</span><span class="mi">1</span><span class="p">))</span><span class="o">.</span><span class="n">reset_index</span><span class="p">(</span><span class="n">drop</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">popular</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[25]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>release_year</th>
<th>genre</th>
<th>count</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>1960</td>
<td>Drama</td>
<td>13</td>
</tr>
<tr>
<th>1</th>
<td>1961</td>
<td>Drama</td>
<td>16</td>
</tr>
<tr>
<th>2</th>
<td>1962</td>
<td>Drama</td>
<td>21</td>
</tr>
<tr>
<th>3</th>
<td>1963</td>
<td>Drama</td>
<td>13</td>
</tr>
<tr>
<th>4</th>
<td>1964</td>
<td>Drama</td>
<td>20</td>
</tr>
<tr>
<th>5</th>
<td>1965</td>
<td>Drama</td>
<td>20</td>
</tr>
<tr>
<th>6</th>
<td>1966</td>
<td>Comedy</td>
<td>16</td>
</tr>
<tr>
<th>7</th>
<td>1967</td>
<td>Comedy</td>
<td>17</td>
</tr>
<tr>
<th>8</th>
<td>1968</td>
<td>Drama</td>
<td>20</td>
</tr>
<tr>
<th>9</th>
<td>1969</td>
<td>Drama</td>
<td>13</td>
</tr>
<tr>
<th>10</th>
<td>1970</td>
<td>Drama</td>
<td>19</td>
</tr>
<tr>
<th>11</th>
<td>1971</td>
<td>Drama</td>
<td>30</td>
</tr>
<tr>
<th>12</th>
<td>1972</td>
<td>Drama</td>
<td>16</td>
</tr>
<tr>
<th>13</th>
<td>1973</td>
<td>Drama</td>
<td>31</td>
</tr>
<tr>
<th>14</th>
<td>1974</td>
<td>Drama</td>
<td>21</td>
</tr>
<tr>
<th>15</th>
<td>1975</td>
<td>Drama</td>
<td>17</td>
</tr>
<tr>
<th>16</th>
<td>1976</td>
<td>Drama</td>
<td>22</td>
</tr>
<tr>
<th>17</th>
<td>1977</td>
<td>Drama</td>
<td>24</td>
</tr>
<tr>
<th>18</th>
<td>1978</td>
<td>Drama</td>
<td>29</td>
</tr>
<tr>
<th>19</th>
<td>1979</td>
<td>Drama</td>
<td>30</td>
</tr>
<tr>
<th>20</th>
<td>1980</td>
<td>Drama</td>
<td>32</td>
</tr>
<tr>
<th>21</th>
<td>1981</td>
<td>Drama</td>
<td>32</td>
</tr>
<tr>
<th>22</th>
<td>1982</td>
<td>Drama</td>
<td>33</td>
</tr>
<tr>
<th>23</th>
<td>1983</td>
<td>Drama</td>
<td>35</td>
</tr>
<tr>
<th>24</th>
<td>1984</td>
<td>Drama</td>
<td>40</td>
</tr>
<tr>
<th>25</th>
<td>1985</td>
<td>Comedy</td>
<td>51</td>
</tr>
<tr>
<th>26</th>
<td>1986</td>
<td>Drama</td>
<td>51</td>
</tr>
<tr>
<th>27</th>
<td>1987</td>
<td>Comedy</td>
<td>57</td>
</tr>
<tr>
<th>28</th>
<td>1988</td>
<td>Comedy</td>
<td>69</td>
</tr>
<tr>
<th>29</th>
<td>1989</td>
<td>Comedy</td>
<td>63</td>
</tr>
<tr>
<th>30</th>
<td>1990</td>
<td>Drama</td>
<td>60</td>
</tr>
<tr>
<th>31</th>
<td>1991</td>
<td>Drama</td>
<td>63</td>
</tr>
<tr>
<th>32</th>
<td>1992</td>
<td>Drama</td>
<td>65</td>
</tr>
<tr>
<th>33</th>
<td>1993</td>
<td>Drama</td>
<td>90</td>
</tr>
<tr>
<th>34</th>
<td>1994</td>
<td>Comedy</td>
<td>88</td>
</tr>
<tr>
<th>35</th>
<td>1995</td>
<td>Drama</td>
<td>93</td>
</tr>
<tr>
<th>36</th>
<td>1996</td>
<td>Drama</td>
<td>104</td>
</tr>
<tr>
<th>37</th>
<td>1997</td>
<td>Drama</td>
<td>83</td>
</tr>
<tr>
<th>38</th>
<td>1998</td>
<td>Drama</td>
<td>108</td>
</tr>
<tr>
<th>39</th>
<td>1999</td>
<td>Drama</td>
<td>113</td>
</tr>
<tr>
<th>40</th>
<td>2000</td>
<td>Drama</td>
<td>101</td>
</tr>
<tr>
<th>41</th>
<td>2001</td>
<td>Comedy</td>
<td>101</td>
</tr>
<tr>
<th>42</th>
<td>2002</td>
<td>Drama</td>
<td>130</td>
</tr>
<tr>
<th>43</th>
<td>2003</td>
<td>Comedy</td>
<td>111</td>
</tr>
<tr>
<th>44</th>
<td>2004</td>
<td>Drama</td>
<td>141</td>
</tr>
<tr>
<th>45</th>
<td>2005</td>
<td>Drama</td>
<td>182</td>
</tr>
<tr>
<th>46</th>
<td>2006</td>
<td>Drama</td>
<td>197</td>
</tr>
<tr>
<th>47</th>
<td>2007</td>
<td>Drama</td>
<td>197</td>
</tr>
<tr>
<th>48</th>
<td>2008</td>
<td>Drama</td>
<td>233</td>
</tr>
<tr>
<th>49</th>
<td>2009</td>
<td>Drama</td>
<td>224</td>
</tr>
<tr>
<th>50</th>
<td>2010</td>
<td>Drama</td>
<td>210</td>
</tr>
<tr>
<th>51</th>
<td>2011</td>
<td>Drama</td>
<td>214</td>
</tr>
<tr>
<th>52</th>
<td>2012</td>
<td>Drama</td>
<td>232</td>
</tr>
<tr>
<th>53</th>
<td>2013</td>
<td>Drama</td>
<td>253</td>
</tr>
<tr>
<th>54</th>
<td>2014</td>
<td>Drama</td>
<td>284</td>
</tr>
<tr>
<th>55</th>
<td>2015</td>
<td>Drama</td>
<td>260</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [26]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#check for most popular genres</span>
<span class="n">popular</span><span class="p">[</span><span class="s1">'genre'</span><span class="p">]</span><span class="o">.</span><span class="n">unique</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[26]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>array(['Drama', 'Comedy'], dtype=object)</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [27]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#check how many Drama and Comedy bars to expect on graph</span>
<span class="n">popular</span><span class="p">[</span><span class="s1">'genre'</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[27]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>Drama     47
Comedy     9
Name: genre, dtype: int64</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [28]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#set figure size</span>
<span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">30</span><span class="p">,</span><span class="mi">10</span><span class="p">))</span>

<span class="c1">#use seaborn to barplot with bar color respective to popular genre </span>
<span class="n">sns</span><span class="o">.</span><span class="n">barplot</span><span class="p">(</span><span class="n">x</span> <span class="o">=</span> <span class="s1">'release_year'</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="s1">'count'</span><span class="p">,</span> <span class="n">data</span> <span class="o">=</span> <span class="n">popular</span><span class="p">,</span> <span class="n">hue</span><span class="o">=</span><span class="s1">'genre'</span><span class="p">,</span><span class="n">dodge</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>

<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">"Which genres are most popular from year to year?"</span><span class="p">,</span> <span class="n">fontsize</span> <span class="o">=</span> <span class="mi">20</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s2">"Year"</span><span class="p">,</span> <span class="n">fontsize</span> <span class="o">=</span> <span class="mi">20</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s2">"Movie Production Count"</span><span class="p">,</span> <span class="n">fontsize</span> <span class="o">=</span> <span class="mi">20</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">(</span><span class="n">prop</span><span class="o">=</span><span class="p">{</span><span class="s2">"size"</span><span class="p">:</span><span class="mi">20</span><span class="p">})</span>

<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAACW4AAANtCAYAAAAKanBNAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjYuMywgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy/P9b71AAAACXBIWXMAAA9hAAAPYQGoP6dpAADYkElEQVR4nOzdd5RV5f0+7HvoHSkCoqhYiCJW7A01togmlmgSC9hi9IsxGjXGEmsSE02zt6hYorEmir0DdikWsCtoFLGBgoi02e8fvnN+jMwMZcYZgetai7XOnP2Uz977nH1OPHeeXVYURREAAAAAAAAAAADqTaOGLgAAAAAAAAAAAGBpI7gFAAAAAAAAAABQzwS3AAAAAAAAAAAA6pngFgAAAAAAAAAAQD0T3AIAAAAAAAAAAKhnglsAAAAAAAAAAAD1THALAAAAAAAAAACgngluAQAAAAAAAAAA1DPBLQAAAAAAAAAAgHomuAUAAECdKSsrS1lZWU4//fRFHuOxxx4rjfPYY4/VWW1JMnjw4NLY48ePr9OxAZYkp59+eul6ubh5991384tf/CKrrrpqWrRoUdqP//73vw1dGgAAAEAlglsAAABLoDlz5qRdu3YpKyvLBhtsUGPboijSqVOn0g/bV111VY3tr7nmmlLbSy65pC7LBoBaeffdd9O3b99cfvnlefvttzNjxoyGLglYSDNmzMiNN96YvffeOz179kzLli3TqlWr9O7dO8cff3wmTpzY0CUCAADUGcEtAACAJVDjxo2z+eabJ0leeOGFTJkypdq2Y8eOzaRJk0p/Dx8+vMax596+9dZb17JSgIVXF6v7sWT6/e9/n08++SRNmjTJn//85zz11FN56aWX8tJLL+X73/9+Q5fHd9j48eNL15bBgwc3dDlLrRdffDGrrbZa9t1339x6660ZP358vvrqq0yfPj2vvPJK/vKXv6RPnz557rnnGrpUAACAOtGkoQsAAADg27H11lvn/vvvT3l5eZ588snsvPPOVbarCGI1btw4c+bMWeDgVufOndO7d++6LTrJNttsk6Io6nxcAJZ8Dz30UJJk9913z29+85sGrgZYWG+//Xbee++9dOzYMQMGDMj222+frl275t13380ll1yShx56KJ9++mn23HPPvP7662nZsmVDlwwAAFArVtwCAABYQs29GtawYcOqbVexbe+9906SvPXWW5kwYUKVbT/66KO8/vrrSZItt9wyZWVldVUuANTa+++/nyTp1atXA1cCLIrmzZvnlFNOyTvvvJO///3v6d+/fzbccMPsueeeeeCBB7LbbrslSd57773ce++9DVwtAABA7QluAQAALKE22mijtGjRIknNtz+s2PbjH/84q666ao3t3SYRgO+ymTNnJkmaNm3awJUAi+IHP/hBzjrrrLRp02aebWVlZRk4cGDp7zfeeKM+SwMAAPhWCG4BAAAsoZo3b56NN944SfLcc89lxowZ87QZN25caXWSLbfcMltuuWWSugtuPffcc/nZz36WFVZYIc2bN8/yyy+fAw44IK+88kq1fR577LGUlZWlrKwsjz32WI3j33PPPdl///2zyiqrpHXr1mnRokV69uyZvfbaK4MHD86XX35ZY//y8vJcfvnl2XzzzdOhQ4e0bt0666yzTv7whz/Mt++Cevzxx7PXXnulW7duadGiRVZZZZUcfvjhefPNN5N8fWvIsrKybLPNNjWO8+abb+aYY47J2muvnfbt26dly5ZZZZVVcuCBB2bEiBHV9qvqeN588835/ve/n2WXXTYtW7bM9773vfzmN7/JpEmTqh3nwAMPTFlZWVZeeeUkyQcffJATTjgha621Vtq2bVvl+ZozZ06uueaa7LrrrunevXuaN2+eTp06Zcstt8zf/va3TJ8+vcZ9HjlyZA455JD06tWrdH579OiRvn37ZtCgQbnzzjsX+baab7/9dv76179mt912y8orr5yWLVumZcuWWWmllfKTn/wk9913X439Bw8eXDqu48ePz4wZM/KPf/wjm266aTp37pyysrKcfvrp8/R79NFHM3DgwKyyyipp1apV2rVrl7XXXjvHH398tSvdLahvnqOJEyfmuOOOS69evdKqVassv/zy2WeffTJ27NhK/caPH5+jjjoqvXr1SsuWLdO1a9fst99+eeutt+Y758yZM3PxxRdn2223zbLLLptmzZqlW7du2WWXXXL99denvLy8xv6vv/56fvnLX6ZPnz5p27ZtmjVrlu7du2e99dbLwQcfnJtuuqnStWvllVeutNLfGWecUToPFf8OPPDABT9oqfpc/uUvf8kGG2yQ9u3bp127dtlkk01y8cUXZ86cOfMd7+OPP84pp5yS9ddfP8sss0xatGiRlVdeOQcccEAef/zxGvtW7F/FPlRcQ3v06FF6/R900EF59dVXF3h/qjN+/PhSu8GDB893v75p5syZGTJkSI488shstNFG6dChQ5o2bZpOnTplk002yemnn55PPvlkofZ35MiROfDAA9OzZ880b958gVd1nHufK3zztTH36+Kb19033ngjRx55ZFZfffW0atWqymM3fvz4HHPMMaVrXqtWrbL66qvnF7/4RV566aUa66uooeKa8Oijj2b33XdP9+7d07Jly6y55po566yzMm3atEr97rnnnuyyyy6ldr17987ZZ59dCqctrPPPP79Uy9NPPz3f9nvttVfKysrSsWPHfPXVV1W2+e9//5u99947K664Ylq0aJFlllkmG264Yc4444xMnjy5xvGffvrpnHLKKdlmm23SrVu3NGvWLO3atUvv3r1zxBFH5OWXX66x/6J8LlWnrKwsPXv2LP190EEHzXNtqeqaXl5enuuvvz677LJLaR+WXXbZbLvttrn44osX+Vx98sknpffA4YcfPt/2Q4YMKdV58803V9lmUb9HJF8f24svvjg//vGPs/rqq6d169al73U/+tGPctNNN9V4vf/md5Hy8vJcddVV2XbbbdO1a9c0atRoga/dU6dOLT3u1KnTAvUBAAD4TisAAABYYp1yyilFkiJJMXTo0Hm2Dx48uEhSrL766kVRFMUVV1xRJCnWXnvtKsfbYIMNiiRFu3btitmzZ8+zvWKu0047rbjooouKJk2alJ6b+1+rVq2qrKcoiuLRRx8ttXv00UerbPPJJ58U3//+96sce+5/V199daV+V199dWnb2LFjaxxj4403Lr744osaju78/elPfyrKysqqHL9t27bF/fffX/Tr169IUvTr16/acc4999yiadOm1dZaVlZW/O53v6uy79zH8+GHHy7233//asdZbbXVig8++KDKcQYOHFgkKVZaaaXiqaeeKjp37jxP/7nP1zvvvFOsu+66NZ6f1VZbrXjttdeqnO9vf/tb0ahRo/me46lTpy7w+ajw9ttvz3fcJMX+++9fzJo1q8ox5n4tPffcc8V66603T//TTjut1H769OnFT3/60xrna926dXHnnXcu9P5UmPscPf/880W3bt2qnWf48OFFURTFww8/XLRv377Kdh06dCjGjBlT7Xzjxo0r1lhjjRr3acsttyw+/fTTKvvffPPNRbNmzeZ7Hl566aVSn5VWWmm+7QcOHLhQx23uczlq1Kiib9++1Y699dZb1/iau//++4t27drVWN+gQYOKOXPmVNm/Yv8GDhxYXHnlldVeQ5s3b17cfPPN892fcePGVVvruHHjSu2+ea0siqI47bTTSturUvF6q+lfp06discff7zaGube30suuaTK/V0Qc+/zgrwu5r7u/ve//y1at249T/u5j90111xTNG/evNqxGzduXPzxj3+str65rwlnn312tZ8Lm2++efHFF18U5eXlxVFHHVXtfDvvvHOVn8Hz8+mnn5b24xe/+EWNbT/++OPS586gQYPm2T5p0qRiu+22q/GYd+nSpXjqqaeqHH9Bzlnjxo2Liy66qNoaF/ZzqSbzq6Xi/M3t008/LbbYYosa+6y55prF+PHjF6iGb9p7772LJMUyyyxTTJ8+vca2e+yxR5Gk6NixY/HVV1/Ns7023yNmz569QJ/HO+ywQ7XXx7m/i9x7773F9ttvX+N7tDpffvllsdZaaxVJihYtWhQTJ06cbx8AAIDvOsEtAACAJdgDDzxQ+kHs97///TzbDznkkCJJcdBBBxVFURSvvPJK6Qe8SZMmVWo7ZcqUonHjxqUfjatSMdemm25aNGrUqFh33XWLq666qnjuueeKYcOGFcccc0zpx78VV1yxmDFjxjxjzC+4NW3atGLttdcutenbt29x2WWXFU888UQxYsSI4j//+U9xzDHHFN27d68xuLX55psXjRo1KgYOHFjcfffdxciRI4v//Oc/xWabbVZq89vf/nYBj/S8brrpptI4HTt2LP785z8XTz75ZPHkk08Wf/7zn4sOHToUHTp0KHr16lUKEFTlnHPOKY2zzjrrFJdccknx0EMPFSNGjCj+9a9/Var3vPPOq/F4br755kWSYvfddy9uv/32YuTIkcU999xT9O/fv9Tmpz/9aZV1VPxA3qlTp6J79+5FmzZtipNPPrl47LHHimeffba48sori1dffbUoiq+DdT169CiSrwMmRx55ZHHLLbcUzz33XPHoo48WJ554YtGqVasiSbHKKqsUn332WaW5XnjhhdLrpGfPnsVf//rX4uGHHy5Gjx5dDBs2rLjiiiuKfffdt2jduvUiBbfeeOONolmzZsVuu+1WnH/++cVDDz1UjBo1qnjooYeKiy++uPSjcJLi1FNPrXKMuV9L66yzTlFWVlYMGDCg0mvpnnvuKYqiKMrLyysd491226247rrriieeeKJ46qmnivPOO69YccUViyRFs2bNiueee26h96ko/t85WnbZZYuePXsWHTt2LP74xz8WTzzxRPH0008Xp59+eikotfLKKxdvvPFG0bZt22KFFVYozjvvvOLpp58uHn/88eKYY44pBUs22WSTKueaOnVqscoqq5T2affddy/uvPPOYsSIEcUtt9xSCsZUvO6+GTKZOHFiKSzTpUuX4swzzyweeOCBYtSoUcUTTzxRXHPNNcXBBx9cdOzYsVJw67XXXiteeuml0thHHHFE8dJLL1X699577y3UcZv7XG600UZFkuInP/lJcc899xQjRowobrjhhtLzFftaldGjR5eOb9OmTYtjjjmmePTRR4tnn322uOyyy4qePXuWxvjNb35T5RgVQaZ11123aNq0adG9e/figgsuKJ555pli6NChxQknnFAK3jRt2rTK10p9Bbf222+/YpVVVimOPfbY4qabbiqeeuqp4rnnnituvfXW4vDDDy8di2WXXbb48MMPa9zf3r17F40bNy5WXnnl4sILLyy9Fs8+++xq65/b5MmTS+e/utfG3K+Litdnz549izZt2hTLLrts8ac//an0XrnggguKjz/+uCiKorjrrrtK74c2bdoUp512WjF8+PDiqaeeKv76179WCgtdfPHFVdZXsX3jjTcukhSbbbZZccMNNxQjRowo7rvvvuIHP/hBqc3JJ59c/PWvfy2SFD/4wQ+K2267rRg5cmRxxx13FJtuummp3SWXXLJAx+abfvaznxVJivbt2xdffvllte3+8Y9/lOYaOXJkpW1fffVVKcjduHHj4oADDihuvPHG4umnny6GDx9e/OEPfyg6depUJF8HQKsKLl1xxRVFhw4digMPPLC46qqriuHDhxejRo0q7rrrruLMM88sHdeysrLi4YcfrrLGhflcmp+XXnqpuP/++yt9Z/rmtWXu1/Hs2bMrff7269evuOWWW4oRI0YUd955Z7H77ruXtq266qqL9Fk1dz033HBDte0++uijUijrl7/85Tzba/s9YtasWUWjRo2K7bbbrjj33HOL++67rxg5cmTx2GOPFVdddVWl/gMGDKiyxrm/i6yzzjpFkuKHP/xhpe8i//73v2s8Hl9++WWx0047lca54IIL5nMEAQAAFg+CWwAAAEuwqVOnllYw2WmnnebZXhEauuqqq0rPVfxYOmTIkEpt77vvvtKPZdWtLDL3ygm77LJLlcGs3//+96U2t99++zzb5xfcOuaYY0rbBw0aVJSXl1dZy4wZM+ZZieGbK3xcd9118/T76quvij59+pR+DK5uxaWafPXVV0XXrl2LJEXnzp2LN954Y542r732WtGxY8dKP/p+09ixY0s/xp522mlV7uucOXNKq2i1adNmnsDd3Mez4sfobyovLy923HHHIknRpEmT4qOPPpqnzdyr67Rp06Z4/vnnq93/fffdt0i+XgXl7bffrrLNqFGjSsGdk046qdK23/3ud0Xy9cpQNa2m8dlnn1W7clFNvvjii2LChAnVbi8vLy8OPPDAUg3fDJYVxbyvpX/+85/Vjnf55ZeXgjb33ntvlW0mTZpUCoxtscUWC71PRVH5HHXu3Ll4880352lz4YUXltosu+yyxeqrr17l+T7++ONL7UaNGjXP9uOOO660/ZRTTplne3l5ebHffvtVG2i58sorS9vmDmZ905dffllluKSi7zdXwFkU3zyXVV3fZs2aVSkwcPfdd8/TpiLc1bhx4+L++++fZ/ukSZOK3r17F0mKRo0aVbma2dwriq200kpVroD3yCOPlK7rG220UY37820Gt958881qr79FURQvvvhi0aZNm2pfI0VReX/XXnvtYvLkydWOt6AW5LUxd7Cwe/fuxTvvvFNlu5kzZxbdu3cvXfdGjx49T5vx48cXyy23XJF8vZpkReCrqpqSFHvttdc8QcbZs2eXQllt27YtWrRoURx99NHzjDNt2rTSMVtnnXVqPhDVePjhh0u1/Otf/6q2XcWKieuuu+4820466aQi+XolqBEjRlTZf+7jsu+++86z/b333iumTZtW7fyfffZZKeCz5ZZbVtlmYT6XFsT83hNzm/taOmDAgCrfCxXHKak+rFmTOXPmlM73DjvsUG27v/3tb6V5vvkarYvvEeXl5VV+j5nbqaeeWgravf766/Ns/+Z3kequCdWZNm1ase2225b6f/N7AwAAwOJMcAsAAGAJVxEmaNu2baUfiz/88MPSD2Bz/8j2ox/9qMofGU8++eRS++pufVWxvUWLFtWusDJlypTSSizHHHPMPNtrCm5Nnjy5tFJT3759F/pWUXMHGvbcc89q21166aWldi+88MJCzVEURfHvf/+71P/CCy+stt15551XY3Dr4IMPLpIUG264YY0BicmTJ5dW4bn88ssrbZv7ePbt27faceYO5t1xxx3zbJ/7B/Izzzyz2lrGjRtXWpntm+G/b/rNb35TCk7M7ec//3mRpFh//fVr7P9t+vTTT0v7ceutt86zfe7X0nbbbVftOOXl5cWqq65aJCmOPfbYGue85557qnxPLqi5z1F1q/F8+eWXRYsWLUrtqguSzX07yW+uwPLVV18VyyyzTJGkWGuttap9H37++eelVXd69+5dadsf/vCHIvl6NZ5F8W0Ft9ZZZ51q3yP/+9//SgGI/v37V9r2zDPPlMY4/PDDq53r8ccfL7X7v//7v3m2zx1kqup1V+GII44otfvmqlv1FdxaEEcffXSRpOjTp0+V2+fe32HDhi3yPHNb2ODWtddeW227uVdO/NOf/lRtu+uvv77U7pxzzqm2platWlV769Crrrqq1K5Hjx7FzJkzq2xXEZBJUmWodH7mviZtv/32VbYZOXJkte//qVOnlm6vOr8Vjy6++OIi+Tq0uii3Hv7vf/9bquOTTz6ZZ/uCfi4tqIUJbq255ppF8nUAdsqUKVW2mTVrVul2sh06dKjyFobzc8YZZxTJ12HPd999t8o2FauQVvWZWRffIxbE7NmzS8H/v/zlL/Nsn/u7SK9evRbq+9s3g7N1cd0HAAD4LmkUAAAAlmhbb711kmTq1Kl5/vnnS88PGzYsSdK1a9esvvrqpee33HLLStsrDB8+PEnSokWLbLTRRjXOucMOO6RLly5Vbmvbtm1pvrfffnsh9iR55JFH8uWXXyZJjjrqqDRu3Hih+s9tv/32q3Zb3759S48XtsYkeeihh5IkjRo1qnGe/fffP2VlZdVuHzJkSJJkr732qrHdMsssk7XXXjtJ8tRTT1Xbbt999612nIXZ55r26e67786cOXPSqlWr/OAHP6hxnIrX5oQJE/Luu++Wnl9uueWSJC+//HKeffbZGseoC7Nmzcp7772XV155JWPGjMmYMWMyYcKEdOrUKUnywgsv1Ni/puPx8ssv56233kqS/PjHP65xnIrjkdR8HuenrKws++yzT5XbWrZsWXr/dejQITvttFOV7Xr27Jm2bdsmmff1MHLkyHz22WdJkgMPPLDa92G7du1Kdbz88sv54IMPStsqzvHkyZNzxx13LOCeffsGDhxY7XtkhRVWyI477pgkeeyxxzJnzpzStor3fJIccsgh1Y6/xRZbZM0115ynzzd16NAhP/rRj6rdfvDBB1c5d0OaPHly3nrrrYwdO7b0PlpmmWWSfH3+Z82aVW3fHj16ZKuttqqnSv+fZs2aZe+99652e8WxLSsrq3TMv2nvvfdO+/btK/Wpyg477JCOHTtWuW3dddctPd5zzz3TtGnT+bYbN25ctXNVZ+59eeSRRypdeytcffXVSb4+Pt+8vg0dOjSff/55kgW/ps2aNSsjR46sse20adMyfvz4Sq+fuY9Bba7DdW3ChAl55ZVXkiT77LNP6Vr5TU2aNMlBBx2U5Ov3x6hRoxZ6roMPPjiNGjVKeXl5rrnmmnm2jxw5Mi+99FKp7TfV9feIJCkvL8+ECRPy2muvlc7VK6+8khVWWCHJ/M/VT37yk4X6/nb++efn/vvvT5KceOKJOf300xe4LwAAwOJAcAsAAGAJN/eP4RXhq7kfVwS1vtl+5MiRmT59epJk5syZpQDNJptskmbNmtU45xprrFHj9oofrqdOnbogu1AyevToeepcVDXVOPcP6wtbY5KMGTMmSbLKKquUggvVzbPKKqtUue2dd97Jxx9/nOTrHyrLyspq/DdixIgkycSJE6udry72uU2bNtXWnKRUx5dffpkmTZrUWPOuu+5a6jd33T/72c/StGnTzJgxI1tssUV22223XHrppRkzZkyKoqh27oUxa9asXHTRRdl0003Tpk2b9OjRI717987aa69d+vfRRx8lST755JMax1pnnXWq3VZxPJJks802q/F4tGnTptS2pvM4P507d642HJKk9JpcbbXV5vtDfjLv66Hi9Z18fT2oydzb5+73wx/+sDT+Hnvske222y5///vfM3LkyEqBqPo2v1DqxhtvnOTrkMncgbaKfWvWrFnWW2+9GseoOCZvvPFGZs6cWWWb9ddfP02aNKl2jPXWW690Ha4IbTSEl156KQcffHCWW265dOzYMauttlr69OlTeg9VBCzKy8szefLkasep6T30bVp99dXTokWLardXnNeePXtm2WWXrbZds2bNsv7661fqU5VevXpVu23uz4oFbbcon0/J/wtcVhUGmjFjRm644YYkyY9+9KNSgLXC3Ne05ZZbrsZrWp8+fUptq7qmffLJJznppJPyve99L23btk3Pnj0rvX769+9fqW115ve5VNfq4hq4oFZYYYVSwHbw4MHzbK8I2TVv3nye8Fpdfo8oiiLXX399tt1227Rp0ybLL7981lhjjUqfmRX/54DafGZWpWIfV1111Zx11lkL1RcAAGBxILgFAACwhNtqq61K4YwFCW5tsMEGadWqVWbNmpWnn346SfLcc8/lq6++SlJ5VaDqtGrVqsbtjRp9/T9HFzagMfePgRUr9iyqmmqsqC9Z+BqTlAIKNf3QX6G6NhWhoYVVsSJZVepin2sKoiV1U/caa6yRG2+8MR06dMjs2bNz11135Ygjjsjaa6+dLl265IADDqj0Wl5YkyZNymabbZYjjzwyzzzzTLXhmQoVAcbqdOjQodpt38Z5nJ8Fff8t6vt00qRJpcfVraxXoVu3blX269SpU+68884sv/zyKYoijz76aH79619nww03TMeOHbPnnnvmrrvuqnHsb8P89qdr166lx3PvT8Xjjh071hi4Sv7fMSmKotow0/zqaNKkSSmcN3cd9enKK6/MBhtskKuvvnqBgoY1vY9qeg99m+Y3b8Wxnd/5SP7fea3pfCzoNfjb/HxKku7du2eXXXZJ8nUYaO5A7B133FHah6pWcKqra9rIkSOzxhpr5Oyzz87rr78+31BuTa+f+X0u1bW6uAYujEMPPTRJ8tZbb1VaDXXukN3uu+8+z+u5rs7VV199lf79++eAAw7IY489Nt/PxNp8ZlalYtXKjTfeuFYrrQIAAHxX1fxfkgAAAFjsdezYMWuttVbGjBlTCrtMmTKldCubbwa3mjZtmo033jiPPfZYhg0blm233bZSSGZBglvU3tw/yJ966qk13s5rbq1bt/62SkqS+f5oWlF3586d8+ijjy7wuD179qz091577ZXtt98+N910U+6///4MHz48H3/8cT755JNcf/31uf766zNw4MBcddVVlYIMC+JXv/pV6bZdu+++ew4++OCss8466dKlS1q0aFEKOq644or53//+N99AQU3HZO7zOGTIkKy88soLVOOCBEW+C2pasWt+ttpqq7z55pu57bbbcs8992TYsGF57733MmXKlPznP//Jf/7zn+y00065/fbb5xsyqyu12Z+66F/X43xbXn311Rx++OGZPXt2unTpkuOPPz7bbbddVl555bRt27Z0i7urrrqqdOvImt5HDRXGWNB5v+vnY1EceuihGTJkSN5+++0MGzYs/fr1S/L/Vjea+9agc5v7mjZq1Khqb+n4TRW30Uu+XsVzn332yaeffpqmTZvml7/8ZX70ox+lV69e6dChQ5o3b57k69u0rrrqqkm+m6+fpH5eG7vttlu6du2aDz/8MFdffXXpe9h///vfUvizqpBdXX2P+MMf/pB77703SdKvX78MGjQoG2ywQbp165aWLVuWPoO33nrrDB8+vFafmVWpCILNb7VXAACAxZXgFgAAwFJg6623zpgxY/Lxxx/n1Vdfzbhx41JeXp42bdqUbu80ty233DKPPfZYKbBVscJD06ZNs9lmm9Vr7XPr3Llz6fEHH3wwT9jnu6JiNYmKWxTVpLo2c9+eqmnTppVuOfVdVlH31KlTs+aaa9bqB/X27dvnsMMOy2GHHZYkeeWVV3LHHXfkggsuyIQJE3LNNddk/fXXz69+9asFHnPKlCm56aabkiT77bdfrr/++mrb1nRrtwU193lcZpllFpvzWJO5b8P44Ycf1nhbt7lXYqrq9o0tWrTIfvvtV7rF17hx43L33XfnggsuyOuvv577778/J598cv7+97/X4R5Ub3778+GHH5Yez70/FY8//fTTzJ49u8ZVtyqOSVlZWbUrz8w9T1Vmz55daZWvuc0dZCwvL692jGnTptU4R00GDx6c2bNnp3Hjxhk6dGi1t2FtqNXA6krFsZ3f+Uj+33mt6Tal3yX9+/fPcsstlw8++CBXX311+vXrl/fffz8PPPBAkmTgwIFVhmLnvqYtu+yylQJZC+qRRx4p3Wr04osvLq0o9U3f1dfPN6+BNZnfNXBBNG3aNAMGDMi5556bW265JRdccEHatGlTCtmtuOKK2X777efpVxffI4qiyD//+c8kX4dtH3nkkWrD0t/V8wUAAPBd51aJAAAAS4Gtttqq9Hj48OGlQNamm25aZbCmYhWup59+OjNmzMiTTz6Z5OvbKH7bKzrVZIMNNig9nvt2Qd81a621VpKvVwupKfwzadKk0o/X37TKKqukffv2SZInnnii7ov8llQEAWfMmJERI0bU6dhrrrlmfvvb3+bpp58uvQ5vvvnmhRrjjTfeyKxZs5IkP/nJT6pt9+qrr+aLL75Y9GL/f3MHIxen81iTuX/8f+aZZ2ps++yzz1bZrzo9e/bMkUcemeeee64UCFnYc1wbzz333AJtb9WqVVZZZZXS8xX7NnPmzDz//PM1jlFxTFZfffVqV5B5/vnnM3v27GrHeOGFF0q3+PzmcW3btm3pcU3Xn9dff73GOmsyduzYJMm6665bbWgrSZ1fA+pbxbEdN25cjUHcWbNmZfTo0ZX6fNc1btw4Bx54YJLk1ltvzRdffJFrrrkm5eXlKSsry0EHHVRlv7q4plW8fpKar8P1/fpZ0NWzvs1rYHUqwm3Tpk3LLbfckvfeey8PPvhgkupDdnXxPWLSpEml8Nnee+9dbWjriy++yGuvvbZIc8zP9OnTM3369FxxxRXfyvgAAAANTXALAABgKTD37Q2HDRtWCj198zaJFTbbbLM0btw406ZNy+DBg/P555/PM05D2HbbbUuBnQsuuKDSbYC+S77//e8n+Xq1mxtuuKHadtdff321txRq3LhxdtlllyTJAw88kFdeeaXuC/0W7LbbbqUfv//xj398K3P06NGjtCrSJ598slB95w7D1LTi0KWXXrpoxX3DBhtsUAogXX755fnqq6/qZNyG1Ldv3yyzzDJJUgp6VGXq1Kml0FXv3r2z3HLLLfAc7dq1y0YbbZSk6nPcokWLJF8HBOvSddddV+17cu7ViLbZZptKode5V7u56qqrqh3/qaeeyssvvzxPn2+aNGlShgwZUu32uef45jhzr0RYU/DlxhtvrHbb/FS8j2p6D33wwQe58847F3mO74KKY1sURWl1o6rceuutpc/Jms7rd80hhxySsrKyTJs2LTfddFMGDx6c5OvP+opbFH7T9ttvX7p16fnnnz/f2+JVZUGuw+Xl5fUe1Km4riQ1X1u6d++eNddcM8nXwdLqQr5z5swpHdMOHTpUCp8vrF69epVC+FdfffUChezq4nvEgn5m/vOf/6wxbFobLVq0SIsWLRb4tpwAAACLG8EtAACApUD37t1LP8I++uijpR/z516Ja27t2rXL2muvnSQ555xzSs83dHBrmWWWyS9+8YskyciRI3P00UdX+6PxrFmz8tFHH9VneSV77LFHunTpkiQ5/fTT89Zbb83T5o033sgZZ5xR4zgnnnhiGjdunPLy8vz4xz/Oe++9V23bOXPm5F//+leNberD9773vey9995Jkn//+9/529/+VmP7cePGzRMg+e9//5vPPvus2j7/+9//8uqrrybJQt8uc7XVVisFy6655poqXz9DhgzJhRdeuFDjVqdRo0Y56aSTkny9AtuAAQNqDARMmTKlzub+tjRv3ry0+suYMWNy1llnzdOmKIoceeSRpdDVkUceWWn7/fffnw8++KDaOT7//PPSSjVVneOKEFhV763aeP7553PuuefO8/zs2bPz85//vLTK1RFHHFFp+8Ybb5wNN9wwSXLFFVfk4YcfnmeMzz//vHT9atSo0TxjfNOvf/3rKm/DNnTo0Fx++eVJvg7RVQTcKvTp06d0S7YLL7ywytfbzTffnFtuuaXG+Wuy+uqrJ/n6OlaxIuPcvvzyy+y7776ZPn36Is/xXbD77rune/fuSZI//OEPeemll+Zp87///S/HHXdckq9XYqsuRPNdtOqqq2abbbZJkpxyyil54403kiQHH3xwtX2WWWaZ0vv5ySefzDHHHFPjLTk//PDD0q32KlS8fpKUgk3fdOKJJ2bUqFELsht1plOnTqVV8OZ3bRk0aFCSr293fNRRR1XZ5owzzigFNX/+85+nefPmtaqv4ro7fPjwXHDBBUm+DpHW9DlY2+8Ryy67bCmoe+ONN1Z5PXnuuefyu9/9blF2aYGUlZWlrKys9FoFAABY0ghuAQAALCUqQlrvv/9+ZsyYkSZNmmTTTTettn3FalwVt/Jr1KhRtSt01aezzjqrFCq78MILs9FGG+WKK67I008/nVGjRuXOO+/M8ccfn549e+aee+5pkBpbtGhRWm3qk08+ySabbJJzzz03Tz/9dJ5++umcc8452XTTTVNeXl76AbuqWzStvfba+ctf/pIkefnll9OnT5/85je/yX333ZfRo0fnqaeeyo033pijjjoqPXr0yP77719j4Km+XHLJJaXbyB177LHp169frrzyyjz99NMZPXp0Hnroofz1r3/NDjvskNVWWy233XZbpf7/+Mc/svzyy2efffbJpZdemqFDh+b555/Po48+mnPPPTdbbLFFKRBy+OGHL1RtnTp1Kq1Act9992XHHXfM7bffnpEjR+bee+/NoYcemj322COrrLJKll122To4Gl/XuMceeyRJbrnllqy11lo599xzS/s1bNiwXH755dl3333TvXv3nH766XUy77fp1FNPLZ3j008/PT/+8Y9z9913Z9SoUbntttuy3Xbb5dprr03y9Qp+hx12WKX+N954Y1ZaaaX0798/5513Xh5++OGMHj06w4YNy8UXX5zNNtss77//fpKqz/Hmm2+eJLnzzjtz2WWXZcyYMXnzzTfz5ptv1iqwueGGG+aEE07Ivvvum/vuuy+jRo3KTTfdlC222CL33ntvkq9Xldt1113n6XvFFVekWbNmmT17dnbZZZccd9xxGTp0aEaMGJErrrgiG2ywQSn4c9xxx9V427R1110377//fvr27ZuLLroozz33XB5//PGcdNJJ2XnnnTN79uw0adIkF1100Tx9mzRpUgqIjRkzJtttt13uuOOOjB49Ovfdd18OOeSQ/OxnPysdw0VxwAEHJPl6VaT+/fvnj3/8Y4YNG5Znn302l1xySdZbb7089thj2WKLLRZ5ju+CZs2a5fLLL09ZWVmmTJmSLbbYImeddVaefPLJPPPMM/n73/+eDTfcMBMmTEiS/OUvf0nnzp0buOqFUxEGqrgdXrt27fLjH/+4xj5nnnlmNtlkkyTJeeedlw022CAXXXRRnnjiidK1+sILL8zuu++eFVdccZ4VDHfaaadSuPmUU07J4Ycfnvvvvz8jR47MTTfdlO233z7nnHNOvb9+mjRpUgpCXnXVVbnxxhvzyiuvlK4tkyZNKrU9/PDDs9lmmyX5egWs73//+7ntttsyatSo3H333dlrr71KodZVV121ToJNe++9d+nWhxWhzppCdkntv0c0atQo++23X5LkxRdfzJZbbpkbb7wxI0aMyMMPP5xjjz02W2+9dVq0aFFaCRMAAICFVAAAALBUuOqqq4okpX8bbbRRje3//e9/V2q/7rrrzneOirannXZaje369etXJCn69es3z7ZHH320NM6jjz5aZf+PP/642HrrrSvVV9W/q6++ulK/q6++urRt3Lhx1dY3bty4asdYGL///e+LsrKyKmtr1apVcffddxdbbbVVkaTYeeedqx3n8ssvL1q1ajXf/W3WrFnxxhtvVOq7IMezQk3nb+DAgUWSYqWVVlqgff/ggw9K+za/fwcddFClvhWvj5r+NWrUqDjrrLMWqJZvevfdd4sVV1yx2rFXXHHFYuzYscVKK61UJCkGDhw4zxgL+lqqMHPmzOKII46o9vUw97+ePXsu0n4t6Dmq6f03t5r2vyi+fp+sscYaNe7LFltsUXz66afV1jq/f4cffngxZ86cefqPHj26aN68eZV9qqu3OnOfy1GjRhXrr79+jfszZcqUase6//77i3bt2tW4T4MGDapyn4qi8jG/4ooriiZNmlT7Xr/xxhurrWPatGnFpptuWm0N22yzTTFmzJgar3OnnXZaaXtVzjjjjBr389hjj53v+2R+r7FFUdN1rMKCvgcqDB48uNrXW5KicePGxR//+Mda1bSgnzsLc01fENOnTy86dOhQGvPnP//5AvWbMmVKseeeey7Q+3jbbbedp/99991XtGjRolav0YX9XFoQd911V7XX6W+ev08//bTYYostatz3Nddcsxg/fnyd1XfEEUeUxm7fvn3x5ZdfLlC/2nyP+Oyzz4r11luv2j4dO3Yshg4dWuvvdtWp6Leg71cAAIDFjRW3AAAAlhLfvM3h/FbP+uZtFBv6Nolz69y5c4YOHZrbb789P/7xj7PCCiukefPmadGiRVZZZZXsvffe+de//pWf/exnDVrnySefnKFDh2b33XdPly5d0rx586y00ko5+OCDM2LEiOyyyy6ZMmVKkpRW0ajKz3/+87z99ts544wzssUWW6Rz585p0qRJWrdunV69emWvvfbKpZdemvfffz+rrbZafe1ejbp165Zhw4blrrvuyn777ZdVVlklrVq1StOmTbPssstm8803z7HHHpuhQ4fmqquuqtT3xhtvLK1Atd5666Vbt25p0qRJ2rRpk7XWWitHHHFERo8enVNOOWWRauvRo0dGjRqV448/Pr169Urz5s3Tvn37rLvuujnttNPy/PPPp3fv3nVxGEqaNm2aiy++OC+88EJ++ctfZu2110779u3TuHHjtG/fPuutt14OOeSQ3HrrrXnllVfqdO5vy8orr5wXXnghF154Yfr165dOnTqladOm6dq1a3beeedcd911GTZsWOm2fXP7+9//nuuvvz4HH3xwNtxwwyy//PJp1qxZWrZsmV69emXgwIEZPnx4LrnkkjRqNO9/vlpvvfXy1FNP5Wc/+1lWXHHFWt+CrEKHDh3y5JNP5uyzz856662Xtm3bpk2bNtloo41ywQUXZOjQoWnbtm21/Xfccce8+eabOemkk7LeeuulXbt2ad68eVZcccXst99+GT58eC688MIq9+mbDj300AwfPjz77LNPunfvnmbNmmX55ZfPgAEDMnr06Pz0pz+ttm+rVq3yyCOP5A9/+EPWXnvttGzZMu3atctGG22UCy+8MA899FBat269SMeowqmnnpq77747O+64Yzp06JBmzZplhRVWyJ577pkHHnigtMrPkmDgwIF59dVX86tf/SprrrlmWrdunZYtW2bVVVfNz3/+84wePTonnnhiQ5e5SFq0aFG6vW0y/xWcKrRt2za33XZbhg8fnkMPPTTf+9730rZt2zRp0iQdO3bMRhttlEGDBuWee+7Jgw8+OE//nXbaKSNGjMj++++f7t27lz4b+vXrl8svvzwPP/xwrV+ji6J///55+OGH86Mf/ahUV3U6duyYYcOG5dprr83OO++crl27pmnTpunUqVO22WabXHjhhXn++eez0kor1Vl9FavdJclPf/rTtGzZcoH61eZ7RPv27fPEE0+UVjxt0aJF2rRpkzXXXDPHHXdcXnjhhe/Ud0QAAIDFTVlRFEVDFwEAAABLo1mzZqV9+/aZPn16TjnllNJtlYD6M3jw4Bx00EFJknHjxmXllVdusFpWXnnlvPPOOxk4cGAGDx7cYHWwdNliiy3y5JNPpnfv3hk7dmxDl0MNrrjiitKtZ5955plsvPHGDVwRAAAAtWXFLQAAAGgg//3vfzN9+vQkyaabbtrA1QCwtHnttdfy5JNPJlnw1bZoOBUrVPbp00doCwAAYAkhuAUAAADfkjfffLPabePHj8+vf/3rJEnXrl2z00471VdZAJAk+fOf/5zk61smHnjggQ1bDDUaNmxYnn766STJ4Ycf3sDVAAAAUFeaNHQBAAAAsKRaY401sssuu2TXXXfNWmutldatW+ejjz7Ko48+mksvvTSfffZZkuQvf/lLmjTxP9EB+HZNnz4977//fr788sv897//Ld2S87DDDkunTp0atjjm8c4772TGjBkZO3ZsjjnmmCRJt27drI4GAACwBPFfhQEAAOBbMmfOnAwZMiRDhgypcnujRo3y+9//Pvvvv389VwbA0uiZZ57JtttuW+m5Hj165PTTT2+YgqhRv3798s4771R67oILLkjLli0bqCIAAADqmuAWAAAAfEuGDBmSe++9N08++WQ+/PDDfPrpp2nevHmWX375bLPNNhk0aFD69OnT0GUCsJQpKyvLcsstl+222y5/+MMf0qFDh4YuiRq0bds2ffr0ycknn5z+/fs3dDkAAADUobKiKIqGLgIAAAAAAAAAAGBpYsWtWigvL8+ECRPStm3blJWVNXQ5AAAAAAAAAABAAyuKIlOnTk337t3TqFGjatsJbtXChAkT0qNHj4YuAwAAAAAAAAAA+I753//+lxVWWKHa7YJbtdC2bdskXx/kdu3aNXA1AAAAAAAAAABAQ5syZUp69OhRyhZVR3CrFipuj9iuXTvBLQAAAAAAAAAAoKQiW1Sd6m+iCAAAAAAAAAAAwLdCcAsAAAAAAAAAAKCeCW4BAAAAAAAAAADUM8EtAAAAAAAAAACAeia4BQAAAAAAAAAAUM8EtwAAAAAAAAAAAOqZ4BYAAAAAAAAAAEA9E9wCAAAAAAAAAACoZ4JbAAAAAAAAAAAA9UxwCwAAAAAAAAAAoJ41aegCSIqiyKxZs1JeXt7QpcBio1GjRmnSpEkaNZI/BQAAAAAAAAAWP4JbDWjOnDn55JNPMnXq1MyaNauhy4HFTqNGjdKqVau0a9cu7du3b+hyAAAAAAAAAAAWmOBWA5kzZ07+97//ZcaMGWnfvn3atGmTxo0bp6ysrKFLg++8oihSXl6er776Kl988UUmTJiQ6dOnp2vXrt5DAAAAAAAAAMBiQXCrgXzyySeZMWNGVlxxxbRs2bKhy4HFUuvWrdOpU6dMnjw5EydOTLNmzdKxY8eGLgsAAAAAAAAAYL4aNXQBS6OiKDJ16tS0b99eaAvqQIcOHdK2bdt89tlnKYqiocsBAAAAAAAAAJgvwa0GMGvWrMyaNStt2rRp6FJgidG+ffvMmDEjs2fPbuhSAAAAAAAAAADmS3CrAZSXlydJGjdu3MCVwJKjSZOv7/w6Z86cBq4EAAAAAAAAAGD+BLcaUFlZWUOXAEsM7ycAAAAAAAAAYHEiuAUAAAAAAAAAAFDPBLcAAAAAAAAAAADqmeAWAAAAAAAAAABAPRPcAgAAAAAAAAAAqGeCWwAAAAAAAAAAAPWsSUMXAN+2xx57LNtuu+08zzdu3Djt2rVL+/bt06NHj/Tt2zdbbrlldttttzRr1qwBKgUAAAAAAAAAYGkhuLUY6Hv8tQ1dwrdm5LkDGmzuOXPmZPLkyZk8eXLGjx+f4cOH5x//+EeWXXbZHHXUUfntb3+bJk28RQAAAAAAAAAAqHtSKSxVjjjiiPzf//1f6e8vvvgikydPzosvvpiHH344Dz30UD7++OP87ne/y5AhQ3LXXXdl2WWXbcCKAQAAAAAAAABYEglusVTp0qVL+vTpM8/zP/jBD3LCCSfk5Zdfzv7775/Ro0fn2WefzR577JFHHnnErRMBAAAAAAAAAKhTjRq6APgu6d27d5544omsv/76SZInnngiF110UQNXBQAAAAAAAADAkkZwC76hZcuWue6661JWVpYk+ctf/pJZs2aVto8fPz5lZWUpKyvL4MGDkyS33357dtlll3Tv3j1NmjTJNttsU2nMp59+Oqecckq22WabdOvWLc2aNUu7du3Su3fvHHHEEXn55ZdrrOnAAw9MWVlZVl555STJxIkTc9xxx6VXr15p1apVll9++eyzzz4ZO3ZspX7jx4/PUUcdlV69eqVly5bp2rVr9ttvv7z11ls1zjdmzJj8/ve/z0477ZQVVlghzZs3T5s2bbL66qtn4MCBefrppxfgSAIAAAAAAAAAUB23SoQqrLXWWtlhhx3ywAMPZMKECXnuueey+eabz9OuKIoMGDAg1113XbVjDR48OAcddNA8z8+aNSuvvPJKXnnllVxxxRU5//zz83//93/zre2FF17IzjvvnIkTJ5aemz59em655Zbcc889ue+++7LlllvmkUceyZ577pnPP/+81O6rr77KDTfckHvvvTfDhw/PWmutNc/4jz32WLbddtt5np85c2befPPNvPnmm7n22mvz29/+NmefffZ86wUAAAAAAAAAYF6CW1CN7bffPg888ECSZPjw4VUGt/7xj3/kxRdfzFZbbZUjjjgivXr1ymeffZbx48eX2syePTsdOnTIj370o2y99dZZffXV07p160yYMCGjRo3K+eefn08++SRHHnlk1lhjjWy33XbV1vTll19mjz32yMyZM/PHP/4x/fr1S+PGjXPfffflj3/8Y6ZNm5YDDjggDz74YHbfffe0b98+Z555ZjbZZJPMnj07t912W/7xj39k8uTJOeSQQ6pcOWv27Nlp3bp1+vfvn+222y5rrLFG2rVrl48++ihjx47N+eefn3feeSd/+tOf0qtXrypDaQAAAAAAAAAA1ExwC6qxwQYblB6//vrrVbZ58cUXM2DAgAwePLh0a8Vv+sEPfpB99903rVq1qvT8+uuvn/79++eoo47K1ltvnRdffDGnnXZajcGtjz/+OEVR5Nlnn82qq65aen6TTTZJ586dc+SRR2b8+PHZfPPN061btzzxxBNZdtllS+222GKLNGnSJOeee26eeeaZjB49Ouuvv36lOdZbb7289957WWaZZeaZf6eddsqRRx6ZXXfdNQ8++GDOOOOMDBgwII0bN662ZgAAAAAAAAAA5tWooQuA76pOnTqVHk+ePLnKNssss0wuvPDCakNbSbL88svPE9qaW8WqWEny+OOP59NPP62xrrPOOqtSaKvCwQcfnBYtWiT5OuB1/vnnVwptVTjiiCNKj4cPHz7P9s6dO1cZ2qrQrFmznHvuuUmSd955J88//3yN9QIAAAAAAAAAMC8rbkE12rRpU3o8derUKtvstttuadu27UKNO23atHz88ceZNm1aiqJIkjRt2rS0/YUXXqh21a2ysrLss88+VW5r2bJlVl999bz00kvp0KFDdtpppyrb9ezZM23bts3UqVPz9ttvz7feGTNm5MMPP8wXX3yR8vLyJCnVXVFv37595zsOAAAAAAAAALB46Xv8tQ1dQkaeO6ChS/jWCG5BNeYOa7Vr167KNuuss84CjfXJJ5/kb3/7W2677ba88cYblYJPVbWtTufOndOxY8dqt1eslLXaaqvVuArYMsssk6lTp1YbSJs2bVrOP//8/Pvf/87YsWMzZ86cRaoXAAAAAAAAAICqCW5BNeYOJFUXlurQocN8xxk5cmR22mmn+d4CscL06dOr3VbTLReTpFGjRgvVrqpA1vjx47Pddttl3Lhx8ys1Sc31AgAAAAAAAABQtUYNXQB8V40ePbr0+Hvf+16VbRo3blzjGDNnzsw+++yTTz/9NE2bNs2vf/3rDB06NB988EG++uqrFEWRoijy1ltvlfrUtBpXfTjggAMybty4lJWV5eCDD84DDzyQ//3vf/nqq69SXl6eoigqBb4aul4AAAAAAAAAgMWRFbegGg8++GDp8ZZbbrlIYzzyyCN5++23kyQXX3xxDj300CrbTZo0aZHGr2uvvvpqHn/88STJSSedlN///vdVtvuu1AsAAAAAAAAAsLiy4hZUYcyYMXn44YeTJD169MiGG264SOOMHTu29PgnP/lJte1GjBixSOPXtcWtXgAAAAAAAACAxZXgFnzD9OnTM2DAgNItAI877rg0abJoi9PNnj279HjatGlVtikvL88VV1yxSOPXtQWpN0kuvfTS+igHAAAAAAAAAGCJJbgFc3n55Zez5ZZbZvTo0UmSfv365Ygjjljk8VZfffXS48GDB1fZ5sQTT8yoUaMWeY66tCD1XnLJJbnjjjvqqSIAAAAAAAAAgCXToi0jBIupjz76KGPGjCn9PW3atEyePDkvvvhiHn744Tz44IOllbY23XTT3HrrrWnatOkiz7fTTjulS5cu+eijj3LKKadk/Pjx2WOPPdK5c+e8+eabueKKK/Lwww9niy22yBNPPFHr/aut9ddfP3369MmYMWNy2WWXZfLkyTnggAOy3HLL5b333sv111+fW2+99TtTLwAAAAAAAADA4kpwi6XKJZdckksuuaTGNssuu2yOPvro/OY3v1nkWyRWaN26da699trsvvvu+eqrr3LZZZflsssuq9Rmm222yYUXXpg+ffrUaq66UFZWluuuuy7bbbddJk+enJtvvjk333xzpTZrr712brnllnTv3r2BqgQAAAAAAAAAWPwJbrHUatSoUdq2bZv27dtnpZVWSt++fbPVVltl1113TbNmzepsnp122ikjRozIn/70pzzyyCP5+OOPs8wyy6R3797Zb7/9csghh+Tdd9+ts/lqa7311svzzz+fs88+O/fee28mTJiQtm3bZrXVVss+++yTQYMGpUWLFg1dJgAAAAAAAADAYq2sqLgvHAttypQpad++fT7//PO0a9dugft99dVXGTduXHr27CkAA3XE+woAAAAAAAAA6lbf469t6BIy8twBDV3CQlvQTFGjeqwJAAAAAAAAAACACG4BAAAAAAAAAADUO8EtAAAAAAAAAACAeia4BQAAAAAAAAAAUM8EtwAAAAAAAAAAAOqZ4BYAAAAAAAAAAEA9E9wCAAAAAAAAAACoZ4JbAAAAAAAAAAAA9UxwCwAAAAAAAAAAoJ4JbgEAAAAAAAAAANQzwS0AAAAAAAAAAIB6JrgFAAAAAAAAAABQzwS3AAAAAAAAAAAA6pngFgAAAAAAAAAAQD0T3AIAAAAAAAAAAKhnglsAAAAAAAAAAAD1THALAAAAAAAAAACgngluAQAAAAAAAAAA1DPBLQAAAAAAAAAAgHomuAXUibKyspSVleX0009v6FIAAAAAAAAAAL7zBLdY6sycOTM33nhjBgwYkDXWWCOdOnVK06ZN07lz5/Tt2zdHHHFEHnrooZSXlzd0qQAAAAAAAAAALKGaNHQBzN+7Z67d0CV8a1Y89aV6ne/222/Psccem/Hjx8+z7dNPP82nn36aUaNG5dJLL02vXr3yt7/9Lf3796/XGgEAAAAAAAAAWPIJbrHUOOuss3LqqaeW/t5hhx3ywx/+ML17984yyyyTSZMm5bXXXsuQIUPy4IMP5vXXX8/JJ58suAUAAAAAAAAAQJ0T3GKpcPXVV5dCW126dMnNN9+cfv36zdNu++23z6BBgzJmzJgcc8wx+fjjj+u7VAAAAAAAAAAAlgKCWyzx3n///Rx55JFJktatW2fo0KFZY401auzTp0+f3H///bnhhhvqo0QAAAAAAAAAAJYyjRq6APi2/f3vf8+XX36ZJDnzzDPnG9qq0KhRo+y///5Vbnv88cdzwAEHZOWVV06LFi2yzDLLZP31188pp5xS4ypdjz32WMrKylJWVpbHHnssRVHkyiuvzJZbbplOnTqlXbt22XjjjXPddddV6jdz5sxceuml2XTTTdOxY8e0bds2W2yxRW6++eYF2peJEyfm5JNPzoYbbpiOHTumefPm6dGjR/bZZ5889NBDCzTGDTfckG222SYdOnRImzZt0qdPn5x22mn57LPPqu0za9asdOvWLWVlZdl5553nO8eYMWNKx+ecc85ZoLoAAAAAAAAAABZHVtxiiVYURa655pokX6+29fOf/7xW45WXl+eoo47KRRddVOn5GTNm5Pnnn8/zzz+fCy+8MLfcckt22GGHGseaNWtWfvSjH2XIkCGVnn/uuecyYMCAjBgxIuedd14mT56c3XffPcOGDavU7sknn8yTTz6ZN998MyeddFK18/zrX//KL37xi0ybNq3S8++9915uueWW3HLLLTnkkENy6aWXpkmTeS8Js2fPzr777ptbbrml0vNjx47N2LFjc/3111cb/mratGkGDBiQc889Nw8++GDef//9LL/88tXWetVVVyVJmjRpkgEDBlTbDgAAAAAAAABgcWfFLZZoY8eOzSeffJIk2WqrrdK2bdtajffb3/62FNrq2bNnLr300jz77LN59NFHc8wxx6Rp06b5/PPPs+uuu+aFF16ocazf/e53GTJkSPbbb7/cfffdGTlyZG688cZ873vfS5Kcf/75eeihh3LggQfmySefzBFHHJEHHnggI0eOzJVXXpnu3bsnSU499dSMHTu2yjluvvnmHHDAAZk2bVpWWWWV/O1vf8t9992XkSNH5rbbbssuu+ySJLnyyivzm9/8psoxjjvuuFJo63vf+16uvPLKPPfcc3nooYfyi1/8IuPHj89PfvKTavfz0EMPTfJ16O3aa6+ttt2sWbNy/fXXJ0l+8IMfpFu3bjUdPgAAAAAAAACAxZoVt1iizR2e6tu3b63Geumll/LXv/41SdKnT58MHz48yyyzTGn7Nttskx133DH9+/fPzJkzc9hhh+WZZ56pdrxnnnkm//jHP/KrX/2q9NwGG2yQbbbZJr169crUqVOz77775pNPPsntt9+e3XffvVK7DTfcMOuvv37mzJmTyy+/POedd16l8T/55JMcdthhKYoiBx98cC677LJKK2ptsMEG2XPPPXPyySfnj3/8Y84777z84he/KAXHKvb5ggsuKLUfOnRo2rRpU9r+/e9/P5tvvnkGDhxY7X726tUrW221VYYPH57BgwfnxBNPrLLdXXfdVbrN5MEHH1zteAAAAAAAAAAASwIrbrFE+/TTT0uPu3TpUquxLrnkkpSXlydJ/vnPf1YKbVXYeeedS6GjZ599Ns8991y1422yySaVQlsVunXrlj322CNJ8vHHH2efffapFNqqsM4662TLLbdMkgwfPrzKej///PMsv/zyufjii6u8DWKSnHHGGVl++eWrXBHr0ksvLe3z5ZdfXim0VWHAgAH5wQ9+UO1+Jv9v1a3XX389TzzxRJVtrr766iRfn6ddd921xvEAAAAAAAAAABZ3glss0aZOnVp63Lp161qN9dBDDyVJ1lprrWyyySbVtvv5z38+T5+q/PSnP61227rrrrtQ7d5+++15tt15551Jkl133TXNmzevdowmTZpks802S5I89dRTlbZV1L/22mvXuGLZ/FbI2nvvvdO+ffsk/y+gNbcPP/ww9957b5LkgAMOqDZkBgAAAAAAAACwpBDcYonWtm3b0uNp06Yt8jgzZszIG2+8kSQ1hraSZP3110/Tpk2TJGPGjKm2Xa9evardNvdqXgvSbu6AWpLMmTMnzz//fJLksssuS1lZWY3/br311iTJxIkTS2PMvc8bbbRRtTUkycYbb1zj9pYtW2bfffdNktx888358ssvK22/7rrrMnv27CRukwgAAAAAAAAALB0Et1iiderUqfT4ww8/XORxJk+eXHo8v1suNm3atDTvpEmTqm3XqlWrarc1atRoodpV3M6wwqRJk0pBqIUxd6Bq8uTJKYoiyfz3uWvXrvMdu+J2iVOnTi0FxSpUrMK1ySabpHfv3gtVMwAAAAAAAADA4sj9yFiizX3LwVGjRtXJmGVlZXUyzrdpzpw5pceHHnpofvWrXy1Qv2bNmlX5fF3s8wYbbJD1118/o0ePztVXX50BAwYkSZ555pm8/PLLSay2BQAAAAAAAAAsPQS3WKKttdZa6dy5cz755JMMHz48U6ZMSbt27RZ6nA4dOpQez2/lrtmzZ+fTTz9NknTs2HGh56oLc89bFEX69Omz0GPMfbvG+e3zgq5mduihh2bQoEEZOnRoxo0bl549e5ZW22rVqlV++tOfLnSdAAAAAAAAAACLI7dKZIlWVlaWgQMHJkmmTZuWf/7zn4s0TvPmzbP66qsn+XqFqJqMHj06s2bNSpJFCkzVhWbNmmWttdZKkjzxxBOLNEaLFi1K+/zcc8/V2HZ+2yvst99+admyZYqiyODBgzN9+vT8+9//TpLstddeixSqAwAAAAAAAABYHAluscQ75phj0qpVqyTJqaeemldffXWB+pWXl+df//pX6e/tt98+STJ27Ng8++yz1fabOxxW0ach/PCHP0ySvPrqq7n//vsXaYyK+l966aWMHj262nZXXXXVAo3Xvn37/PjHP06SXHPNNbn11lvz+eefJ3GbRAAAAAAAAABg6SK4xRJv+eWXz4UXXpjk61W3+vXrl6FDh9bY5+WXX87OO++cc889t/TcEUcckUaNvn7LHHbYYZkyZco8/R544IFceeWVSZKNN944G220UV3txkL71a9+lTZt2iRJDjrooIwdO7bG9nfffXdefPHFSs/94he/SFlZWZKv93natGnz9PvXv/6Ve+65Z4HrOvTQQ5Mk77zzTn7zm98kSVZdddX069dvgccAAAAAAAAAAFjcCW6xVDjooINy5plnJkk++uijbLPNNtlpp51y8cUX59FHH83o0aPz8MMP55JLLsmuu+6addZZJw8++GClMdZee+0ce+yxSZIXXnghG2ywQa644oqMGDEiQ4cOzXHHHZddd901c+bMSbNmzXLZZZfV+37OrWvXrrnmmmtSVlaWDz74IBtuuGGOOOKI3HnnnRk1alSeeeaZ3HbbbTnhhBOy6qqrZtddd827775baYx11103gwYNSpKMGDEiG264YQYPHpyRI0fmkUceyRFHHJEBAwZkww03XOC6tt566/Tq1StJMnHixCTJgQceWAqIAQAAAAAAAAAsDZo0dAFQX373u99lrbXWyrHHHpvx48fngQceyAMPPFBt+7XWWivnnHNOpef+9Kc/Zdq0abn44ovz1ltv5bDDDpunX/v27XPz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tttuuyTJ1VdfnTXXXDNPP/10Nt100zzwwAN5+eWX89BDD6Vr165Zb731ctZZZ+WEE07I6aefnmbNmjXErgEAAAAAAAAAAEuBWgW3KkJRi6KsrCwPP/xwbaYv+fzzz5MkHTt2TJKMHDkys2bNyvbbb19qs8Yaa2TFFVfMU089lU033TRPPfVU1l577XTt2rXUZqeddsoRRxyRsWPHZv31159nnhkzZmTGjBmlv6dMmVIn9QMAAAAAAAAAAEuXWgW3HnvssZSVlaUoimrblJWVVfq7ou03n19U5eXlOfroo7PFFlukT58+SZKJEyemWbNmWWaZZSq17dq1ayZOnFhqM3doq2J7xbaqnH322TnjjDPqpG4AAAAAAAAAAGDpVavg1tZbbz3fANa0adPy5ptv5rPPPktZWVl69eqV5ZZbrjbTVjJo0KCMGTMmjz/+eJ2NWZ0TTzwxv/71r0t/T5kyJT169PjW5wUAAAAAAAAAAJYstV5xa0Hdc889OeqoozJp0qRceeWV2WKLLWozdZLkyCOPzF133ZVhw4ZlhRVWKD3frVu3zJw5M5999lmlVbc+/PDDdOvWrdTm2WefrTTehx9+WNpWlebNm6d58+a1rhsAAAAAAAAAAFi6NaqviXbZZZc8/vjjadKkSfbYY4+8//77izxWURQ58sgj85///CePPPJIevbsWWl7375907Rp0zz88MOl51577bW8++672WyzzZIkm222WV566aV89NFHpTYPPvhg2rVrl969ey9ybQAAAAAAAAAAAPNTb8Gt5OuVrI455ph88sknOeeccxZ5nEGDBuX666/PDTfckLZt22bixImZOHFipk+fniRp3759DjnkkPz617/Oo48+mpEjR+aggw7KZpttlk033TRJsuOOO6Z379454IAD8sILL+T+++/PKaeckkGDBllVCwAAAAAAAAAA+FbVa3ArSbbccsskyd13373IY1xyySX5/PPPs80222S55ZYr/bvppptKbf7+979n1113zV577ZWtt9463bp1y+23317a3rhx49x1111p3LhxNttss+y///4ZMGBAzjzzzEXfOQAAAAAAAAAAgAXQpL4nbNasWZJkwoQJizxGURTzbdOiRYtcdNFFueiii6pts9JKK+Wee+5Z5DoAAAAAAAAAAAAWRb2vuPX4448nSVq1alXfUwMAAAAAAAAA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2GOPvPDCC6lUKjnqqKNq2TQAAAAAAAAAAEDDal/Lyptsskm++c1v5uc//3nuu+++rLfeetl///2z3XbbZfXVV0+STJ8+PXfffXfGjBmTN954I5VKJccee2y22GKLevQDAAAAAAAAAAA0nJoGt5LkJz/5SV555ZWMHDkyr7/+ekaOHJmRI0e+b7miKJIkX/3qV/Pzn/+81s0CAAAAAAAAAAA0rJpulZgkTU1NufDCC3Pddddl4MCBSf49pPXujyTZdtttc8MNN+SCCy5IpVKpdbMAAAAAAAAAAAANq+bBrYX22muvjB07Nv/85z9z66235sorr8yVV16ZW2+9Nf/6179yzz335Atf+EJdtnX33Xdnzz33TN++fVOpVHLdddct8vxhhx2WSqWyyMeuu+66yDKzZs3KwQcfnG7duqVHjx458sgj89prr9WlDwAAAAAAAAAA4MPUfKvE9+rZs2c+97nP1ftlF/H6669n8803zxFHHJF99tlnscvsuuuui9yysWPHjos8f/DBB2f69Om55ZZbMn/+/Bx++OH52te+ltGjR7doOwAAAAAAAAAAQN0Ht8qw2267ZbfddvvQZTp27Jg+ffos9rnHHnssN998cx588MFstdVWSZJzzjknu+++e37yk5+kb9++i11v7ty5mTt3bvPv58yZs5SfAQAAAAAAAAAAsDyr260S25o777wzvXr1ygYbbJCvf/3reemll5qfGzduXHr06NE8tJUkO++8c5qamnL//fd/4Gv+8Ic/TPfu3Zs/1lprrRb9HAAAAAAAAAAAgGVTTVfcOuKII5Z63UqlkgsvvLCWzX+gXXfdNfvss0/WXXfdPPXUU/ne976X3XbbLePGjUu7du0yY8aM9OrVa5F12rdvn549e2bGjBkf+LrDhw/P8ccf3/z7OXPmGN4CAAAAAAAAAACWWE2DWxdffHEqlcoSr1cURYsObh1wwAHNv/7kJz+ZzTbbLB//+Mdz5513Zqeddlrq1+3YsWM6duxYj0QAAAAAAAAAAGA5VtPgVr9+/T5ycOv111/PSy+91Dysteqqq6ZLly61bHaJfexjH8uqq66aJ598MjvttFP69OmTF198cZFl3n777cyaNSt9+vQptQ0AAAAAAAAAAFj+1DS49cwzz1S13Msvv5wrrrgip5xySnr06JEbbrghG2ywQS2bXiL/+Mc/8tJLL2X11VdPkgwcODCzZ8/O+PHj079//yTJ7bffngULFmTAgAGldQEAAAAAAAAAAMunpjI2svLKK+eYY47J2LFj8+KLL2a33XbLyy+/vNSv99prr2XixImZOHFikmTatGmZOHFinn322bz22ms58cQT87e//S3PPPNMbrvttgwZMiTrrbdeBg8enCTZaKONsuuuu2bYsGF54IEHMnbs2Bx33HE54IAD0rdv33p8ygAAAAAAAAAAAB+olMGthTbYYIP8x3/8R5555pn89Kc/XerXeeihh7Lllltmyy23TJIcf/zx2XLLLXPKKaekXbt2eeSRR7LXXntl/fXXz5FHHpn+/fvnnnvuSceOHZtf4/LLL8+GG26YnXbaKbvvvns++9nP5oILLqj5cwQAAAAAAAAAAPgoNd0qcWnsvPPOOfPMM/OHP/wh/+///b+leo1BgwalKIoPfP4vf/nLR75Gz549M3r06KXaPgAAAAAAAAAAQC1KveJWkqy00kpJkmeffbbsTQMAAAAAAAAAALQJpQ9uTZgwIUnSoUOHsjcNAAAAAAAAAADQJpQ6uDVt2rScdtppqVQq2WKLLcrcNAAAAAAAAAAAQJvRvpaVR40a9ZHLLFiwIC+//HIeeuihXH/99XnjjTdSqVRy9NFH17JpAAAAAAAAAACAhlXT4NZhhx2WSqVS9fJFUSRJ/uM//iP7779/LZsGAAAAAAAAAABoWDUNbiX/N4z1UXr06JHtt98+xxxzTHbZZZdaNwsAAAAAAAAAANCwahrcmjZt2kcu09TUlK5du6ZHjx61bAoAAAAAAAAAAGCZUdPg1tprr12vDgAAAAAAAAAAgOVGU2sHAAAAAAAAAAAALG8MbgEAAAAAAAAAAJTM4BYAAAAAAAAAAEDJ2lezULt27eq+4UqlkrfffrvurwsAAAAAAAAAANDWVTW4VRRFS3cAAAAAAAAAAAAsN6oa3Dr11FM/9Pk//elPeeihh5Ikm2yySbbeeuv07t07STJz5sw8+OCDmTRpUiqVSrbaaqvsvvvuNWYDAAAAAAAAAAA0rpoHt84444w89NBD2XzzzXPBBRfk05/+9GKXe/DBB3PUUUfloYceyh577JFTTjll6YoBAAAAAAAAAAAaXFMtK99222057bTTsv766+fee+/9wKGtJPn0pz+de+65J+utt15OP/303HrrrbVsGgAAAAAAAAAAoGFVdcWtD/LLX/4ylUol3/3ud7Piiit+5PIrrrhivvvd7+bII4/MOeeck5133rmWzQMAAAAAAAAsN/qfOKq1EzJ+xNDWTgCAZUZNV9x66KGHkiSbbbZZ1etsvvnmSf5960QAAAAAAAAAAIDlUU2DW7NmzUqSvPLKK1WvM2fOnCTJyy+/XMumAQAAAAAAAAAAGlZNg1t9+/ZNklxzzTVVr/P73/8+SbL66qvXsmkAAAAAAAAAAICGVdPg1q677pqiKPKb3/wmY8aM+cjlf//73+c3v/lNKpVKdt9991o2DQAAAAAAAAAA0LBqGtz63ve+l27dumXBggU58MAD88UvfjHXXXddnn/++cyfPz9vv/12nn/++Vx33XXZe++9s//+++edd95J165dM3z48Hp9DgAAAAAAAAAAAA2lfS0rr7HGGvnjH/+YPffcM3PmzMkf//jH/PGPf/zA5YuiSNeuXXP99ddnjTXWqGXTAAAAAAAAAAAADaumK24lyXbbbZdHH300X/rSl9LU1JSiKBb70dTUlH322SePPPJIdthhh3q0AwAAAAAAAAAANKSarri10FprrZWrr746M2fOzB133JFHH300s2bNSpKsvPLK+eQnP5kdd9wxffr0qcfmAAAAAAAAAAAAGlpdBrcW6t27dw444IAccMAB9XxZAAAAAAAAAACAZUrNt0oEAAAAAAAAAABgydT1iltJMnPmzEyaNKn5Vok9e/bMpptumt69e9d7UwAAAAAAAAAAAA2pLoNbRVHkggsuyLnnnpspU6YsdpmNN9443/jGNzJs2LBUKpV6bBYAAAAAAAAAAKAh1XyrxJdffjnbb799jjnmmEyZMiVFUSz2Y8qUKfn617+e7bffPrNnz65DOgAAAAAAAAAAQGOq6YpbRVFkyJAhGTt2bJJklVVWyX777ZcBAwakT58+SZIZM2bkgQceyJgxY/Kvf/0r9913X4YMGZK77rqr9noAAAAAAAAAAIAGVNPg1ujRo3PvvfemUqnkoIMOyvnnn5+uXbu+b7mhQ4fmRz/6UY499thceumluffee3PFFVfkwAMPrGXzAAAAAAAAAAAADammWyWOHj06SbLDDjvk0ksvXezQ1kIrrbRSLrnkkuywww4piiKXXXZZLZsGAAAAAAAAAABoWDUNbj388MOpVCo57rjjql7nG9/4RpJkwoQJtWwaAAAAAAAAAACgYdU0uDVr1qwkybrrrlv1OguXXbguAAAAAAAAAADA8qamwa3u3bsnSV544YWq15k+fXqSpFu3brVsGgAAAAAAAAAAoGHVNLi16aabJklGjhxZ9ToLl124LgAAAAAAAAAAwPKmpsGtfffdN0VR5Nprr81pp52Woig+dPkzzzwz11xzTSqVSr785S/XsmkAAAAAAAAAAICG1b6WlYcNG5ZzzjknU6dOzZlnnpk//OEPOeywwzJgwID06tUrlUolM2fOzP33359LLrkkkyZNSpJsuOGGGTZsWF0+AQAAAAAAAAAAgEZT0+BWhw4dctNNN2WnnXbKtGnTMnny5Jx44okfuHxRFPnYxz6Wm266Ke3b17RpAAAAAAAAAACAhlXTrRKTZJ111skjjzySb3/72+nevXuKoljsR/fu3XPCCSdk4sSJ6devXz3aAQAAAAAAAAAAGlJdLnu14oorZsSIETnrrLMyfvz4TJo0KbNmzUqS9OzZM5tuumn69++fFVZYoR6bAwAAAAAAAAAAaGg1DW6dccYZSZIBAwZk8ODBWWGFFTJw4MAMHDiwLnEAAAAAAAAAAADLopoGt0477bRUKpVce+219eoBAAAAAAAAAABY5tU0uLXKKqtk1qxZ6devX716AAAAAAAAgGVI/xNHtXZCxo8Y2toJAADv01TLyuutt16SZMaMGXWJAQAAAAAAAAAAWB7UNLi1//77pyiKjBkzpl49AAAAAAAAAAAAy7yaBreOOeaYbL755hk1alQuvvjiOiUBAAAAAAAAAAAs29rXsvKMGTPyu9/9LkceeWSOPPLIjB49OgcddFA222yzrLzyymnXrt2Hrt+vX79aNg8AAAAAAAAAANCQahrcWmeddVKpVJIkRVHktttuy2233VbVupVKJW+//XYtmwcAAAAAAAAAAGhINQ1uJf8e2FrcrwEAAAAAAAAAAFi8mga3Ro4cWa8OAAAAAAAAAACA5UZNg1uHHnpovToAAAAAAAAAAACWG02tHQAAAAAAAAAAALC8Waorbk2aNCl/+ctf8r//+79555130rdv3wwaNCjbbrttvfsAAAAAAAAAAACWOUs0uPXGG2/kiCOOyNVXX73Y5wcOHJirrroqa6yxRl3iAAAAAAAAAAAAlkVLdKvEfffdN1dffXWKoljsx3333ZfPfe5zeeON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hx+e3r17Z//9988NN9yQt99+ux6bBgAAAAAAAAAAaDh1Gdx6t7XWWivf+c538ve//z2TJk3K8OHDs/baa6coirz55pv5/e9/n7333jurr756vTcNAAAAAAAAAADQENq35ItvvPHGOeuss3LWWWflvvvuy+jRo3P55ZfnlVdeyaxZs1py0wAAAAAAQAPof+Ko1k5IkowfMbS1EwAAgOVM3a+4tTgvv/xyHn300TzyyCN59dVXy9gkAAAAAAAAAABAm9ViV9x66623cv311+fyyy/PX//618yfPz9JUhRFkmTrrbduqU0DAAAAAAAAAAC0aXUd3FqwYEFuueWWXH755bnuuuvy+uuvJ/m/Ya1PfOITOfjgg3PwwQfn4x//eD03DQAAAAAAAAAA0DDqMrj1t7/9LaNHj86YMWPyz3/+M8n/DWv17t07BxxwQA4++OBstdVW9dgcAAAAAAAAAABAQ6tpcOsHP/hBrrjiikybNi3J/w1rde3aNXvvvXcOPvjg7LTTTmlqaqq9FAAAAAAAAAAAYBlR0+DWWWedlUqlkqIo0qFDh+y66645+OCDs9dee6VTp071agQAAAAAAAAAAFim1HwprG233Ta/+tWvMn369Fx//fXZb7/9Wnxo6+67786ee+6Zvn37plKp5Lrrrlvk+aIocsopp2T11VdP586ds/POO+eJJ55YZJlZs2bl4IMPTrdu3dKjR48ceeSRee2111q0GwAAAAAAAAAAIKnxilvPPPNM+vXrV6+Wqr3++uvZfPPNc8QRR2SfffZ53/M//vGP88tf/jKXXHJJ1l133fzgBz/I4MGDM2XKlOahsoMPPjjTp0/PLbfckvnz5+fwww/P1772tYwePbrsTwcAAAAAAIA2pv+Jo1o7IeNHDP3Q558945MllXywfqc82toJAAANq6bBrdYY2kqS3XbbLbvttttinyuKIj//+c9z8sknZ8iQIUmSUaNGpXfv3rnuuutywAEH5LHHHsvNN9+cBx98MFtttVWS5Jxzzsnuu++en/zkJ+nbt29pnwsAAAAAAAAAALD8qWlwa3FmzpyZSZMmZdasWUmSnj17ZtNNN03v3r3rvanFmjZtWmbMmJGdd965+bHu3btnwIABGTduXA444ICMGzcuPXr0aB7aSpKdd945TU1Nuf/++7P33nsv9rXnzp2buXPnNv9+zpw5LfeJ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s/LKK+eLX/xiVY1ldd55553v248LPx588ME20Zgkjz/+eIYMGZJVV1013bp1y2c/+9nccccdVezFcjsffvjhfP7zn0+PHj2yyiqr5Gtf+1qp39efeeaZD/x6Xn311c3LPfvss9ljjz3SpUuX9OrVKyeeeGLefvvtNtX4H//xH+nfv386duyYLbbYoup9WGbn3//+9xx44IFZa6210rlz52y00Ub5xS9+0aYaX3rppey6667p27dvOnbsmLXWWivHHXdc5syZ06Y63+2ll17KmmuumUqlktmzZ7epxsU9f+WVV1bVWGZnklx88cXZbLPN0qlTp/Tq1SvHHntsm2m8+OKLP3CZF198sc10JsmDDz6YnXbaKT169MjKK6+cwYMH5+9//3ubarztttuyzTbbpGvXrunTp09OOumkqr+n16MzSWbMmJFDDjkkffr0yYorrphPfepTueaaaxZZppZzn7IaaznvKauz1nOfsvZlLec9ZXYutDTnPmU11nLeU2ZnsvTnPmU01nreU1ZnUtu5T1mNrX3ekyRPPfVU9t5776y22mrp1q1b9ttvv8ycOXORZVr72FNNY1s49nxUZ1s49lSzL9vCsaeazoVa69hTTWNbOPZUuy9b89jzUY1t5dhTzb5s7WNPNY21Hnt++MMf5tOf/nS6du2aXr165Ytf/GKmTp26yDJvvfVWjj322KyyyipZaaWV8qUvfel9HdW8p3bnnXfmU5/6VDp27Jj11lsvF198cZtqnD59eg466KCsv/76aWpqyre+9a2q+sru/MMf/pDPf/7zzX8uBg4cmL/85S9tqvHee+/Ntttum1VWWSWdO3fOhhtumLPPPruqxjI7323s2LFp37591e+3ltX4Qd8zZ8yY0aY6k38fw7///e9n7bXXTseOHbPOOuvkoosuajONhx122GL35SabbNLm9uXll1+ezTffPF26dMnqq6+eI444Ii+99FKbajzvvPOy0UYbpXPnztlggw0yatSoj+yrd2c1/1fyyCOPZLvttkunTp2y1lpr5cc//nGbanzrrbdy2GGH5ZOf/GTat2+/RP9XWmbnnXfemSFDhmT11VfPiiuumC222CKXX355m2qcOnVqdtxxx/Tu3TudOnXKxz72sZx88smZP39+m+p8tyeffDJdu3at+py3rMYPev/9b3/7W1Wdi2Nwq85ef/31bL755jnvvPPe91xRFPniF7+Yp59+Otdff30mTJiQtddeOzvvvHNef/315uXGjRuXXXfdNbvsskseeOCBPPjggznuuOPS1PR/X66DDz44kydPzi233JIbb7wxd999d772ta+1uc558+bly1/+cr7+9a9X3VZm4//8z/9kwYIF+c1vfpPJkyfn7LPPzq9//et873vfa1OdSbLjjjtmzJgxmTp1aq655po89dRT2XfffdtU40Lf+c530rdv36raWqvzjDPOyPTp05s/vvGNb7SpxmuuuSaHHHJIDj/88Pz973/P2LFjc9BBB1XVWFbnNttss8g+nD59er761a9m3XXXzVZbbdUmGpPkC1/4Qt5+++3cfvvtGT9+fDbffPN84QtfqPrErYzOF154ITvvvHPWW2+93H///bn55pszefLkHHbYYVU11qNzrbXWet/X8/TTT89KK62U3XbbLUnyzjvvZI899si8efNy33335ZJLLsnFF1+cU045pc00LnTEEUdk//33r3r/ld05fvz49OrVK5dddlkmT56c73//+xk+fHjOPffcNtPY1NSUIUOG5IYbbsjjjz+eiy++OLfeemuOPvroNrUv3+3II4/MZpttVnVf2Y0jR45cZLklOcksq/NnP/tZvv/97+e73/1uJk+enFtvvTWDBw9uM43777//+5YZPHhwdthhh/Tq1avNdL722mvZdddd069fv9x///25995707Vr1wwePLiqE+EyGv/+979n9913z6677poJEybkqquuyg033JDvfve7Ve3HenQmydChQzN16tTccMMNefTRR7PPPvtkv/32y4QJE5qXqeXcp6zGWs57yuqs9dynrH1Zy3lPmZ0LLc25T5mNS3veU2ZnLec+ZTTWet5T5r6s5dynjMa2cN7z+uuvZ5dddkmlUsntt9+esWPHZt68edlzzz2zYMGC5tdqzWNPtY2tfeypprO1jz3V7svWPvZU27lQaxx7lqSxNY891Xa25rGnmsa2cOypdl+25rGnmsZ6HHvuuuuuHHvssfnb3/6WW265JfPnz88uu+yyyDHwP//zP/PHP/4xV199de6666688MIL2WeffZqfr+Y9tWnTpmWPPfbIjjvumIkTJ+Zb3/pWvvrVr1Y1cFRW49y5c7Paaqvl5JNPzuabb171Piy78+67787nP//5/PnPf8748eOz4447Zs8991zsv+dbq3HFFVfMcccdl7vvvjuPPfZYTj755Jx88sm54IIL2tS+XGj27NkZOnRodtppp6r6WqNx6tSpi3zfrPZ9ojI799tvv9x222258MILM3Xq1FxxxRXZYIMN2kzjL37xi0X24XPPPZeePXvmy1/+cpval2PHjs3QoUNz5JFHZvLkybn66qvzwAMPZNiwYW2m8Ve/+lWGDx+e0047LZMnT87pp5+eY489Nn/84x9L25cLfdj/lcyZMye77LJL1l577YwfPz4jRozIaaedVtX3orIa33nnnXTu3Dn/8R//kZ133vkju1qr87777stmm22Wa665Jo888kgOP/zwDB06NDfeeGObaezQoUOGDh2av/71r5k6dWp+/vOf57e//W1OPfXUj2wss3Oh+fPn58ADD8x2221XVV9rNN56662LfN/s379/1a3vU9BikhTXXntt8++nTp1aJCkmTZrU/Ng777xTrLbaasVvf/vb5scGDBhQnHzyyR/4ulOmTCmSFA8++GDzYzfddFNRqVSK559/vs10vtvIkSOL7t27L3FbmY0L/fjHPy7WXXfdNt95/fXXF5VKpZg3b16bavzzn/9cbLjhhsXkyZOLJMWECROWqK+MzrXXXrs4++yzl6qrjMb58+cXa6yxRvG73/2u5saW7HyvefPmFauttlpxxhlntJnGf/7zn0WS4u67725+bM6cOUWS4pZbbmkznb/5zW+KXr16Fe+8807zY4888kiRpHjiiSdK63yvLbbYojjiiCOaf//nP/+5aGpqKmbMmNH82K9+9auiW7duxdy5c9tE47udeuqpxeabb75EXa3RudAxxxxT7Ljjjm268Re/+EWx5pprLnFjGZ3nn39+scMOOxS33XZbkaR4+eWX21Tje1+7Fi3VOWvWrKJz587Frbfe2mYb3+vFF18sOnToUIwaNapNdT744INFkuLZZ59tfmxpv6+3VOPw4cOLrbbaapFlbrjhhqJTp07FnDlzlqixls4VV1zxfV+/nj17Ni9Tz3Oflmp8t1rPe8rqXGhpz33KbFza854yOutx7tOSjfU672nJznqe+5T157KW856W7KznuU9LNbaF856//OUvRVNTU/HKK680LzN79uyiUqk076fWPvZU0/hurXXsWdLOhco89ixtY9nHniXpbK1jT7WNrX3sqaaztY89S/PnsjWOPdV0tvaxp5rGeh97iuLf56FJirvuuqt5mx06dCiuvvrq5mUee+yxIkkxbty4oiiqe0/tO9/5TrHJJpsssq3999+/GDx4cJtpfLcddtih+OY3v7nEbWV3LrTxxhsXp59+eptu3HvvvYuvfOUrS9xYRuf+++9fnHzyyTW939pSjXfcccdSvxdYZudNN91UdO/evXjppZfabON7XXvttUWlUimeeeaZNtU5YsSI4mMf+9gi2/rlL39ZrLHGGm2mceDAgcUJJ5ywyLaOP/74Ytttt13ixqXtfLcP+rt7/vnnFyuvvPIifwZOOumkYoMNNmgzje926KGHFkOGDFnitrI7F9p9992Lww8/vE03/ud//mfx2c9+dokby+j8zne+U3zlK1+p6Zy3pRqnTZtW0xzE4rjiVonmzp2bJOnUqVPzY01NTenYsWPuvffeJMmLL76Y+++/P7169co222yT3r17Z4cddmh+Pvn3lVt69OixyE/X7Lzzzmlqasr999/fZjpbUks2vvLKK+nZs2eb7pw1a1Yuv/zybLPNNunQoUObaZw5c2aGDRuWSy+9NF26dKmpqyU7k+RHP/pRVllllWy55ZYZMWLEEt0WqKUbH3744Tz//PNpamrKlltumdVXXz277bZbJk2aVHNjPTvf64YbbshLL72Uww8/vM00rrLKKs2XoH399dfz9ttv5ze/+U169epV29RznTvnzp2bFVZYYZErhXXu3DlJ6vJ9tZrO9xo/fnwmTpyYI488svmxcePG5ZOf/GR69+7d/NjgwYMzZ86cTJ48uU00trSW7KzX8aelGl944YX84Q9/yA477FBzY707p0yZkjPOOCOjRo1a7JUg20Jjkhx77LFZddVVs/XWW+eiiy5KURRtqvOWW27JggUL8vzzz2ejjTbKmmuumf322y/PPfdcm2l8r1GjRqVLly5LdEWEMjo32GCDrLLKKrnwwgszb968vPnmm7nwwguz0UYbZZ111mkTjXPnzl3kNZJ/H3veeuutjB8/vqbGJencZpttctVVV2XWrFlZsGBBrrzyyrz11lsZNGhQkpY996lXY0tryc6yjz1L2ljP8556d7bUuU+992VLnPfUs7Mlz31a6s9lPc976tnZkuc+9WpsC+c9c+fOTaVSSceOHZuX6dSpU5qampqXae1jTzWNLa0lO8s89ixNY2sce6rtbM1jz5Lsy9Y89lTT2drHnqX5c9kax55qOlv72FNNY0sce1555ZUkaf5eNn78+MyfP3+Rq4BsuOGG6devX8aNG5ekuvfUxo0b974riQwePLj5NdpCY72V1blgwYK8+uqrS3X8KatxwoQJue+++5b6fbeW7Bw5cmSefvrpqq/I0hqNSbLFFltk9dVXz+c///mMHTu2zXXecMMN2WqrrfLjH/84a6yxRtZff/2ccMIJefPNN9tM43tdeOGF2XnnnbP22msvcWNLdg4cODDPPfdc/vznP6coisycOTO///3vs/vuu7eZxg963+2BBx6o+rZ0tXZWY9y4cdl+++2zwgorLPK5TJ06NS+//HKbaKy3MjuX9tynrMYnn3wyN998c6nHnmrdfvvtufrqqxd7Zda20pgke+21V3r16pXPfvazueGGG2pqNbhVooVf9OHDh+fll1/OvHnz8t///d/5xz/+kenTpydJnn766STJaaedlmHDhuXmm2/Opz71qey0007N92+fMWPG+y7x2b59+/Ts2bPqW3+V0dmSWqrxySefzDnnnJOjjjqqTXaedNJJWXHFFbPKKqvk2WefzfXXX99mGouiyGGHHZajjz666kt2t0Zn8u/70l555ZW54447ctRRR+W//uu/8p3vfKfNNL57mZNPPjk33nhjVl555QwaNCizZs1qM53vdeGFF2bw4MFZc80120xjpVLJrbfemgkTJqRr167p1KlTfvazn+Xmm2/Oyiuv3GY6P/e5z2XGjBkZMWJE5s2bl5dffrn5VlULX6elO99r4YDBNtts0/zYjBkzFjkZSdL8+1qPP/VqbGkt1XnfffflqquuWqLbHpfVeOCBB6ZLly5ZY4010q1bt/zud7+rubGenXPnzs2BBx6YESNGpF+/fnVpq3dj8u/bhYwZMya33HJLvvSlL+WYY47JOeec06Y6n3766SxYsCD/9V//lZ///Of5/e9/n1mzZuXzn/985s2b1yYaF7fMQQcd1PzGe63q1dm1a9fceeedueyyy9K5c+estNJKufnmm3PTTTelffv2baJx8ODBue+++3LFFVfknXfeyfPPP58zzjgjSbnHnjFjxmT+/PlZZZVV0rFjxxx11FG59tprs9566yVp2XOfejW2tJbqrOe5T70bW+K8p56dLXnuU8992VLnPfXsbMlzn5b6u1PP8556drbkuU+9GtvCec9nPvOZrLjiijnppJPyxhtv5PXXX88JJ5yQd955p3mZ1j72VNPY0lqqs+xjz5I0tuaxp5rO1j72VLsvW/vYU01nax97lubvTmsce6rpbO1jTzWN9T72LFiwIN/61rey7bbbZtNNN03y7+PGCiuskB49eiyybO/evZuPG9W8p/ZBy8yZM2eJBjtasrGeyuz8yU9+ktdeey377bdfm2tcc80107Fjx2y11VY59thj89WvfnWJGlu684knnsh3v/vdXHbZZTW9n9GSjauvvnp+/etf55prrsk111yTtdZaK4MGDcrDDz/cpjqffvrp3HvvvZk0aVKuvfba5vfejjnmmDbT+G4vvPBCbrrppqX6M9nSndtuu20uv/zy7L///llhhRXSp0+fdO/efYkHPFqycfDgwfnd736X8ePHpyiKPPTQQ/nd736X+fPn51//+lcpndWo1/f+lmyspzI7x4wZkwcffHCJB+/LaNxmm23SqVOnfOITn8h2223X/J5wW+l86aWXcthhh+Xiiy9Ot27dlritjMaVVlopP/3pT3P11VfnT3/6Uz772c/mi1/8Yk3DWwa3StShQ4f84Q9/yOOPP56ePXumS5cuueOOO7Lbbrs1/8THwnuvH3XUUTn88MOz5ZZb5uyzz84GG2yQiy66SGcLNj7//PPZdddd8+Uvf7mq+yC3RueJJ56YCRMm5K9//WvatWuXoUOH1ny1jno1nnPOOXn11VczfPjwmnpaujNJjj/++AwaNCibbbZZjj766Pz0pz/NOeec0/yTXK3duHCZ73//+/nSl76U/v37Z+TIkalUKrn66qtraqxn57v94x//yF/+8pe6XfmoXo1FUeTYY49Nr169cs899+SBBx7IF7/4xey55551ecO7Xp2bbLJJLrnkkvz0pz9Nly5d0qdPn6y77rrp3bt3Xa4eVE3nu7355psZPXp0qVeyaoTGluqcNGlShgwZklNPPTW77LJLm2s8++yz8/DDD+f666/PU089leOPP77mxnp2Dh8+PBtttFG+8pWv1KWrJRqT5Ac/+EG23XbbbLnlljnppJPyne98JyNGjGhTnQsWLMj8+fPzy1/+MoMHD85nPvOZXHHFFXniiSdyxx13tInGdxs3blwee+yxun4fqFfnm2++mSOPPDLbbrtt/va3v2Xs2LHZdNNNs8ceeyzVT1K2ROMuu+ySESNG5Oijj07Hjh2z/vrrN/9kYpnHnh/84AeZPXt2br311jz00EM5/vjjs99+++XRRx+tuWFZaGypznqf+9S7sSXOe+rZ2ZLnPvXcly113lPPzpY892mJvzv1Pu+pZ2dLnvvUq7EtnPesttpqufrqq/PHP/4xK620Urp3757Zs2fnU5/6VF2v3NrIjS3V2RrHniVpbM1jTzWdrX3sqXZftvaxp5rO1j72LOnfndY69lTT2drHnmoa633sOfbYYzNp0qRceeWVNX1+LakRGpPyOkePHp3TTz89Y8aMed9g9kcpo/Gee+7JQw89lF//+tf5+c9/niuuuGKJX6OlOt95550cdNBBOf3007P++uvX9FotuS832GCDHHXUUenfv3+22WabXHTRRdlmm21y9tlnt6nOBQsWpFKp5PLLL8/WW2+d3XffPT/72c9yySWXLNF7RWX93bnkkkvSo0ePfPGLX1yq9Vuyc8qUKfnmN7+ZU045JePHj8/NN9+cZ555JkcffXSbafzBD36Q3XbbLZ/5zGfSoUOHDBkyJIceemiSJX/frRG+rzdCY1Je5x133JHDDz88v/3tb7PJJpss0bplNF511VV5+OGHM3r06PzpT3/KT37ykyV+jZbsHDZsWA466KBsv/32Nb1OSzauuuqqOf744zNgwIB8+tOfzo9+9KN85Stfqe3/fOp200XeJ++5L/u7zZ49u3jxxReLoiiKrbfeujjmmGOKoiiKp59+ukhSXHrppYssv99++xUHHXRQURRFceGFFxY9evRY5Pn58+cX7dq1K/7whz+0mc53q+Xeo2U0Pv/888UnPvGJ4pBDDlnkfvdtrfPdnnvuuSJJcd9997WJxiFDhhRNTU1Fu3btmj+SFO3atSuGDh26RI0t2bk4kyZNKpIU//M//9MmGm+//fYiSXHPPfcssszWW29dfO9731uixpbsfLczzjijWG211Yp58+YtcV9LNt56661FU1NT8corryyyzHrrrVf88Ic/bDOd7zZjxozi1VdfLV577bWiqampGDNmTCmd7zZq1KiiQ4cOzcst9IMf/OB993Je+Pk9/PDDbaLx3ZbkPt6t1Tl58uSiV69eS/V3u6zGd7vnnnuKJMULL7zQZjo333zzRY4/TU1NzcefU045pU00Ls6NN95YJCneeuutJWpsyc6LLrqoSFI899xzizzeq1ev4oILLmgTje92xBFHFFtsscUSdZXV+bvf/a7o1avXIv+unDt3btGlS5fiiiuuaBONCy1YsKB4/vnnizfeeKOYMmVKkaR44IEHlqhxaTuffPLJIkkxadKkRZbfaaediqOOOqooivqe+7RU47vVet5TRmc9zn3K2JcLLe15T0t21vPcp8x9ubTnPS3ZWc9znzL2Za3nPS3ZWc9znzL2ZVs47/nnP/9ZvPzyy0VRFEXv3r2LH//4x0VRtP6xp5rGd2utY8+SdLbWsWdJGt+t7GNPNZ2tfeyppnFxyj72VNPZ2seeahrfrbWOPdV0tvaxp5rGd6v12HPssccWa665ZvH0008v8vhtt91WJGne/kL9+vUrfvaznxVFUd17atttt13xzW9+c5FlLrrooqJbt25tpvHddthhh/f1trXOK664oujcuXNx4403ttnGdzvzzDOL9ddfv810vvzyy83HmoUflUql+bHbbrut1Rs/yAknnFB85jOfqaqvrM6hQ4cWH//4xxdZZuH7MI8//nibaFxowYIFxXrrrVd861vfqqqr7M6vfOUrxb777rvIMkv6vnVZ+3LevHnFc889V7z99tvF+eefX3Tt2nWJ/j1cS+e7fdD/lRxyyCHFkCFDFnls4b+VZs2a1SYa3+3QQw99X2+1yuq88847ixVXXLH4zW9+02Yb3+3SSy8tOnfuXLz99tttprN79+6LHHve/X8+F154YZtoXJxzzz236NOnT1XLLo4rbrWS7t27Z7XVVssTTzyRhx56KEOGDEmSrLPOOunbt2+mTp26yPKPP/548z2EBw4cmNmzZ2f8+PHNz99+++1ZsGBBBgwY0GY6y1Jr4/PPP59BgwY1/3RVS/30Yr335cKfDqvHT6zVo/GXv/xl/v73v2fixImZOHFi/vznPyf599TuWWedVbfGWjsXZ+LEiWlqalrin7hpqcb+/funY8eOiywzf/78PPPMM3X/+1WPfVkURUaOHJmhQ4emQ4cOde2rtfGNN95I8v6fYGhqamr+O9QWOt+td+/eWWmllXLVVVelU6dO+fznP19K57tdeOGF2WuvvbLaaqst8vjAgQPz6KOP5sUXX2x+7JZbbkm3bt2y8cYbt4nGMtXaOXny5Oy444459NBD6/59sl6N79USx55aO6+55ppFjj8Lb+V4zz335Nhjj20TjYszceLErLzyyunYsWPdGmvt3HbbbZNkke9Xs2bNyr/+9a+6Hn/qsS9fe+21jBkzpkWvuldL5xtvvJGmpqZUKpXmxxb+vp7Hn3rsy0qlkr59+6Zz58654oorstZaa+VTn/pU3Ro/rPODjtPt2rVr3k9lnfvU0limWjvLOPep974s+9hTTWdZ5z713pctcd5Ta2dZ5z712Jctfd5Ta2dZ5z71+nPZFs57Vl111fTo0SO33357Xnzxxey1115JWv/YU01jmWrtbM1jT7WN79Wa5z0f1Nnax55qGhen7GNPNZ2tfeyppnGh1jz2VNPZ2seeahrfbWmPPUVR5Ljjjsu1116b22+/Peuuu+4iz/fv3z8dOnTIbbfd1vzY1KlT8+yzz2bgwIFJqntPbeDAgYu8xsJlFr5GW2isVZmdV1xxRQ4//PBcccUV2WOPPdpk43stWLCg6mNPGZ3dunXLo48+2nzsmThxYo4++uhssMEGmThx4kf+u6g19+XEiROz+uqrf2hf2Z3bbrttXnjhhbz22mvNyzz++ONpamr6yFvhlr0v77rrrjz55JNL/L5bWZ0L33d7t3bt2jU3tIXGhTp06JA111wz7dq1y5VXXpkvfOELVf17uB6d1Rg4cGDuvvvuzJ8/f5HPZYMNNvjI2x6X1VirMjvvvPPO7LHHHvnv//7vfO1rX2uTje+18C4c1fzbrazOcePGLXLsOeOMM9K1a9dMnDgxe++9d5toXJwlOfYs1lKPfLFYr776ajFhwoRiwoQJRZLiZz/7WTFhwoTif//3f4uiKIoxY8YUd9xxR/HUU08V1113XbH22msX++yzzyKvcfbZZxfdunUrrr766uKJJ54oTj755KJTp07Fk08+2bzMrrvuWmy55ZbF/fffX9x7773FJz7xieLAAw9sc53/+7//W0yYMKE4/fTTi5VWWql5m6+++mqbaPzHP/5RrLfeesVOO+1U/OMf/yimT5/e/NGW9uXf/va34pxzzikmTJhQPPPMM8Vtt91WbLPNNsXHP/7xqq7UUdbX+92mTZtWJCkmTJjQpvblfffdV5x99tnFxIkTi6eeeqq47LLLitVWW63qn04sa19+85vfLNZYY43iL3/5S/E///M/xZFHHln06tWr6gn3Mr/mt956a5GkeOyxx6pqK7Pxn//8Z7HKKqsU++yzTzFx4sRi6tSpxQknnFB06NChmDhxYpvpLIqiOOecc4rx48cXU6dOLc4999yic+fOxS9+8YtS92dRFMUTTzxRVCqV4qabbnrfc2+//Xax6aabFrvssksxceLE4uabby5WW221Yvjw4W2mceHzEyZMKI466qhi/fXXb97m3Llz20zno48+Wqy22mrFV77ylUWOPdVcqamsxj/96U/FRRddVDz66KPFtGnTihtvvLHYaKONim233baqxrI63+uOO+5Y7E9MtGbjDTfcUPz2t78tHn300eKJJ54ozj///KJLly5LdEWwsvblkCFDik022aQYO3Zs8eijjxZf+MIXio033riqn+4u8+v9u9/9rujUqVPVX+eyOx977LGiY8eOxde//vViypQpxaRJk4qvfOUrRffu3av6yb+y9uWPf/zj4pFHHikmTZpUnHHGGUWHDh0+8KfcW6Jz3rx5xXrrrVdst912xf333188+eSTxU9+8pOiUqkUf/rTn5qXq+Xcp6zGWs57yuqs9dynjMZaz3vK6nyvJT33KaOx1vOeMvdlLec+ZX69l/a8p6zOWs99ytqXbeG856KLLirGjRtXPPnkk8Wll15a9OzZszj++OMXWaY1jz3VNrb2saeaztY+9lTT2BaOPdV0vlfZx55qGtvCsaeazqJo3WNPtY1F0brHnmo6W/vYU+2+rPXY8/Wvf73o3r17ceeddy7yfeyNN95oXuboo48u+vXrV9x+++3FQw89VAwcOLAYOHBg8/PVvKf29NNPF126dClOPPHE4rHHHivOO++8ol27dsXNN9/cZhqLomj+mvXv37846KCDigkTJhSTJ09uU/vy8ssvL9q3b1+cd955i2xn9uzZbabx3HPPLW644Ybi8ccfLx5//PHid7/7XdG1a9fi+9//fpval++1JFceKavx7LPPLq677rriiSeeKB599NHim9/8ZtHU1FTceuutbarz1VdfLdZcc81i3333LSZPnlzcddddxSc+8Yniq1/9aptpXOgrX/lKMWDAgKr2X2t0jhw5smjfvn1x/vnnF0899VRx7733FltttVWx9dZbt5nGqVOnFpdeemnx+OOPF/fff3+x//77Fz179iymTZtW2r4sio/+v5LZs2cXvXv3Lg455JBi0qRJxZVXXll06dKlqqtFldVYFP++c8mECROKPffcsxg0aFDzMm1pX95+++1Fly5diuHDhy+ynZdeeqnNNF522WXFVVddVUyZMqV46qmniquuuqro27dvcfDBB7epffleS3KV6bIaL7744mL06NHFY489Vjz22GPFWWedVTQ1NRUXXXRRVZ2LY3Crzhb+Z+F7Pw499NCiKIriF7/4RbHmmmsWHTp0KPr161ecfPLJi/1D+MMf/rBYc801iy5duhQDBw5836WbX3rppeLAAw8sVlpppaJbt27F4YcfXvUbM2V2HnrooYvdzh133NEmGkeOHLnYbSzJTGMZnY888kix4447Fj179iw6duxYrLPOOsXRRx9d/OMf/2gzje+1NINbZXSOHz++GDBgQNG9e/eiU6dOxUYbbVT813/9V9VvxpW1L+fNm1d8+9vfLnr16lV07dq12Hnnnd93y4m20FkURXHggQcW22yzTdVtZTc++OCDxS677FL07Nmz6Nq1a/GZz3ym+POf/9zmOg855JCiZ8+exQorrFBsttlmxahRo6purGfn8OHDi7XWWusDL9f7zDPPFLvttlvRuXPnYtVVVy2+/e1vF/Pnz29TjTvssMNit1PtSVEZnaeeeupit7H22mu3mcbbb7+9GDhwYPP3y0984hPFSSedtESDMmV9zRe3zWo7y2i86aabii222KJYaaWVihVXXLHYfPPNi1//+tdLdFnssvblK6+8UhxxxBFFjx49ip49exZ777138eyzz7apxqIoioEDB37obZDbQudf//rXYtttty26d+9erLzyysXnPve5Yty4cW2qcccdd2z+Oz5gwIAlOj7Wq/Pxxx8v9tlnn6JXr15Fly5dFnsMrOXcp6zGWs57yuqs9dynjMZaz3vK6nyvJT33KaOx1vOesjqLorZznzK/3kt73lNmZy3nPmU1toXznpNOOqno3bt30aFDh+ITn/hE8dOf/rRYsGDBIsu09rGnmsa2cOz5qM62cOz5qMa2cuyp5mv+bq1x7PmoxrZy7KlmX7b2safar3drH3uq6WztY081jbUeez7o+9jIkSObl3nzzTeLY445plh55ZWLLl26FHvvvff7hlSreU/tjjvuKLbYYotihRVWKD72sY8tso220ri47VT7flZZnR/03uDCP1ttofGXv/xlsckmmxRdunQpunXrVmy55ZbF+eefX/V7RWV+zd9tSQa3ymr87//+7+LjH/940alTp6Jnz57FoEGDittvv72qxjI7i+LfP+i38847F507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"/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="Answers">Answers<a class="anchor-link" href="#Answers">¶</a></h3><ol>
<li>Top two most popular genres are Drama and Comedy</li>
<li>Drama has been most popular generally from year to year</li>
</ol>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="Question-2-:-How-did-film-budgets-change-from-each-decade?">Question 2 : How did film budgets change from each decade?<a class="anchor-link" href="#Question-2-:-How-did-film-budgets-change-from-each-decade?">¶</a></h3>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [29]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#make a copy of the df1/cleaned df</span>
<span class="n">budget</span> <span class="o">=</span> <span class="n">df1</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [30]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">budget</span><span class="o">=</span><span class="n">budget</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s1">'decade'</span><span class="p">)[</span><span class="s1">'budget'</span><span class="p">]</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span><span class="o">.</span><span class="n">reset_index</span><span class="p">(</span><span class="n">name</span><span class="o">=</span><span class="s1">'budget'</span><span class="p">)</span>
<span class="n">budget</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[30]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>decade</th>
<th>budget</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>1960</td>
<td>2.202421e+06</td>
</tr>
<tr>
<th>1</th>
<td>1970</td>
<td>2.975516e+06</td>
</tr>
<tr>
<th>2</th>
<td>1980</td>
<td>7.598380e+06</td>
</tr>
<tr>
<th>3</th>
<td>1990</td>
<td>2.039298e+07</td>
</tr>
<tr>
<th>4</th>
<td>2000</td>
<td>2.222758e+07</td>
</tr>
<tr>
<th>5</th>
<td>2010</td>
<td>1.815299e+07</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [31]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#set figure size </span>
<span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span> <span class="o">=</span> <span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">5</span><span class="p">))</span>

<span class="c1">#use seaborn to lineplot average film budget per decade </span>
<span class="n">sns</span><span class="o">.</span><span class="n">barplot</span><span class="p">(</span><span class="n">x</span> <span class="o">=</span> <span class="s1">'decade'</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="s1">'budget'</span><span class="p">,</span> <span class="n">data</span> <span class="o">=</span> <span class="n">budget</span><span class="p">)</span>

<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">"Average Film Budget"</span><span class="p">,</span> <span class="n">fontsize</span> <span class="o">=</span> <span class="mi">30</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s2">"Decade"</span><span class="p">,</span> <span class="n">fontsize</span> <span class="o">=</span> <span class="mi">20</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s2">"$ millions"</span><span class="p">,</span> <span class="n">fontsize</span> <span class="o">=</span> <span class="mi">20</span><span class="p">)</span>


<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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+JaUlGQeffRRl97LevXqOb2XsbGxpkWLFi717d+/v0lKSvL4vUlPyvHcCd9iY2OdPgNsNpuJi4tzebycCN+OHDliatWq5dJ7XaFCBbNr164snWd//fWX6du3r0vj2Gw2M3nyZGNM1sI3Kz5LCd8AALfinm8AgELp5qWkNwUGBqp3795ObW69zNRut2v27Nnp7u+OO+5QvXr1HMsbNmzQ0aNH3app9uzZMsY4lgcNGpRu26tXr6p379764IMPZLfbnbaFhoaqcePGatq0aapL9C5fvqz77rtP8+bNc6s2SXrppZf0wQcfOJaLFy+uunXrqlmzZgoNDU2zz19//ZVqXcmSJVWnTh21aNFCTZs2VVhYWKo2e/fuVfv27XX27FmXatu3b5+6du3quCTtJm9vb9WqVUvNmzd3GufUqVPq2bOny/u/1a+//qo2bdro999/d1pfpEgR1axZUy1atFD9+vVTXeK4efNmtW7dWrGxsW6PWRg888wzTpeBlytXTk2bNlXDhg3l4+Pj1Hbfvn2O8/PatWvq3r27tmzZ4theuXJl3XHHHapTp47TPdQkaf78+Xr77bctPJKsmz59utNnQIsWLRQQEJCLFTk7ffq0unTpooMHDzqtv/mz37x5c6fLzk+fPq2ePXvqzJkzbo1jt9vVv39/p8/om8qXL6/mzZurbt26jp8LY4yef/55ff31124fU258lgIACqFcDv8AAMgVn376qdNsg8ceeyxVmwMHDji1qV27dob7fPvtt53av/HGG27VdOtsEi8vL3Pq1Kl024aHhzuN5e/vbyZMmGCOHDmSqu3OnTtN//79U83ayGxm2a3ty5Ur55gVUqtWLTNv3jxz7do1p/a7d+82hw8fdlr3zjvvGB8fHzNw4EAze/Zsc+zYsTTHOnfunPnoo49MhQoVnMa99957M6zRmBuzVpo2berUr0SJEubf//63+fPPP53aHjx40AwdOtTRrlq1am7NyImOjjbBwcFOfW6//XbzzTffmMuXLzu1vXbtmpk7d67TDEpJ5q677jJ2uz3T43JXfp75VrVqVce/u3fvbrZs2eLU/vLly+b1119PdXnv0qVLzYgRIxznzFNPPZVq9taJEyfM/fff79SvePHibl2C7Y5bx5EbM9++/vprU6xYMae+3333nVvjWT3zrWfPnk7tixUrZl577bVU72VkZKTT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1/PPP69PPvlEklw+p3Pys/S2225z/NsYowULFrg1BgAg/yN8y4L4+Hg1atRIU6dOzVL/MWPGKDo62ulVv379XH2EPAAUVPPnz3cKYWrUqJHqPmHuShnepZxZdysvLy89+uijjuVr167plVdecWrj6iWnt44/YsQIx3JiYqKGDx+uO++8U0uXLlV8fHyqPomJifr999/17rvvqn379qpbt64+/fRTt4Mud4SHhzstjx8/XmPGjEk1U/DcuXOaPHmymjdvruPHj8tms7l1j7j69etrwoQJTuu+/PJL1alTR2PGjNGcOXO0bNkyzZo1S+Hh4WrYsKHji/yt76MrZs+e7RSm7t+/X82aNdOoUaPSvdn7hQsXtHLlSj333HOqWrWq+vbtq19//dWtcZF/bdy4UStXrkzztXjxYn344Yd65JFHVKVKlVT3IGzQoIHGjRuX4f7vuusuVaxY0bF8+vRpdezY0XFfy5uSkpK0YsUKtWvXznG5fMoHiWTkb3/7m9MTQRMSEtSzZ0+9/vrrqcK+vXv3qn///nrrrbck3Xj6s6tsNpumT5/udO+3o0eP6o477lD//v316aef6ocfftC3336rCRMmqG7duvrvf/8r6calpJUrV3brmHLis7R79+5Oy08++aSefvppffPNN/rpp5+cfib27t3rcv0AgHzEwCOSzMKFC53W/fXXX+b55583FSpUMH5+fqZFixZmzZo16e5j586dRpJZv369tcUCQCHUpUsXI8nxeumllzze55UrV4yfn5/Tfn/77bd02+/fv9+p7a2vli1bZqmG69evm4EDB6a5T29vb1OjRg1zxx13mCZNmphq1aqZYsWKpdk2Kioq3TFubdexY8cs1di4ceNUY3p5eZk6deqYli1bmpo1a5oiRYqk+m80aNAgl+s0xhi73W4ef/zxdN/ntF5PP/20WbNmjdO6N998M9Pj2rVrlwkLC0tzn4GBgaZ+/fqmZcuW5rbbbjPly5dPs11W3s/MdOzY0WmMmTNnerxPd2qeOHGiU/uM/vaJiopyajto0CCXa5o5c2aWj9Pdn6uscOdnMKNXgwYNTExMjEtjzp8/P819BAcHm+bNm5uGDRuakiVLOm178cUX3X4/Tpw4YapUqZLmZ06tWrXMHXfcYSpVquS0rWLFimbOnDlO6yZOnJjpMf3888/G19fX5ferRo0a5uzZ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5cqVU0BAgAYOHKgzZ844teEcQF42adIk3XHHHSpZsqSCg4PVp08f7d+/36nNX3/9paeeekplypSRv7+/+vXrl+rn3JW/edauXaumTZvKx8dHNWvW1KxZs6w+PCBT2XUOPPPMM2rWrJl8fHzUuHHjNMfatWuX2rdvL19fX4WFhenf//63VYeFNBC+IUfFx8erUaNGmjp1aqptxhj16dNHR44c0eLFi7Vjxw5VqVJFXbt2VXx8vKNdRESEevbsqe7du2vLli3aunWrRo4cKS+v//txfvjhh7Vnzx6tWLFCS5cu1fr16zV8+PAcOUYgM56eB2FhYYqOjnZ6vf766/L391evXr0kScnJybr77rt1/fp1bdq0SZ9//rlmzZqlV199NUePFUhPdvw+CA8P1/79+/X9999r9+7duv/++zVw4EDt2LHD0YbfB8irPD0H4uPj1b17d9lsNq1evVobN27U9evXdc8998hutzv2xTmAvGzdunV66qmntHnzZq1YsUKJiYnq3r2702f9c889pyVLlmjevHlat26dTp8+rfvvv9+x3ZW/eaKionT33Xerc+fO2rlzp0aNGqXHH39cP/30U44eL5BSdpwDNw0dOlQPPPBAmuNcunRJ3bt3V5UqVbR9+3a98847eu211zRt2jTLjg0pGCCXSDILFy50LO/fv99IMpGRkY51ycnJply5cubTTz91rGvZsqV55ZVX0t3v3r17jSSzdetWx7off/zR2Gw2c+rUqew9CMBDWT0PUmrcuLEZOnSoY3nZsmXGy8vLxMTEONZ99NFHJiAgwCQkJGTvQQAeyup5UKJECTN79mynfZUuXdrRht8HyC+ycg789NNPxsvLy8TFxTnaXLx40dhsNrNixQpjDOcA8p+zZ88aSWbdunXGmBs/00WLFjXz5s1ztNm3b5+RZCIiIowxrv3NM27cOHPbbbc5jfXAAw+YHj16WH1IgFuycg7cauLEiaZRo0ap1n/44YemVKlSTt8DXnjhBVOnTp3sPwikiZlvyDMSEhIkSb6+vo51Xl5e8vHx0S+//CJJOnv2rH799VcFBwerTZs2CgkJUceOHR3bpRsz44KCgtS8eXPHuq5du8rLy0u//vprDh0NkDWunAcpbd++XTt37tRjjz3mWBcREaGGDRsqJCTEsa5Hjx66dOmS9uzZY1H1QPZw9Txo06aN5s6dq/Pnz8tut2vOnDn666+/1KlTJ0n8PkD+5co5kJCQIJvNJh8fH0cbX19feXl5OdpwDiC/iYuLkySVLl1a0o2/cRITE9W1a1dHm7p166py5cqKiIiQ5NrfPBEREU77uNnm5j6AvCIr54ArIiIi1KFDBxUrVsyxrkePHtq/f78uXLiQTdUjI4RvyDNufoiMHz9eFy5c0PXr1/Wvf/1LJ0+eVHR0tCTpyJEjkqTXXntNw4YN0/Lly9W0aVPdeeedjvugxMTEKDg42Gnf3t7eKl26tGJiYnL2oAA3uXIepDRjxgzVq1dPbdq0cayLiYlx+iNUkmOZ8wB5navnwbfffqvExESVKVNGPj4+GjFihBYuXKiaNWtK4vcB8i9XzoFWrVqpRIkSeuGFF3T16lXFx8drzJgxSk5OdrThHEB+YrfbNWrUKLVt21YNGjSQdONnuFixYgoKCnJqGxIS4vgZduVvnvTaXLp0yem+0UBuyuo54Aq+G+Q+wjfkGUWLFtV3332nAwcOqHTp0vLz89OaNWvUq1cvx/3cbt7DZMSIERoyZIiaNGmiKVOmqE6dOvrss89ys3wgW7hyHtzq2rVr+vrrr51mvQH5navnwYQJE3Tx4kWtXLlS27Zt0+jRozVw4EDt3r07F6sHPOfKOVCuXDnNmzdPS5Yskb+/vwIDA3Xx4kU1bdo0zd8XQF731FNPKTIyUnPmzMntUoBcwTlQsHnndgHArZo1a6adO3cqLi5O169fV7ly5dSyZUvH5RLly5eXJNWvX9+pX7169XT8+HFJUmhoqM6ePeu0PSkpSefPn1doaGgOHAXgmczOg1vNnz9fV69eVXh4uNP60NBQbdmyxWndzacicR4gP8jsPDh8+LA++OADRUZG6rbbbpMkNWrUSBs2bNDUqVP18ccf8/sA+Zorvwu6d++uw4cP69y5c/L29lZQUJBCQ0NVvXp1SfxNhPxj5MiRjgeCVKpUybE+NDRU169f18WLF51m/pw5c8bxM+zK3zyhoaGpng555swZBQQEqHjx4lYcEuAWT84BV6R3DtzcBuvxv8WQJwUGBqpcuXI6ePCgtm3bpvvuu0+SVLVqVVWoUCHV45cPHDigKlWqSJJat26tixcvavv27Y7tq1evlt1uV8uWLXPuIAAPpXce3GrGjBm69957Va5cOaf1rVu31u7du52+dK1YsUIBAQGpwmsgL0vvPLh69aokpZrhU6RIEccsaX4foCBw5XdB2bJlFRQUpNWrV+vs2bO69957JXEOIO8zxmjkyJFauHChVq9erWrVqjltb9asmYoWLapVq1Y51u3fv1/Hjx9X69atJbn2N0/r1q2d9nGzzc19ALklO84BV7Ru3Vrr169XYmKiY92KFStUp04dlSpVyvMDQeZy+4kPKFwuX75sduzYYXbs2GEkmf/+979mx44d5tixY8YYY7799luzZs0ac/jwYbNo0SJTpUoVc//99zvtY8qUKSYgIMDMmzfPHDx40LzyyivG19fXHDp0yNGmZ8+epkmTJubXX381v/zyi6lVq5Z58MEHc/RYgfRkx3lgjDEHDx40NpvN/Pjjj6m2JSUlmQYNGpju3bubnTt3muXLl5ty5cqZ8ePHW358gCs8PQ+uX79uatasadq3b29+/fVXc+jQIfOf//zH2Gw288MPPzja8fsAeVV2/C747LPPTEREhDl06JD54osvTOnSpc3o0aOd2nAOIC978sknTWBgoFm7dq2Jjo52vK5evepo88QTT5jKlSub1atXm23btpnWrVub1q1bO7a78jfPkSNHjJ+fnxk7dqzZt2+fmTp1qilSpIhZvnx5jh4vkFJ2nAPG3PhesGPHDjNixAhTu3Ztx++Xm083vXjxogkJCTGPPvqoiYyMNHPmzDF+fn7mk08+ydHjLcwI35Cj1qxZYySleg0aNMgYY8x7771nKlWqZIoWLWoqV65sXnnlFafHId80adIkU6lSJePn52dat25tNmzY4LT9zz//NA8++KDx9/c3AQEBZsiQIeby5cs5cYhAprLrPBg/frwJCwszycnJaY5z9OhR06tXL1O8eHFTtmxZ8/zzz5vExEQrDw1wWXacBwcOHDD333+/CQ4ONn5+fub22283s2fPdmrD7wPkVdlxDrzwwgsmJCTEFC1a1NSqVctMnjzZ2O12pzacA8jL0joHJJmZM2c62ly7ds38/e9/N6VKlTJ+fn6mb9++Jjo62mk/rvzNs2bNGtO4cWNTrFgxU716dacxgNySXedAx44d09xPVFSUo83vv/9u2rVrZ3x8fEzFihXN22+/nUNHCWOMsRljjGXT6gAAAAAAAIBCjHu+AQAAAAAAABYhfAMAAAAAAAAsQvgGAAAAAAAAWITwDQAAAAAAALAI4RsAAAAAAABg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"/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="Answers">Answers<a class="anchor-link" href="#Answers">¶</a></h3><ol>
<li>1990s has the highest film budget on average while 1970s has the lowest</li>
<li>There is an increase in film production budget from 1970s to 1990s</li>
<li>There is a decrease in film production budget from 1990s to 2010s</li>
</ol>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="Question-3:-What-kinds-of-properties-are-associated-with-movies-that-have-high-revenues?">Question 3: What kinds of properties are associated with movies that have high revenues?<a class="anchor-link" href="#Question-3:-What-kinds-of-properties-are-associated-with-movies-that-have-high-revenues?">¶</a></h3>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [32]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#make a copy of the df1/cleaned df</span>
<span class="n">revenue</span> <span class="o">=</span> <span class="n">df1</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
<span class="n">revenue</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[32]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>popularity</th>
<th>budget</th>
<th>revenue</th>
<th>director</th>
<th>runtime</th>
<th>vote_count</th>
<th>vote_average</th>
<th>release_year</th>
<th>genre</th>
<th>decade</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>32.985763</td>
<td>150000000</td>
<td>1513528810</td>
<td>Colin Trevorrow</td>
<td>124</td>
<td>5562</td>
<td>6.5</td>
<td>2015</td>
<td>Action</td>
<td>2010</td>
</tr>
<tr>
<th>0</th>
<td>32.985763</td>
<td>150000000</td>
<td>1513528810</td>
<td>Colin Trevorrow</td>
<td>124</td>
<td>5562</td>
<td>6.5</td>
<td>2015</td>
<td>Adventure</td>
<td>2010</td>
</tr>
<tr>
<th>0</th>
<td>32.985763</td>
<td>150000000</td>
<td>1513528810</td>
<td>Colin Trevorrow</td>
<td>124</td>
<td>5562</td>
<td>6.5</td>
<td>2015</td>
<td>Science Fiction</td>
<td>2010</td>
</tr>
<tr>
<th>0</th>
<td>32.985763</td>
<td>150000000</td>
<td>1513528810</td>
<td>Colin Trevorrow</td>
<td>124</td>
<td>5562</td>
<td>6.5</td>
<td>2015</td>
<td>Thriller</td>
<td>2010</td>
</tr>
<tr>
<th>1</th>
<td>28.419936</td>
<td>150000000</td>
<td>378436354</td>
<td>George Miller</td>
<td>120</td>
<td>6185</td>
<td>7.1</td>
<td>2015</td>
<td>Action</td>
<td>2010</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [33]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#makeing new df where it's sorted by decreasing revenue</span>
<span class="n">high_revenue</span> <span class="o">=</span> <span class="n">revenue</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">by</span> <span class="o">=</span> <span class="p">[</span><span class="s1">'revenue'</span><span class="p">],</span> <span class="n">ascending</span> <span class="o">=</span> <span class="p">[</span><span class="kc">False</span><span class="p">])</span>
<span class="n">high_revenue</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[33]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>popularity</th>
<th>budget</th>
<th>revenue</th>
<th>director</th>
<th>runtime</th>
<th>vote_count</th>
<th>vote_average</th>
<th>release_year</th>
<th>genre</th>
<th>decade</th>
</tr>
</thead>
<tbody>
<tr>
<th>1386</th>
<td>9.432768</td>
<td>237000000</td>
<td>2781505847</td>
<td>James Cameron</td>
<td>162</td>
<td>8458</td>
<td>7.1</td>
<td>2009</td>
<td>Action</td>
<td>2000</td>
</tr>
<tr>
<th>1386</th>
<td>9.432768</td>
<td>237000000</td>
<td>2781505847</td>
<td>James Cameron</td>
<td>162</td>
<td>8458</td>
<td>7.1</td>
<td>2009</td>
<td>Adventure</td>
<td>2000</td>
</tr>
<tr>
<th>1386</th>
<td>9.432768</td>
<td>237000000</td>
<td>2781505847</td>
<td>James Cameron</td>
<td>162</td>
<td>8458</td>
<td>7.1</td>
<td>2009</td>
<td>Fantasy</td>
<td>2000</td>
</tr>
<tr>
<th>1386</th>
<td>9.432768</td>
<td>237000000</td>
<td>2781505847</td>
<td>James Cameron</td>
<td>162</td>
<td>8458</td>
<td>7.1</td>
<td>2009</td>
<td>Science Fiction</td>
<td>2000</td>
</tr>
<tr>
<th>3</th>
<td>11.173104</td>
<td>200000000</td>
<td>2068178225</td>
<td>J.J. Abrams</td>
<td>136</td>
<td>5292</td>
<td>7.5</td>
<td>2015</td>
<td>Action</td>
<td>2010</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [34]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#use panda corr function to see correlation of the high_revenue df </span>
<span class="n">high_rev_corr</span><span class="o">=</span><span class="n">high_revenue</span><span class="o">.</span><span class="n">corr</span><span class="p">(</span><span class="n">numeric_only</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">high_rev_corr</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[34]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>popularity</th>
<th>budget</th>
<th>revenue</th>
<th>runtime</th>
<th>vote_count</th>
<th>vote_average</th>
<th>release_year</th>
</tr>
</thead>
<tbody>
<tr>
<th>popularity</th>
<td>1.000000</td>
<td>0.541758</td>
<td>0.665801</td>
<td>0.142398</td>
<td>0.794882</td>
<td>0.233379</td>
<td>0.110153</td>
</tr>
<tr>
<th>budget</th>
<td>0.541758</td>
<td>1.000000</td>
<td>0.729429</td>
<td>0.201128</td>
<td>0.641743</td>
<td>0.101052</td>
<td>0.147880</td>
</tr>
<tr>
<th>revenue</th>
<td>0.665801</td>
<td>0.729429</td>
<td>1.000000</td>
<td>0.171686</td>
<td>0.798649</td>
<td>0.195299</td>
<td>0.081189</td>
</tr>
<tr>
<th>runtime</th>
<td>0.142398</td>
<td>0.201128</td>
<td>0.171686</td>
<td>1.000000</td>
<td>0.174363</td>
<td>0.158572</td>
<td>-0.135148</td>
</tr>
<tr>
<th>vote_count</th>
<td>0.794882</td>
<td>0.641743</td>
<td>0.798649</td>
<td>0.174363</td>
<td>1.000000</td>
<td>0.279316</td>
<td>0.131383</td>
</tr>
<tr>
<th>vote_average</th>
<td>0.233379</td>
<td>0.101052</td>
<td>0.195299</td>
<td>0.158572</td>
<td>0.279316</td>
<td>1.000000</td>
<td>-0.125364</td>
</tr>
<tr>
<th>release_year</th>
<td>0.110153</td>
<td>0.147880</td>
<td>0.081189</td>
<td>-0.135148</td>
<td>0.131383</td>
<td>-0.125364</td>
<td>1.000000</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [35]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#use seaborn to visualize the correlation above </span>
<span class="n">sns</span><span class="o">.</span><span class="n">heatmap</span><span class="p">(</span><span class="n">high_rev_corr</span><span class="p">,</span> <span class="n">xticklabels</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">annot</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">cmap</span><span class="o">=</span><span class="s1">'Greens'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">'Correlation Heatmap'</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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"/>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [38]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#vote count has highest correlation of 0.8</span>
<span class="n">sns</span><span class="o">.</span><span class="n">relplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s1">'vote_count'</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="s1">'revenue'</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">high_rev_corr</span><span class="p">,</span> <span class="n">kind</span><span class="o">=</span><span class="s2">"scatter"</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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x1RdXa3Vq1ersLBQS5cu1dq1ayM9IwAALVZYZ9TDhg3TmjVrtHHjRrVu3VqTJk3S7t27tWbNGt12222RnhEAgBYrrG8mi2V8MxkAIJaEdUb9wAMPaNOmTREeBQAAfFtYoT558qRuv/12paWl6cknn9SuXbsiPBYAAJDCDPXbb7+t48ePa+LEifq///s/9evXTz169NC0adN0+PDhCI8IAEDLFZH3qL/44gu98cYbWrx4sfbt26dz585FYrZGwXvUAIBYcsm/lKOyslLbt2/Xn//8Zx0+fFgpKSmRmAsAAOgSQv3hhx/qwQcfVEpKiu6991653W6tXbtWX3zxRSTnAwCgRQvrC086d+6sU6dO6fbbb9f8+fM1dOhQuVyuSM8GAECLF1aon3nmGf30pz9Vu3btIjwOAAD4Z5f0YbL9+/frwIEDysnJUVJSkowxcjgckZwv4vgwGQAgloT1HvVXX32lW2+9Vd26ddOQIUN0/PhxSdL999+vJ554IqIDAgDQkoUV6scff1wJCQk6cuSIkpOTg8tHjBihDRs2RGw4AABaurDeo37vvff07rvv6oorrghZnpGRoc8//zwigwEAgDDPqM+cORNyJn3eqVOn+PQ3AAARFFaob7zxRi1dujT4s8PhUHV1tV588UXdfPPNERsOAICWLqyXvl966SXdcsst2r59uwKBgJ566il9+umnOnXqlD766KNIzwgAQIvV4FBXVlbqV7/6ldasWaP3339fbdu2VVlZme68806NHTtWqampjTEnAAAtUljXUV9++eX605/+pIyMjMaYqVFxHTUAIJaE9R71L37xCy1atCjSswAAgG8J6z3qc+fOafHixdq4caP69eun1q1bh6yfNWtWRIYDAKClCyvUf/vb39S3b19J0t69e0PW2f4VogAAxJJL+q7vWMR71ACAWBL276MGAACNj1ADAGAxQg0AgMUINQAAFiPUAABYjFADAGAxQg0AgMUINQAAFiPUAABYjFADAGAxQg0AgMUINQAAFiPUAABYjFADAGAxQg0AgMUINQAAFiPUAABYjFADAGAxQg0AgMUINQAAFiPUAABYjFADAGAxQg0AgMUINQAAFrMi1HPnzlV6eroSExOVlZWlbdu2XdR+y5cvl8Ph0E9+8pPGHRAAgCiJeqhXrFihvLw8TZ48WR9//LF69eqlwYMH68SJE3Xu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lpjPPvvMPPTQQ6Zdu3amqKjIGGPMqFGjzPjx44Pbz5gxwzidTrNy5Upz/Pjx4K20tDRaT8FqDT2+38anvuvW0ON75MgR07ZtW/Poo4+awsJCs3btWtOhQwfz3HPPRespWKuhx3by5Mmmbdu25o033jAHDx407733nrn66qvNz372s2g9BauVlpaanTt3mp07dxpJZtasWWbnzp3m888/N8YYM378eDNq1Kjg9ucvz3ryySfN7t27zdy5c7k8qyV5+eWXzZVXXmmcTqcZMGCA+d///d/guptuusmMHj06+PNVV11lJNW4TZ48uekHjxENOb7fRqjr19Dj+6c//clkZWUZl8tlunTpYp5//nlz7ty5Jp46NjTk2FZWVppnnnnGXH311SYxMdGkpaWZX/7yl+brr79u+sFjwIcffljr36Xnj+no0aPNTTfdVGOf3r17G6fTabp06WJee+21iM/Fr7kEAMBivEcNAIDFCDUAABYj1AAAWIxQAwBgMUINAIDFCDUAABYj1AAAWIxQAwBgMUINAIDFCDXQAjgcDr311lvRHiPilixZonbt2kV7DKBREWoAACxGqAHLzZ8/X506dQr5NZCSNGzYMN13332SpFdffVVXX321nE6nrrnmGv3hD38Ibpeeni5J+pd/+Rc5HI7gz5L09ttvq2/fvkpMTFSXLl00ZcoUnTt37qLmOn36tP7t3/5NKSkpSkxMVM+ePbV27drg+lWrVqlHjx5yuVxKT0/XzJkzQ/av7Sy/Xbt2WrJkiSTp8OHDcjgcWr16tW6++WYlJyerV69eKigokCRt2rRJY8aMkc/nk8PhkMPh0DPPPHNRswMxJeK/5gNARJ06dco4nU6zcePG4LKvvvoquGz16tUmISHBzJ071xQWFpqZM2ea+Ph488EHHxhjjDlx4oSRZF577TVz/Phxc+LECWOMMZs3bzZut9ssWbLEHDhwwLz33nsmPT3dPPPMM/XOVFVVZb73ve+ZHj16mPfee88cOHDArFmzxqxfv94YY8z27dtNXFycefbZZ01hYaF57bXXTFJSUshvFpJk3nzzzZD79Xg8wW0OHTpkJJlrr73WrF271hQWFpq77rrLXHXVVaaystJUVFSY2bNnG7fbza92RbNGqIEYMGzYMHPfffcFf/6v//ov06lTJ1NVVWUGDhxoHnzwwZDtf/rTn5ohQ4YEf64tirfeequZNm1ayLI//OEPJjU1td553n33XRMXF2cKCwtrXX/33Xeb2267LWTZk08+abp3717nTLWFeuHChcH1n376qZFkdu/ebYwx5rXXXjMej6feeYFYxkvfQAwYOXKkVq1apYqKCknSsmXL9K//+q+Ki4vT7t27NWjQoJDtBw0apN27d9d5n3/5y1/07LPPqk2bNsHbgw8+qOPHj6u8vLzOfXft2qUrrrhC3bp1q3X9hWbat2+fqqqq6nu6ITIzM4P/OzU1VZJ04sSJBt0HEMtaRXsAAPUbOnSojDFat26d+vfvry1btuj3v//9Jd1nWVmZpkyZojvvvLPGusTExDr3TUpKuqTHlv7+HrUxJmRZZWVlje0SEhJC9pFU4/16oDkj1EAMSExM1J133qlly5Zp//79uuaaa9S3b19J0nXXXaePPvpIo0ePDm7/0UcfqXv37sGfExISapzJ9u3bV4WFheratWuD58nMzNQXX3yhvXv31npWfX6mf/bRRx+pW7duio+PlyRdfvnlOn78eHD9vn376j2T/zan09ngM3Qg1hBqIEaMHDlSP/7xj/Xpp5/qF7/4RXD5k08+qZ/97Gfq06ePcnNztWbNGq1evVobN24MbpOenq78/HwNGjRILpdL7du316RJk/TjH/9YV155pe666y7FxcXpL3/5i/72t7/pueeeq3OWm266STk5ORo+fLhmzZqlrl27as+ePXI4HLr99tv1xBNPqH///po6dapGjBihgoICzZkzR6+88krwPm655RbNmTNH2dnZqqqq0rhx40LOni9Genq6ysrKlJ+fr169eik5OVnJyckNug/AetF+kxzAxamqqjKpqalGkjlw4EDIuldeecV06dLFJCQkmG7dupmlS5eGrH/nnXdM165dTatWrcxVV10VXL5hwwYzcOBAk5SUZNxutxkwYICZP3/+Rc3z1VdfmTFjxpjvfOc7JjEx0fTs2dOsXbs2uH7lypWme/fuJiEhwVx55ZXmpZdeCtn/2LFj5gc/+IFp3bq1ycjIMOvXr6/1w2Q7d+4M7vP1118bSebDDz8MLnv44YfNd77zHSPJTJ48+aJmB2KJw5hvvUkEAACswae+AQCwGKEGUMOyZctCLtv651uPHj2iPR7QovDSN4AaSktLVVxcXOu6hIQEXXXVVU08EdByEWoAACzGS98AAFiMUAMAYDFCDQCAxQg1AAAWI9QAAFiMUAMAYDFCDQCAxf4/UU2KehgOuQMAAAAASUVORK5CYII="/>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [39]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#budget has second highest correlation of 0.73</span>
<span class="n">sns</span><span class="o">.</span><span class="n">relplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s1">'budget'</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="s1">'revenue'</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">high_rev_corr</span><span class="p">,</span> <span class="n">kind</span><span class="o">=</span><span class="s2">"scatter"</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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"/>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [40]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#popularity has the 3rd highest correlation of 0.67</span>
<span class="n">sns</span><span class="o">.</span><span class="n">relplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s1">'popularity'</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="s1">'revenue'</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">high_rev_corr</span><span class="p">,</span> <span class="n">kind</span><span class="o">=</span><span class="s2">"scatter"</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedImage jp-OutputArea-output" tabindex="0">
<img alt="No description has been provided for this image" class="" src="data:image/png;base64,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"/>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<h3 id="Answer">Answer<a class="anchor-link" href="#Answer">¶</a></h3><p>Vote Count, Budget, and Popularity Points show highest association with movies that have high revenues</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p><a id="conclusions"></a></p>
<h2 id="Conclusions">Conclusions<a class="anchor-link" href="#Conclusions">¶</a></h2><h3 id="Summary">Summary<a class="anchor-link" href="#Summary">¶</a></h3><ol>
<li>The top two most popular genres are Drama and Comedy.</li>
<li>Drama has been most popular generally from 1960 to 2015.</li>
<li>1990s has the highest film budget on average while 1970s has the lowest.</li>
<li>There is an increase in budget from 1970s to 1990s.</li>
<li>There is a decrease in budget from 1990s to 2010s.</li>
<li>Vote Count, Budget, and Popularity has highest association with the movies that have high revenues.</li>
</ol>
<h3 id="Limitations:">Limitations:<a class="anchor-link" href="#Limitations:">¶</a></h3><ol>
<li>The dataset contains null and zero values in some features. These zero and null values hinders the analysis and have to be removed. so data cleaning is a necessary part before moving on to the dataset's investigation.</li>
<li>There were multiple genres in each movie, I split the genress so each genre is allocated to 1 row.</li>
<li>The revenue and budget were not denominated in currency, so it’s unsure whether they are in USD, or another currency.</li>
</ol>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1"># Running this cell will execute a bash command to convert this notebook to an .html file</span>
<span class="o">!</span>python<span class="w"> </span>-m<span class="w"> </span>nbconvert<span class="w"> </span>--to<span class="w"> </span>html<span class="w"> </span>Investigate_a_Dataset.ipynb
</pre></div>
</div>
</div>
</div>
</div>
</div>
</main>
</body>
</html>
