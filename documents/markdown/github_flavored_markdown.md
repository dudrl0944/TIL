# GFM(Github Flavored Markdown)

[GFM](https://help.github.com/en/github/writing-on-github/basic-writing-and-formatting-syntax#styling-text) 페이지 보면서 연습한 페이지 입니다.

## In this article
- [Headings](#Headings)
- [Styling text](#Styling)
- Quoting text
- Quoting code
- Links
- Section links
- Relative links
- Lists
- Task lists
- Mentioning people and teams
- Referencing issues and pull requests
- Referencing external resources
- Content attachments
- Using emoji
- Paragraphs and line breaks
- Ignoring Markdown formatting
- Further reading

### Headings
``` 
# 가장 큰 제목
## 두번째로 큰 제목
###### 가장 작은 제목
```
# 가장 큰 제목
## 두번째로 큰 제목
###### 가장 작은 제목

### Styling text

|Style                  |Syntax             |Keyboard shortcut  |Example   |Output  |
| --------------------- | ------------------| ----------------- |----------|--------|
|Bold                   |`** **`or`__ __`   |command/control + b|`**blod**`|**blod**|
|Italic                 |`* *`or`_ _`       |command/control + i|`*italicized*`|*italicized*|
|Strikethrough          |`~~ ~~`            |                   |`~~mistaken text~~`|~~mistaken text~~|
|Bold and nested italic |`** **`and`_ _`    |                   |`**This text is _extremely_ important**`|**This text is _extremely_ important**|
|All bold and italic    |`*** ***`          |                   |`***All this text is important***`|	***All this text is important***|


### 인용한 내용(Quoting text)
```
In the words of Abraham Lincoln:

> Pardon my French
```

In the words of Abraham Lincoln:

> Pardon my French


### 인용한 코드(Quoting code)
```
Use `git status` to list all new or modified files that haven't yet been committed.
```
Some basic Git commands are:
```
git status
git add
git commit
```

회색박스 생성하기
``````
````
```
function test() {
  console.log("notice the blank line before this function?");
}
```
````
``````


문법 하이라이팅 하기
``````
```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```
``````
```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```

### 링크
`[GitHub Pages](https://pages.github.com/)`

### Section 링크
`[Contribution guidelines for this project](docs/CONTRIBUTING.md)`
파일 경로에`./`와`../`를 사용할 수 있다.


### Lists
```
- George Washington
- John Adams
- Thomas Jefferson
```
- George Washington
- John Adams
- Thomas Jefferson

```
* George Washington
* John Adams
8 Thomas Jefferson
```
* George Washington
* John Adams
* Thomas Jefferson


```
1. James Madison
2. James Monroe
3. John Quincy Adams
```
1. James Madison
2. James Monroe
3. John Quincy Adams


```
1. First list item
   - First nested list item
     - Second nested list item
```
1. First list item
   - First nested list item
     - Second nested list item

### Task lists
```
- [x] Finish my changes
- [ ] Push my commits to GitHub
- [ ] Open a pull request
- [ ] \(Optional) Open a followup issue
부가 설명 `\`
```
- [x] Finish my changes
- [ ] Push my commits to GitHub
- [ ] Open a pull request
- [ ] \(Optional) Open a followup issue

### Mentioning people and teams
`@github/support What do you think about these updates?`
@github/support What do you think about these updates?

### Referencing issues and pull requests
`To DO`
### Referencing external resources
`To DO`
### Content attachments
`To Do`
### Using emoji
`To Do`
### Paragraphs and line breaks
`To Do`
### Ignoring Markdown formatting
`To Do`





