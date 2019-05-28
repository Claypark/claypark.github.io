---
title: "UICollectionView."
date: 2019-05-28 17:18:28 +0900
categories: AppleDocs
tags:
- UICollectionView
- Apple Documentation
---

# UICollectionView
- 데이터 항목의 정렬 된 컬렉션을 관리하고 사용자 정의 가능한 레이아웃을 사용하여 데이터 항목을 표시하는 객체입니다.

***

## 선언
```swift
class UICollectionView : UIScrollView
```

## 개요
**그림 1** flow layout을 사용한 컬렉션 뷰
![figure_1](/assets/images/post/2019-05-28-figure1.png)

&nbsp;&nbsp;&nbsp;&nbsp;
인터페이스에서 컬렉션 뷰를 추가할 때, 앱에서는 주로 컬렉션 뷰와 관련된 데이터를 관리하는 일을 합니다. `UICollectionViewDataSource` 프로토콜을 따르는 컬렉션 뷰는 앱에 의해서 *data source* 객체로부터 데이터를 가져옵니다. 컬렉션 뷰 내의 데이터는 각각의 *item*안에 구성되어있습니다. 그리고 이 *item*들을 *section*으로 그룹핑해서 표시할 수 있습니다. *item*은 화면에 표시하기 위한 데이터의 가장 작은 단위입니다. 예를 들면, 사진 앱에서, *item*은 아마 single image 하나 일 것입니다. 컬렉션 뷰는 *data source*가 설정하고 제공하는 `UICollectionViewCell` 클래스의 인스턴스인 *cell*을 사용하여 *item*들을 화면에 표시합니다.

&nbsp;&nbsp;&nbsp;&nbsp;
*cell* 이외에도, 컬렉션 뷰는 다른 타입의 뷰를 사용하여 데이터를 화면에 뿌려줄 수 있습니다. 이러한 *supplementary view*들은 각각의 *cell*와 별개로 *section header*와 *footer*처럼 사용할 수 있습니다. *supplementary view*를 만드는 것은 필수적이지 않고, 뷰들의 레이아웃을 배치하는 `UICollectionViewLayout`객체에 정의되어 있습니다.

&nbsp;&nbsp;&nbsp;&nbsp;
인터페이스에 포함시키는 것(위처럼 data source에 구성하는 것) 이외에도, `UICollectionView` 객체의 메소드들을 사용하여 data source 객체의 순서와 시각적으로 보이는 아이템들의 순서가 일치하는지 확인할 수 있고, 컬렉션뷰 내의 셀을 추가하거나 삭제, 재배치하고 싶을 때마다, 이 클래스의 *insert*, *delete*, *rearrange* 메소드를 사용 할 수 있습니다. 또한 컬렉션 뷰 객체를 *selected item*을 관리하기 위해서 사용할 때가 있는데, 이 동작의 경우에는 컬렉션 뷰는 연결된 *delegate* 객체와 함께 작동합니다.
<br>

## 컬렉션 뷰와 레이아웃 객체

&nbsp;&nbsp;&nbsp;&nbsp;
컬렉션 뷰와 관련된 가장 중요한 객체는 `UICollectionViewLayout`클래스의 subclass인 *layout* 객체입니다. __*layout*객체는 컬렉션 뷰 내의 모든 *cell*과 *supplementary view*의 구조와 위치를 정의합니다.__ 해당 위치를 정의하더라도, *layout*객체는 실제로 해당 뷰에 직접 적용하지는 않습니다. *cell*과 *supplementary view*를 만드는 것은 *collectionView*와 *dataSource*객체간에 조정이 필요하기 때문입니다. 컬렉션 뷰는 실제로 뷰에 레이아웃 정보를 적용합니다. 따라서, 어떤 의미에서, *layout*객체는 시각적인 정보만을 제공하는 또다른 *data source*라고 할 수 있습니다.

&nbsp;&nbsp;&nbsp;&nbsp;
일반적으로 컬렉션 뷰를 생성할 때 *layout*객체를 지정하는데, 컬렉션 뷰의 *layout*을 동적으로 변경할 수도 있습니다. *layout*객체는 *collectionView* 내에 `collectionViewLayout`프로퍼티로 저장되어 있습니다. 이 프로퍼티를 변경하면, 애니메이션 없이 즉시 *layout*이 갱신됩니다. 애니메이팅 되는것을 원한다면, 반드시 `setCollectionViewLayout(_:animated:completion:)`메소드를 호출해줘야 합니다.

&nbsp;&nbsp;&nbsp;&nbsp;
*gesture recognizer*나 *touch events*에 의해 작동되는 interactive transition을 만들고 싶다면, `startInteractiveTransition(to:completion:)`메소드를 호출하여 *layout* 객체를 변경하십시오. 이 메소드는 중간 *layout* 객체를 만듭니다. 이 객체의 목적은 트랜지션 진행을 추적하기 위해 *gesture recognizer*나 *event-handling code*와 함께 작동하기 위함입니다. `event-handling code`가 트랜지션이 끝난 것을 결정 할 때, `finishInteractiveTransition()`이나 `cancelInteractiveTransition()`메소드를 호출하여 중간 *layout*객체를 지우고 의도했던 *layout* 객체로 설정하십시오.

## *Cell*과 *Supplimentary View* 생성하기

&nbsp;&nbsp;&nbsp;&nbsp;
