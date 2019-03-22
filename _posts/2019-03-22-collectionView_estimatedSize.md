---
title: "Implements collectionView's self-sizing cell."
date: 2019-03-22 17:34:12 +0900
categories: iOS
tags:
- CollectionView
- UI
---
  
  
  
### 개요

구현할 것:
- width가 고정인 CollectionViewCell의 자동 높이 계산.

필요한 것: 
- CollectionViewLayout의 estimatedSize 설정해주기.
- CollectionViewCell에서 메소드 구현해주기.
- Autolayout을 통해 width 고정 시키기.
<br/>
<br/>

### CollectionViewLayout의 estmatedSize 설정해주기.

```swift
collectionViewLayout.itemSize = UICollectionViewFlowLayout.automaticSize
collectionViewLayout.estimatedItemSize = CGSize(width: 100, height: 100)
```  
<br/>
<br/>

### CollectionViewCell에서 메소드 구현해주기.

```swift
override func preferredLayoutAttributesFitting(_ layoutAttributes: UICollectionViewLayoutAttributes) -> UICollectionViewLayoutAttributes {
    setNeedsLayout()
    layoutIfNeeded()

    let size = contentView.systemLayoutSizeFitting(layoutAttributes.size)
    var frame = layoutAttributes.frame
    frame.size.height = ceil(size.height)
    layoutAttributes.frame = frame

    return layoutAttributes
}
```
<br/>  
<br/>  
  
### Autolayout을 이용해 width 고정시키기.

```swift
override func awakeFromNib() {
    ...
    contentView.widthAnchor.constraint(equalToConstant: UIScreen.main.bounds.width).isActive = true
    ...
}
```
<br/>  
<br/>  
  
### 전체 코드

```swift

class ViewController: UIViewController {
    @IBOutlet weak var collectionView: UICollectionView!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        ...
        
        // setting estimatedSize
        collectionView.collectionViewLayout.itemSize = UICollectionViewFlowLayout.automaticSize
        collectionView.collectionViewLayout.estimatedItemSize = CGSize(width: 100, height: 100)
        
        ...
    }
}


class CollectionViewCell: UICollectionViewCell {
    ...
    
    // self-sizing cell height
    override func preferredLayoutAttributesFitting(_ layoutAttributes: UICollectionViewLayoutAttributes) -> UICollectionViewLayoutAttributes {
        setNeedsLayout()
        layoutIfNeeded()
        
        let size = contentView.systemLayoutSizeFitting(layoutAttributes.size)
        var frame = layoutAttributes.frame
        frame.size.height = ceil(size.height)
        
        return layoutAttributes
    }
    
    // fixing cell width
    override func awakeFromNib() {
        contentView.widthAnchor.constraint(equalToConstant: UIScreen.main.bounds.width).isActive = true
    }
}

```
