<div align="center">
<h1>rescript-hooks-testing-library</h1>

<img src="https://raw.githubusercontent.com/testing-library/react-hooks-testing-library/main/public/ram.png">

ReScript bindings for [`react-hooks-testing-library`](https://github.com/mpeyper/react-hooks-testing-library).

</div>
<hr/>

## Installation

`npm install --save-dev rescript-hooks-testing-library`

Then add `rescript-hooks-testing-library` to `bs-dev-dependencies` in your `bsconfig.json`:

```json
{
  "bs-dev-dependencies": ["@glennsl/bs-jest", "rescript-hooks-testing-library"]
}
```

## Example

```reason
open Jest
open Expect
open Testing

type counterType = {
  counter: int,
  set: (int => int) => unit,
}

let useCounter = initial => {
  let (counter, set) = React.useState(() => initial)
  {counter: counter, set: set}
}

describe("useCounter", () => {
  open Result
  let container = renderHook(() => useCounter(0), ())
  test("counter is 0", () => expect(container.result.current.counter) |> toEqual(0))
  test("counter is 1", () => {
    act(() => container.result.current.set(prev => prev + 1))
    expect(container.result.current.counter) |> toEqual(1)
  })
  test("counter is 2", () => {
    act(() => container.result.current.set(prev => prev + 1))
    expect(container.result.current.counter) |> toEqual(2)
  })
})


```
#### More usage examples
1. [Tests](https://github.com/glebskr/rescriot-hooks-testing-library/tree/master/__tests__)
2. [react-hooks-testing-library documentation](https://react-hooks-testing-library.com/)
