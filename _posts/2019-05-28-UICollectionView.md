---
title: "UICollectionView."
date: 2019-05-28 17:18:28 +0900
categories: AppleDocs
tags:
- UICollectionView
- Apple Documentation
---

# UICollectionView
&nbsp;&nbsp;&nbsp;&nbsp;
__데이터 항목의 정렬 된 컬렉션을 관리하고 사용자 정의 가능한 레이아웃을 사용하여 데이터 항목을 표시하는 객체입니다.__



## 선언
```swift
class UICollectionView : UIScrollView
```

## 개요
**그림 1** flow layout을 사용한 컬렉션 뷰
![figure_1](/assets/images/post/2019-05-28-figure1.png)

&nbsp;&nbsp;&nbsp;&nbsp;
인터페이스에서 컬렉션 뷰를 추가할 때, 앱에서는 주로 컬렉션 뷰와 관련된 데이터를 관리하는 일을 합니다. [`UICollectionViewDataSource`](https://developer.apple.com/documentation/uikit/uicollectionviewdatasource) 프로토콜을 따르는 컬렉션 뷰는 앱에 의해서 *data source* 객체로부터 데이터를 가져옵니다. 컬렉션 뷰 내의 데이터는 각각의 *item*안에 구성되어있습니다. 그리고 이 *item*들을 *section*으로 그룹핑해서 표시할 수 있습니다. *item*은 화면에 표시하기 위한 데이터의 가장 작은 단위입니다. 예를 들면, 사진 앱에서, *item*은 아마 single image 하나 일 것입니다. 컬렉션 뷰는 *data source*가 설정하고 제공하는 [`UICollectionViewCell`](https://developer.apple.com/documentation/uikit/uicollectionviewcell) 클래스의 인스턴스인 *cell*을 사용하여 *item*들을 화면에 표시합니다.

&nbsp;&nbsp;&nbsp;&nbsp;
*cell* 이외에도, 컬렉션 뷰는 다른 타입의 뷰를 사용하여 데이터를 화면에 뿌려줄 수 있습니다. 이러한 *supplementary view*들은 각각의 *cell*와 별개로 *section header*와 *footer*처럼 사용할 수 있습니다. *supplementary view*를 만드는 것은 필수적이지 않고, 뷰들의 레이아웃을 배치하는 [`UICollectionViewLayout`](https://developer.apple.com/documentation/uikit/uicollectionviewlayout)객체에 정의되어 있습니다.

&nbsp;&nbsp;&nbsp;&nbsp;
인터페이스에 포함시키는 것(위처럼 data source에 구성하는 것) 이외에도, `UICollectionView` 객체의 메소드들을 사용하여 data source 객체의 순서와 시각적으로 보이는 아이템들의 순서가 일치하는지 확인할 수 있고, 컬렉션뷰 내의 셀을 추가하거나 삭제, 재배치하고 싶을 때마다, 이 클래스의 *insert*, *delete*, *rearrange* 메소드를 사용 할 수 있습니다. 또한 컬렉션 뷰 객체를 *selected item*을 관리하기 위해서 사용할 때가 있는데, 이 동작의 경우에는 컬렉션 뷰는 연결된 [*delegate*](https://developer.apple.com/documentation/uikit/uicollectionview/1618033-delegate) 객체와 함께 작동합니다.
<br>

## 컬렉션 뷰와 레이아웃 객체

&nbsp;&nbsp;&nbsp;&nbsp;
컬렉션 뷰와 관련된 가장 중요한 객체는 [`UICollectionViewLayout`](https://developer.apple.com/documentation/uikit/uicollectionviewlayout)클래스의 subclass인 *layout* 객체입니다. __*layout*객체는 컬렉션 뷰 내의 모든 *cell*과 *supplementary view*의 구조와 위치를 정의합니다.__ 해당 위치를 정의하더라도, *layout*객체는 실제로 해당 뷰에 직접 적용하지는 않습니다. *cell*과 *supplementary view*를 만드는 것은 *collectionView*와 *dataSource*객체간에 조정이 필요하기 때문입니다. 컬렉션 뷰는 실제로 뷰에 레이아웃 정보를 적용합니다. 따라서, 어떤 의미에서, *layout*객체는 시각적인 정보만을 제공하는 또다른 *data source*라고 할 수 있습니다.

&nbsp;&nbsp;&nbsp;&nbsp;
일반적으로 컬렉션 뷰를 생성할 때 *layout*객체를 지정하는데, 컬렉션 뷰의 *layout*을 동적으로 변경할 수도 있습니다. *layout*객체는 *collectionView* 내에 [`collectionViewLayout`](https://developer.apple.com/documentation/uikit/uicollectionview/1618047-collectionviewlayout)프로퍼티로 저장되어 있습니다. 이 프로퍼티를 변경하면, 애니메이션 없이 즉시 *layout*이 갱신됩니다. 애니메이팅 되는것을 원한다면, 반드시 [`setCollectionViewLayout(_:animated:completion:)`](https://developer.apple.com/documentation/uikit/uicollectionview/1618017-setcollectionviewlayout)메소드를 호출해줘야 합니다.

&nbsp;&nbsp;&nbsp;&nbsp;
*gesture recognizer*나 *touch events*에 의해 작동되는 interactive transition을 만들고 싶다면, [`startInteractiveTransition(to:completion:)`](https://developer.apple.com/documentation/uikit/uicollectionview/1618098-startinteractivetransition)메소드를 호출하여 *layout* 객체를 변경하십시오. 이 메소드는 중간 *layout* 객체를 만듭니다. 이 객체의 목적은 트랜지션 진행을 추적하기 위해 *gesture recognizer*나 *event-handling code*와 함께 작동하기 위함입니다. `event-handling code`가 트랜지션이 끝난 것을 결정 할 때, [`finishInteractiveTransition()`](https://developer.apple.com/documentation/uikit/uicollectionview/1618080-finishinteractivetransition)이나 [`cancelInteractiveTransition()`](https://developer.apple.com/documentation/uikit/uicollectionview/1618075-cancelinteractivetransition)메소드를 호출하여 중간 *layout*객체를 지우고 의도했던 *layout* 객체로 설정하십시오.

## Cell과 Supplimentary View 생성하기

&nbsp;&nbsp;&nbsp;&nbsp;
컬렉션 뷰의 *dataSource*객체는 *item*의 내용과, 컨텐츠를 표시하는데 사용할 *view* 를 제공합니다. 컬렉션 뷰가 컨텐츠를 처음 로드할 때, *dataSource*에게 현재 보이는 *item*에 대한 *view*를 제공해달라고 요청합니다. 코드 작성을 간단히 하기 위해서는, 코드에서 명시적으로 뷰를 생성하는 대신, 컬렉션 뷰에서 항상 *view*들을 *dequeue*하도록 해야합니다. 아래에 뷰를 dequeueing하기 위한 두 개의 메소드가 있습니다. 메소드는 요청하는 뷰의 타입에 따라서 호출하면 됩니다.

- [`dequeueReusableCell(withReuseIdentifier:for:)`](https://developer.apple.com/documentation/uikit/uicollectionview/1618063-dequeuereusablecell): *collectionView* 내에서 *item*에 대한 __*cell*__을 얻을 때 사용합니다.
- [`dequeueReusableSupplementaryView(ofKind:withReuseIdentifier:for:)`](https://developer.apple.com/documentation/uikit/uicollectionview/1618068-dequeuereusablesupplementaryview): *layout* 객체에 의해 요청된 __*supplementary view*__ 를 얻을 때 사용합니다.

위의 메소드들을 호출하기 전에, *collectionView*에 *class*나 *nib* 파일을 등록하는 과정을 통해서 반드시 *collectionView*에게 어떻게 해당 뷰를 생성할 지 알려줘야 합니다. 예를 들면, *cell*을 등록할 때, [`register(_:forCellWithReuseIdentifier:)`](https://developer.apple.com/documentation/uikit/uicollectionview/1618089-register)나 [`register(_:forCellWithReuseIdentifier:)`](https://developer.apple.com/documentation/uikit/uicollectionview/1618083-register)메소드를 사용해서 컬렉션 뷰에 등록합니다. 이 과정에서 뷰의 목적에 맞는 *reuse identifier*를 지정할 수 있습니다. 이 *reuse identifier* string을 나중에 *view*를 *dequeueing*할 때 사용할 수 있습니다.

&nbsp;&nbsp;&nbsp;&nbsp;
*delegate* 메소드안에서 적합한 뷰를 *dequeueing*한 이후, 컬렉션 뷰를 사용하기 위해 뷰의 컨텐츠를 설정하고 리턴하십시오. *layout*객체로부터 레이아웃 정보를 받은 이후에, 컬렉션 뷰는 뷰에 레이아웃을 적용하고 화면에 보여줍니다.

view를 설정하고 만들기 위한 *data source* 메소드를 구현하는 더 많은 정보는, 이 [`UICollectionViewDataSource`](https://developer.apple.com/documentation/uikit/uicollectionviewdatasource)를 참조하십시오.

## Item을 대화형으로 재배치하기

&nbsp;&nbsp;&nbsp;&nbsp;
컬렉션 뷰는 유저 인터렉션 기반으로 *item*을 움직일 수 있게 합니다. 일반적으로 컬렉션 뷰에서 *item*의 순서는 *dataSource*에 정의되어 있습니다. *item* 재배치 기능을 지원하려면, *gesture recognizer*를 컬렉션 뷰 *item*과 유저 인터렉션을 추적하고 *item*의 위치를 갱신하도록 설정해줘야 합니다. 

&nbsp;&nbsp;&nbsp;&nbsp;
*item*의 대화형 재배치를 시작하기 위해, 컬렉션 뷰의 [`beginInteractiveMovementForItem(at:)`](https://developer.apple.com/documentation/uikit/uicollectionview/1618019-begininteractivemovementforitem)메소드를 호출하십시오. *gesture recognizer*가 터치 이벤트를 추적하는 동안, 터치한 위치의 변화를 보고하기 위한 [`updateInteractiveMovementTargetPosition(_:)`](https://developer.apple.com/documentation/uikit/uicollectionview/1618079-updateinteractivemovementtargetp)메소드를 호출하십시오. 제스처 추적이 끝날때, 인터렉션과 컬렉션 뷰의 갱신을 종료하는 [`endInterativeMovement()`](https://developer.apple.com/documentation/uikit/uicollectionview/1618082-endinteractivemovement)나 [`cancelInteractiveMovement()`](https://developer.apple.com/documentation/uikit/uicollectionview/1618076-cancelinteractivemovement) 메소드를 호출하십시오.


