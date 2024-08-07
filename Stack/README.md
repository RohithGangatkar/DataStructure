A simple stack can be implemented in GO using

1]container/list package
2]slice

A stack will have below operations:
1]Push
2]Pop
3]Front
4]Size
5]Empty


1]With lock example for Slice
type customStack struct {
    stack []string
    lock  sync.RWMutex
}

func (c *customStack) Push(name string) {
    c.lock.Lock()
    defer c.lock.Unlock()
    c.stack = append(c.stack, name)
}

func (c *customStack) Pop() error {
    len := len(c.stack)
    if len > 0 {
        c.lock.Lock()
        defer c.lock.Unlock()
        c.stack = c.stack[:len-1]
        return nil
    }
    return fmt.Errorf("Pop Error: Stack is empty")
}

func (c *customStack) Front() (string, error) {
    len := len(c.stack)
    if len > 0 {
        c.lock.Lock()
        defer c.lock.Unlock()
        return c.stack[len-1], nil
    }
    return "", fmt.Errorf("Peep Error: Stack is empty")
}

