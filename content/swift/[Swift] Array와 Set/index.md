---
emoji: π§
title: '[Swift] Arrayμ Setμ μλμ°¨μ΄'
date: '2023-02-17 00:00:00'
author: κ³ λ°
tags: Swift
categories: Swift
---

# κ°μ

[μκ³ λ¦¬μ¦ λ¬Έμ ](https://gobanest.com/algorithm/programmers/κ°μ₯%20λ¨Ό%20λΈλ/)λ₯Ό νλ λμ€.. Arrayμ Setμ μ¬μ©νμλ λ§μ μκ°μ°¨μ΄κ° λ°μνλ κ²μ λ°κ²¬νλ€.

<br/>

κ·Έ μ΄μ λ λ¬΄μμΌκΉ.

κ°λ¨ν μ€νμ ν΅ν΄μ μΌλ§λ μλκ° μ°¨μ΄λλμ§ μμλ³΄κ³  μ΄μ  λν μμλ³΄μ.

<br/>

## μ€ν

μ°μ  μ€νμ μ¬μ©ν  μ μ©ν μ‘°μλ₯Ό μκ°νλ€.

μ½λλ₯Ό ν΄λ‘μ λ‘ λ°μμ μ¬μ©ν  μ μλ μμ£Ό μ’μ λμμ΄λ€.

<br/>

```swift
public func progressTime(_ closure: () -> ()) -> TimeInterval {
    let start = CFAbsoluteTimeGetCurrent()
    closure()
    let diff = CFAbsoluteTimeGetCurrent() - start
    return (diff)
}
```

μ½λλ [μ΄κ³³](https://chanhhh.tistory.com/94)μμ κ°μ Έμλ€.

<br/>

κ·Έ λ€μ Arrayμ Setμ μμ μΆκ°, μν, μ­μ λ₯Ό νμ€νΈνλ€.

<br/>

```swift
import Foundation

public func ArraySet_Performance() {
    
    var testArray: [Int] = []
    var testSet = Set<Int>()
    
    // Addition
    /// Array: 18.3260840177536
    print(progressTime {
        for i in 0...10*1000 {
            testArray.append(i)
        }
    })
    
    /// Set: 0.09251093864440918
    print(progressTime {
        for i in 0...10*1000 {
            testSet.insert(i)
        }
    })
    
    // Iteration
    /// Array: 0.029738903045654297
    print(progressTime {
        for _ in testArray {
            
        }
    })
    
    /// Set: 0.000051975250244140625
    print(progressTime {
        for _ in testSet {
            
        }
    })
    
    // Removal
    /// Array: 0.008929967880249023
    print(progressTime{
        while !testArray.isEmpty {
            testArray.removeFirst()
        }
    }
    )
    
    /// Set: 0.0012810230255126953
    print(progressTime{
        while !testSet.isEmpty {
            testSet.removeFirst()
        }
    }
    )
    
}

```

<br/>

1λ§λ² κΈ°μ€ μλμ μ°¨μ΄λ λ€μκ³Ό κ°λ€.

<br/>

    1. μΆκ°: μ½ 198λ°°
    2. μν: μ½ 570λ°°
    3. μ²«λ²μ§Έ μμ μ­μ : μ½ 6λ°°

<br/>

μνκ° μλ μ°¨μ΄λ κ°μ₯ ν¬μ§λ§, κΈ°μ€ μλμ μ°¨μ΄ λλ¬Έμ μΆκ°κ° κ°μ μ°¨μ΄κ° κ°μ₯ λ§μ΄λλ€.

<br/>

μ€λ‘ μ΄λ§μ΄λ§ν μ°¨μ΄μ΄λ€.. μ μ΄λ° μ°¨μ΄κ° λλ κ²μΌκΉ?

<br/>

## μ΄μ 

<br/>

μ°μ  Arrayμ Setμ κ°μ₯ ν° μ°¨μ΄λ `μ λ ¬`μ΄λ€.

μ½λλ₯Ό λ³΄μ.

<br/>

```swift
public func AccessValue() {
    
    var testArray: [Int] = []
    var testSet = Set<Int>()
    
    for i in 0...100 {
        testArray.append(i)
    }

    for i in 0...100 {
        testSet.insert(i)
    }

    print("Array")
    for i in testArray {
        print(i, terminator: " ")
    }
    print("")
    print("Set")
    for i in testSet {
        print(i, terminator: " ")
    }

}

/* Result
 
 // Array is an ordered, random-access collection.
 
 Array
 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71 72 73 74 75 76 77 78 79 80 81 82 83 84 85 86 87 88 89 90 91 92 93 94 95 96 97 98 99 100
 
 // Set is an unordered collection of unique elements.
 
 Set
 51 10 85 95 84 76 78 25 5 77 53 18 40 29 36 45 96 80 28 0 34 4 56 48 35 15 3 42 41 68 50 64 47 88 16 57 14 38 92 74 7 24 90 46 87 1 62 65 23 54 12 55 58 79 32 43 31 17 22 81 100 6 89 94 99 66 82 61 8 9 60 91 26 19 86 93 2 71 52 27 13 37 39 73 49 72 59 33 75 11 83 98 20 63 67 97 21 30 70 69 44
 */

```

<br/>

λ³΄λ€μνΌ Arrayμ Setμ λκ°μ μμλ‘ μ½μμ νμ§λ§, Arrayλ μμ°¨μ μΌλ‘ μ κ±°λ λ°λ©΄ Setμ λλ€νκ² μ­μ λμλ€.

μ΄λ¬ν μ°¨μ΄μ μ΄μ λ₯Ό Arrayμ Setμ μμ μΆκ°, μν, μ­μ  λ©μλμμ μ΄ν΄λ³΄μ.

<br/>

### μΆκ°

[Array]
```swift
  public mutating func append(_ newElement: __owned Element) {
    // Separating uniqueness check and capacity check allows hoisting the
    // uniqueness check out of a loop.
    _makeUniqueAndReserveCapacityIfNotUnique()
    let oldCount = _buffer.mutableCount
    _reserveCapacityAssumingUniqueBuffer(oldCount: oldCount)
    _appendElementAssumeUniqueAndCapacity(oldCount, newElement: newElement)
    _endMutation()
  }
```

<br/>

- _makeUniqueAndReserveCapacityIfNotUnique()
    - κ°μ unique μ²΄ν¬ λ° μΆκ° buffer μμ±
- _reserveCapacityAssumingUniqueBuffer(oldCount: oldCount)
    - νΉμν κ²½μ° λλ¬Έμ buffer κ° μ λλ‘ μμ±λμ§ μμμ λ, buffer μμ±
- _appendElementAssumeUniqueAndCapacity
    - μλ‘μ΄ λ²νΌμ μμ μΆκ°

Arrayμ κ²½μ° elementκ° μΆκ°λ  λ κ°μ΄ unique νμ§ (μ£Όμνκ²λ class μΈμ§) μ²΄ν¬ν ν bufferλ₯Ό μμ±νμ¬ μμλ₯Ό μΆκ°ν΄μ€λ€.

μ΄ κ³Όμ μμ elementμ μμμ uniqueκ° μ μ§λλ€.


<br/>



[Set]
```swift
  internal func _unsafeInsertNew(_ element: __owned Element) {
    _internalInvariant(count + 1 <= capacity)
    let hashValue = self.hashValue(for: element)
    if _isDebugAssertConfiguration() {
      // In debug builds, perform a full lookup and trap if we detect duplicate
      // elements -- these imply that the Element type violates Hashable
      // requirements. This is generally more costly than a direct insertion,
      // because we'll need to compare elements in case of hash collisions.
      let (bucket, found) = find(element, hashValue: hashValue)
      guard !found else {
        ELEMENT_TYPE_OF_SET_VIOLATES_HASHABLE_REQUIREMENTS(Element.self)
      }
      hashTable.insert(bucket)
      uncheckedInitialize(at: bucket, to: element)
    } else {
      let bucket = hashTable.insertNew(hashValue: hashValue)
      uncheckedInitialize(at: bucket, to: element)
    }
    _storage._count &+= 1
  }
```

<br/>

λ°λ©΄μ Setμ μμ μΆκ° κ³Όμ μ λ³΄λ©΄, hashValueλ‘ μ€λ³΅λ κ°μ μ°Ύκ³  μ€λ³΅λ κ°μ΄ μλ€λ©΄ μμ μμλ₯Ό μ°Ύμ§ μλλ€.

```swift
    let (bucket, found) = find(element, hashValue: hashValue)
    guard !found else {
    ELEMENT_TYPE_OF_SET_VIOLATES_HASHABLE_REQUIREMENTS(Element.self)
    }
```

<br/>

λλ¬Έμ Arrayμλ λ€λ₯΄κ² `μ€λ³΅λ κ°μ΄ μλ€.`

<br/>

```swift
/// Insert a new entry for an element at index'.
@inlinable @inline(__always)
internal func insert( bucket: Bucket) {
    _internalInvariant(!isOccupied(bucket))
    words[bucket.word].uncheckedInsert(bucket.bit)
}
```

<br/>

λ λ€λ₯΄κ² μ£Όλͺ©ν΄μΌν  λΆλΆμ hashTableμ insert λμμ΄λ€.

ν΄λΉ μ½λλ₯Ό λ³΄λ©΄ wordsμ subscriptλ‘ bucket.wordλ₯Ό μ¬μ©νλ κ²μ λ³Ό μ μλ€. κ·Έλ¦¬κ³  μ΄ words[bucket.word] (UnsafeMutablePointer) κ³΅κ°μ bitκ° μ μ₯λλ€.


<br/>

```swift
extension _UnsafeBitset {
@inlinable
@inline (__ always)
internal static func word(for element: Int) -> Int {
    _internalInvariant(element >= 0)
    // Note: We perform on UInts to get faster unsigned math (shifts).
    let element = UInt (bitPattern: element)
    let capacity = UInt(bitPattern: Word.capacity)
    return Int(bitPattern: element / capacity)
}
```

<br/>

wordλ offset (element)κ³Ό capacityλ₯Ό μ΄μ©ν΄ κ³ μ νκ² μμ±λμ΄ μ¬μ©λλ€.

<br/>

μ μ₯λλ κ°μ μ£Όμλ hashValueκ° λ°λμ λ°λΌ wordμ μμ±μμ λ§€λ² λ¬λΌμ§λ€.

λλ¬Έμ `λ§€λ² Setμ μμκ° λ¬λΌμ§λ κ²`μ΄λ€.

<br/>
<br/>

μ΄μ¨λ  μ΄λ¬ν λ©μλμ λμ μ°¨μ΄λ₯Ό λ΄€μ λ μ°λ¦¬κ° μμλ³΄κ³ μ νλ Arrayμ Setμ 'μΆκ°' λ©μλμ μ±λ₯μ°¨μ΄λ buffer μμ±κ³Ό bucket μμ±μ μ°¨μ΄μ μλλ― νλ€.

<br/>


### μν

[Array]
```swift
  public mutating func next() -> Elements.Element? {
    if _position == _elements.endIndex { return nil }
    let element = _elements[_position]
    _elements.formIndex(after: &_position)
    return element
  }
```

<br/>

Arrayμ Iteratorλ μ°λ¦¬κ° μ°λ κ² μ²λΌ subscriptλ₯Ό μ¬μ©νκ³ μλ€.

<br/>


[Set]
```swift
    // hashTable Iterator
    internal mutating func next() -> Bucket? {
      if let bit = word.next() {
        return Bucket(word: wordIndex, bit: bit)
      }
      while wordIndex + 1 < hashTable.wordCount {
        wordIndex += 1
        word = hashTable.words[wordIndex]
        if let bit = word.next() {
          return Bucket(word: wordIndex, bit: bit)
        }
      }
      return nil
    }
```

<br/>

hashTableμ Iteratorλ₯Ό λ³΄λ©΄ λ€μ bucketμ wordIndexμ λ€μ bitλ‘ μλ³νμ¬ Iteration νκ³  μλ€.

<br/>

Arrayμ Setμ 'μΆκ°' λ©μλμ μ±λ₯μ°¨μ΄λ₯Ό λ³΄μλ©΄..

Arrayμ element μ κ·Όμ O(1)μΈλ°, Set λν O(1) μ΄λ€.

κ·Έλ¬λ subscript λμμμ Setμ΄ μ‘°κΈ λ λΉ λ₯΄κΈ° λλ¬Έμ μ΄λ¬ν μ°¨μ΄κ° λ°μνλκ² μλκ° μΆλ€. 

<br/>

[Array]
```swift
  public subscript(index: Int) -> Element {
    get {
      // This call may be hoisted or eliminated by the optimizer.  If
      // there is an inout violation, this value may be stale so needs to be
      // checked again below.
      let wasNativeTypeChecked = _hoistableIsNativeTypeChecked()

      // Make sure the index is in range and wasNativeTypeChecked is
      // still valid.
      let token = _checkSubscript(
        index, wasNativeTypeChecked: wasNativeTypeChecked)

      return _getElement(
        index, wasNativeTypeChecked: wasNativeTypeChecked,
        matchingSubscriptCheck: token)
    }
    _modify {
      _makeMutableAndUnique() // makes the array native, too
      _checkSubscript_mutating(index)
      let address = _buffer.mutableFirstElementAddress + index
      defer { _endMutation() }
      yield &address.pointee
    }
  }
```

<br/>

[Set]
```swift
  internal mutating func next() -> Int? {
    guard value != 0 else { return nil }
    let bit = value.trailingZeroBitCount
    value &= value &- 1       // Clear lowest nonzero bit.
    return bit
  }
```

<br/>

Arrayλ Setκ³Ό λΉκ΅ν΄μ μ‘°κΈ λ μ²λ¦¬κ° λ§μ΄ μΌμ΄λκ³ , Setμ κ°λ¨νκ² bitλ₯Ό κ΅¬νμ¬ λ€μ μμμ μμλ₯Ό λ³΄μ¬μ£Όκ³  μλ€.

μ΄ λλ¬Έμ μλ μ°¨μ΄κ° λλκ² μλκΉ μκ°νλ€.

<br/>

### μ­μ 

[Array]

```swift
public mutating func removeFirst(_ k: Int) {
    if k == 0 { return }
    _precondition(k >= 0, "Number of elements to remove should be non-negative")
    guard let idx = index(startIndex, offsetBy: k, limitedBy: endIndex) else {
        _preconditionFailure(
        "Can't remove more items from a collection than it contains")
    }
    self = self[idx..<endIndex]
}
```

<br/>

[Set]

```swift
  internal func delete<D: _HashTableDelegate>(
    at bucket: Bucket,
    with delegate: D
  ) {
    _internalInvariant(isOccupied(bucket))

    // If we've put a hole in a chain of contiguous elements, some element after
    // the hole may belong where the new hole is.

    var hole = bucket
    var candidate = self.bucket(wrappedAfter: hole)

    guard _isOccupied(candidate) else {
      // Fast path: Don't get the first bucket when there's nothing to do.
      words[hole.word].uncheckedRemove(hole.bit)
      return
    }

    // Find the first bucket in the contiguous chain that contains the entry
    // we've just deleted.
    let start = self.bucket(wrappedAfter: previousHole(before: bucket))

    // Relocate out-of-place elements in the chain, repeating until we get to
    // the end of the chain.
    while _isOccupied(candidate) {
      let candidateHash = delegate.hashValue(at: candidate)
      let ideal = idealBucket(forHashValue: candidateHash)

      // Does this element belong between start and hole?  We need two
      // separate tests depending on whether [start, hole] wraps around the
      // end of the storage.
      let c0 = ideal >= start
      let c1 = ideal <= hole
      if start <= hole ? (c0 && c1) : (c0 || c1) {
        delegate.moveEntry(from: candidate, to: hole)
        hole = candidate
      }
      candidate = self.bucket(wrappedAfter: candidate)
    }

    words[hole.word].uncheckedRemove(hole.bit)
  }
```

<br/>

Arrayμ Setμ 'μ²«λ²μ§Έ μμ μ­μ ' λ©μλμ μ±λ₯μ°¨μ΄λ₯Ό λ³΄μλ©΄...

Arrayμ Set λͺ¨λ μ²«λ²μ§Έ μμλ₯Ό μ μΈν μμλ€μ μ¬ν λΉνλ μ½λκ° μλ€.

<br/>

    Array: self = self[idx..<endIndex]
    Set:  while _isOccupied(candidate) { }

<br/>

μ΄ κ³Όμ μμ μμλ§λ€μ bufferκ³Ό bucketμ μ¬ν λΉμμ Setμ΄ λ λΉ¨λΌμ κ·Έλ°κ² μλκ° μκ°μ΄ λ λ€.

<br/>


# λ§λ¬΄λ¦¬

## μμ½

κ²°κ³Όμ μΌλ‘ Array λ³΄λ€ Setμ μΆκ°, μν, μ κ±° μλκ° μλ±ν λΉ¨λλ€.

κ·Έλ κΈ° λλ¬Έμ λ§μ½μ **μμκ° μ€μνμ§μκ³ ** **μ€λ³΅κ°μ΄ νμμλ** κ²½μ°λΌλ©΄ Setμ μ¬μ©νλκ² μλ μΈ‘λ©΄μμ ν° μ΄μ μ΄ μλ€.

κ·Έλ¦¬κ³  μ΄λ¬ν μλ μ°¨μ΄κ° λ°μνλ μ΄μ λ `buffer`μ `bucket`μ μ°¨μ΄λΌκ³  μκ°νλ€.

<br/>

## νκΈ°

μ€νλ νκ³  Swift μ€νμμ€ μ½λλ λ―μ΄λ³΄λ©° μμΈμ μ°Ύμλ΄€λλ°, μμΈνκ² νμνκΈ°μλ λ΄μ©μ΄ λ§μ΄ μ΄λ ΅κ³  λ°©λνμ¬ νλ¦μ νμνλλ° μ£Όλ ₯νλ€.

κ²°λ‘ μ μΌλ‘ μΆμΈ‘μ±μ κΈμ μ μλλ°, μ‘°κΈ λ μ»΄ν¨ν° μ§μμ μκ³  μ½λλ₯Ό λ―μ΄λ³΄λ©΄ λμ± λ λͺνν κ²°λ‘ μ λ΄λ¦΄ μ μμ κ²μ΄λΌ κΈ°λνλ€. λμ CS μ§μμ΄ λ§μ΄ λΆμ‘±νλ€κ³  λ€μνλ² λκΌλ€.

```toc

```
