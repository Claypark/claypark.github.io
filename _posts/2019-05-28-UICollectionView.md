---
title: "UICollectionView."
date: 2019-05-28 17:18:28 +0900
categories: Apple Document
tags:
- UICollectionView
- Apple Documentation
---

# UICollectionView
- 데이터 항목의 정렬 된 컬렉션을 관리하고 사용자 정의 가능한 레이아웃을 사용하여 데이터 항목을 표시하는 객체입니다.
*****

## 선언
```swift
class UICollectionView : UIScrollView
```

## 개요
**그림 1** flow layout을 사용한 컬렉션 뷰
![figure_1](/assets/images/post/2019-05-28-figure1.png)
  유저 인터페이스에서 컬렉션 뷰를 추가할 때, 앱에서는 주로 컬렉션 뷰와 관련된 데이터를 관리하는 일을 합니다. `UICollectionViewDataSource` 프로토콜을 따르는 컬렉션 뷰는 앱에 의해서 *data source* 객체로부터 데이터를 가져옵니다. 컬렉션 뷰 내의 데이터는 각각의 *item*안에 구성되어있습니다. 그리고 이 *item*들을 *section*으로 그룹핑해서 표시할 수 있습니다. *item*은 화면에 표시하기 위한 데이터의 가장 작은 단위입니다. 예를 들면, 사진 앱에서, *item*은 아마 single image 하나 일 것입니다. 컬렉션 뷰는 *data source*가 설정하고 제공하는 `UICollectionViewCell` 클래스의 인스턴스인 *cell*을 사용하여 *item*들을 화면에 표시합니다. 
  *cell* 이외에도, 컬렉션 뷰는 다른 타입의 뷰를 사용하여 데이터를 화면에 뿌려줄 수 있습니다. 이러한 *supplementary view*들은 각각의 *cell*와 별개로 *section header*와 *footer*처럼 사용할 수 있습니다. *supplementary view*를 만드는 것은 필수적이지 않고, 뷰들의 레이아웃을 배치하는 `UICollectionViewLayout`객체에 정의되어 있습니다.
  유저 인터페이스에 포함시키는 것(위처럼 data source에 구성하는 것) 이외에도, `UICollectionView` 객체의 메소드들을 사용할 수 있습니다. 
