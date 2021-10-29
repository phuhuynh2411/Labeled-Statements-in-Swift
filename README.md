## Labeled Statements in Swift

In Swift a labeled statement is a string followed by a colon before the statement it will refer to. It can be applied to the control flow elements (conditional or loop statements). It's also be applied to the `do` without `catch` like an example below.

```swift
outer: do {}
```

I will explain in details about the above block of code later in another section of this article.

### Label with conditional statement

You often see that when using a `if`, you just simply type 

```swift
if condidtion {}
```

In a codebase, it's rarely to see an `if` statement with a label.

```swift
outer: if condition {}
```

I named the above label as 'outer', but you can type anything. Actually, it cannot be any text here. It must be followed the rules that you write a variable in Swift. If you add a second word to the above label 'outer inter', the complier will prompt an error.

You could use a label with a `if` statement in case you would like to break the scope at center point. Here is a example code. At the time of writing this article, I don't find any use case of it. If you do, please send me a message through Twitter.

```swift
outer: if condition {
    if condition2 { break outer }
    let foo = 2
}
```

With the label the `break` keyword now supported in the conditional statement. You might find its use cases yourself in some situations in your project.

### Label with loop statement

Suppose you have something like two nested loops shown below, and you need to break the outer loop in side the inner loop.

```swift
outer: for i in 0..<3 {
inter: for j in 0..<3 {
    if j == 2 { break outer }
    }
}
```

Without the label, you cannot break the outer loop. If you use the `break` keyword by itself, it only breaks the inner loop. Can I use `continue` here? The answer is 'yes'. Swift is really powerful, isn't it?

```swift
outer: for i in 0..<3 {
inter: for j in 0..<3 {
    if j == 2 { continue outer }
    }
}
```

### Label with loop and switch statement

A useful use case when you use a loop as a outer scope and a `switch` as an inner scope.

```swift
outer: for i in 1..<3 {
    switch bar {
    case .bar1: break outer
    case .bar2: print("bar2")
    }
}
```

In this case, if you don't use the label, you will have no way to break the outer loop inside the case of the switch statement. The 'break' without the label will break the switch case instead of breaking the outer loop.

### Do without the Catch statement

I occasionally see the 'do' without 'catch' in the codebase, but maybe you see it often in your project. 'Do' introduces a new scope of code, and combination with a label, you can break out of that scope.

```swift
newScope: do {
    print("do")
    break newScope
}
```

If you don't add the label 'newScope', you would get a complier error, and the break statement doesn't make any sense.

### Conclusion

The labeled statement can come in handy in case you would like to break a scope at a given point. I hope you found this article useful, and if you have any questions or comments, feel free to contact me via Twitter.
