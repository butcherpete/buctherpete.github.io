---
title: Vim Bookmarks 
tags: [vim]
keywords: vim 
last_updated: January 29, 2017
summary: "This vim plugin allows toggling bookmarks per line. A quickfix window gives access to all bookmarks. Annotations can be added as well. These are special bookmarks with a comment attached. They are useful for preparing code reviews. All bookmarks will be restored on the next startup."
sidebar: notes_sidebar
permalink: vim_bookmarks.html
folder: vim 
---

## Resources

[vim-bookmarks](https://github.com/MattesGroeger/vim-bookmarks)

## Bookmarks

Shortcut |	Command |	Action
------ | ------------ | --------
`mm`  | 	`:BookmarkToggle` | Toggle bookmark at current line.

## Annotations

Shortcut |	Command |	Action
------ | ------------ | --------
`mi` | 	`:BookmarkAnnotate` <TEXT> | Add/edit/remove annotation at current line.	

## Navigation

Shortcut |	Command |	Action
------ | ------------ | --------
`mn` | 	`:BookmarkNext` |  Jump to next bookmark in buffer.
`mp` | 	`:BookmarkPrev`|  Jump to previous bookmark in buffer.
`ma` | 	`:BookmarkShowAll` | Show all bookmarks (toggle).
`mc` | 	`:BookmarkClear` | Clear bookmarks in current buffer only.
`mx` | 	`:BookmarkClearAll` | Clear bookmarks in all buffers.
`mkk` | 	`:BookmarkMoveUp` | Move up bookmark at current line.	
`mjj` | 	`:BookmarkMoveDown` | Move down bookmark at current line.	
 | `:BookmarkSave` <FILE_PATH> |  Save all bookmarks to a file.		
 | `:BookmarkLoad` <FILE_PATH> | Load bookmarks from a file.		

## Saving Bookmarks to File

Command |	Action
------------ | --------
`:BookmarkSave` <FILE_PATH> |  Save all bookmarks to a file.		

## Loading Bookmarks from File

Command |	Action
------------ | --------
`:BookmarkLoad` <FILE_PATH> | Load bookmarks from a file.		
