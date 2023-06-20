# RxJs
Reactive programming using Observables. Easy to compose async or callback based code

Set of operators to transform, filter, and combine streams of data. Declarative programming

## Observables

Stream of data over time. Emit multiple values async.

- `Observable.create()`
- `of(obj)`, `from(obj)`, `interval()`

## Subscribers

Consumes values emitted from observables.

- `subscribe()` uses a callback
- Import `{of}` from 'rxjs'

```javascript
const observable = of(1, 2, 3);

observable.subscribe(
    value => console.log(value),
    error => console.log(error),
    () => console.log('Complete')
);
```

## Operators

- Map
- Filter
- Take
- Merge
- Concat
- SwitchMap

Operators use pipe syntax.

Map operator takes the emitted value as input and performs a transformation on it, emitting the transformed value.

Filter takes the emitted value and emits that value if a certain condition is true.

Concat combines multiple observables sequentially, waiting for each one to complete before moving to the next.

```javascript
const source1 = of(1, 2);
const source2 = of(3, 4);

const result = concat(source1, source2);

result.subscribe(value => console.log(value)); // 1, 2, 3, 4
```

Merge combines multiple observables async, completing in order each observable complete
```javascript
Const source1 = of(1,2);
Const source2 = of(3,4);

Const result = concat(source1, source2);
result.subscribe(value => console.log(value) //1,3,2,4
```
```javascript
observable.pipe(
    filter(value => value%2 === 0)
    map(value => value * 2)
).subscribe(value => console.log(value)
```
Order of operators determine the sequence of transformations
Operators are composed using pipe method to chain multiple transformers
Data flows left to right. Each operator processing se quencially 

## Subjects
Both observables and observers. Used to multicast
next(), error(), complete() are used to emit or complete the stream
Subject, BehaviourSubject, ReplaySubject, AsyncSubject
```javascript
Import {Subject} from ‘rxjs’

Const subject = new Subject<number>();
subject.subscribe(value => console.log(‘subscriber 1’, value);
subject.subscribe(value => console.log(‘subscriber 2’, value);
subject.next(1)
subject.next(2)
```
—---

## forkJoin 

Combines emission of multiple observables and wait for all to complete. Emits last value for each in the same order provided. 
```javascript
Const source1 = of(1,2,3)
Cons source2 = of(‘A’, ‘B’, ‘C’);
forkJoin([source1, source2]).subscribe(res => console.log(res)};
// [3, ‘C’]
```
## combineLatest

Combines emission of multiple observables into array of projection. Emit value time any of its provided observables emit value, Combines the latest emitted values from each observable
```javascript
Const source1 = of(1,2,3)
Cons source2 = of(‘A’, ‘B’, ‘C’);
forkJoin([source1, source2]).subscribe(([s1, s2]) => console.log(s1, s2)};
// 1, ‘A’
// 2, ‘A’
// 2, ‘B’
```
## Zip
Combines emission of multiple observables and emit once every source observable emit

## Merge
Combines emission… emit values as they arrive from any observable


