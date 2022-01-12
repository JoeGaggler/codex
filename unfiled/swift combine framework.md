#todo - how to avoid retain cycles when implementing a custom `Publisher`

-----

call `publisher.subscribe` , providing itself as the subscriber
publisher creates subscription, passes it to subscriber via `receive`
subscriber calls `request` to initiate demand (can call again later?)

subscription calls `receive` on subscriber to handle new value
subscriber returns new ADDITIVE demand to subscription

-----

Publisher

```swift
protocol Publisher {
    associatedtype Output
    associatedtype Failure : Error
    
	func receive<S: Subscriber>(subscriber: S) where 
		Self.Output == S.Input
		Self.Failure == S.Failure		      
}
```

typically a struct? does not require identity
do not call `receive(subscriber:)` - supposed to call `subscribe(_:)` instead.

-----

Subscription

```swift
public protocol Subscription : Cancellable, CustomCombineIdentifierConvertible {

    /// Tells a publisher that it may send more values to the subscriber.
    func request(_ demand: Subscribers.Demand)
}
```

must be classes
strong reference to the subscriber, freed when cancelled

-----

Subscriber

```swift
public protocol Subscriber : CustomCombineIdentifierConvertible {
    associatedtype Input
    associatedtype Failure : Error

	func receive(subscription: Subscription)
    func receive(_ input: Self.Input) -> Subscribers.Demand
    func receive(completion: Subscribers.Completion<Self.Failure>)
}
```

-----

Subscribers.Demand

```swift
.unlimited
.max(_ value: Int)
.none // same as `max(0)`
```
