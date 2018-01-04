---
layout: post
title:  "iOS View관련 Method"
date:   2018-01-02 15:36:20
author: Jakouk
categories: iOS
---

## iOS View관련 Method

1. loadView() vs awakeFromNib()
- loadView()는 viewController에 의해서 관리되는 메서드로 viweController는 현재 뷰가 nil일때 viewController를 호출한다. 따라서 storyboard를 사용하면 loadView 메서드를 사용할 필요가 없고 코드만을 이용해서 화면을 만들경우 loadView()를 이용하면 된다. 
- awakeFromNib()은 NSObject에 카테고리로 추가된 메서드로 viewController는 현재 뷰에 storyBoard에 있을때 부르게 된다. viewController의 메서드들 중에서 가장 먼저 불린다.

> 결국 loadView()나 awakeFromNib()를 사용할때 Storyboard를 이용해서 작업하면 awakeFromNib 코드만을 이용해서 작업하면 loadView를 사용하면 된다. 

- Tip
>> - 스토리보드를 사용해서 만들경우 loadView()와 awakeFromNib()를 만들면 awakeFromNib()이 실행되고 loadView()가 실행된다.
>> - 코드만을 사용해서 만들경우 loadView()와 awakeFromNib()를 만들면 awkeFromNib()은 실행되지 않고 loadView()만 실행된다. 

계속해서 Method들을 대해서 추가하면서 설명할 예정이다. 





