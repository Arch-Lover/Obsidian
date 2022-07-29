# Markdown Basics

## Headlines, paragraph, and Basic Formatting

### Headlines

#### Headlines level 4
##### Headlines level 5
###### Headlines level 6

### Paragraphs and Line Breaks

as we can see the LVM is named xubuntu--vg-root, but we cannot run fsck on this name as it will not find it.  We need to get the whole name.  To do this we are going to run the lvm lvscan command to get the LV name so we can run fsck on the LVM.

As we can see our name to check is /dev/xubuntu-vg/root so we should be able to run fsck on that name.

If the /dev/xubuntu-vg/root is  
not ACTIVE, we need to make it active so that we can run the check on it

### Emphasis and Bolding

#### Italics

This *works*, and this _works_ too.


#### Bolding

This **works**, and __works__ too.

This ***works***, and this ___works___ too.

### Blockquotes

> as we can see the LVM is named xubuntu--vg-root, but we cannot run fsck on this name as it will not find it.  We need to get the whole name.  To do this we are going to run the lvm lvscan command to get the LV name so we can run fsck on the LVM.
>
> As we can see our name to check is /dev/xubuntu-vg/root so we should be able to run fsck on that name.

### Horizantal Rule

___

---

***

### Lists


### Numbers Lists

1. Item 1
2. Item 2
1. Item 4
1. Item 5
1. Item 6

---

1. Item 1

2. Item 2
1. Item 4
1. Item 5
1. Item 6


1. Item 1
  1. Item 1
  2. Item 2


### Bulleted Lists

* Item
* Item


* Item
  * Item
    * Item

*Italics Item*
*Item with no Formatting
* Bulleted Item


* ***Bulleted, bold, Italics***


1. Item 1
  * Item
  * Item
2. Item 2
  * Item
    1. Item 1
    2. item 2

---

## Code

To install the latest version of NPM, you can type, `npm install npm@latest -g`

```Go
package main()

(
  import fmt
)

```
---

## Links

[GOOGLE](https://google.com)


[GOOGLE](https://google.com "Link to Google search engine")


---

### Images

![Google logo](https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png)


[![Google logo](https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png)](goole.com)



![Google logo](https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png "cute google")


[![Google logo](https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png "Hi google")](goole.com)

---
