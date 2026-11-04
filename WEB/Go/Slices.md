In go a good way of using arrays is using Slices.
A go Slice is essentially a small structure that contains three fields 
```go
type SliceHeader struct {
    Data *string // Pointer to underlying array
    Len  int     // Number of elements
    Cap  int     // Capacity
}
```
So when we are using the [low:high] operator, we are not cloning the whole array, but we're creating a new slice header with different components.

