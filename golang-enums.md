# Enums In Golang

Enums are a useful feature of C and you can bring them into Go by combining the `type` and `iota` features.

For a basic example you can make an enum to hold all the states of a state machine.

    type State int

    const (
        init_state State = iota
        button_pressed
        lever_pulled
        final_state
    )

This code defines a type State and gives it an underlying type `int`. Then the `const` defines our states. By using `iota` each state after the first is defined implicitly as:

    button_state State = ioto + 1

`iota` by default starts at 0, and with the underlying type being `int` this makes each following state one larger then the last.

This can also be done with strings by adding a `String()` method to the `State` type.

    func (s State) String() string {
        switch s {
            case init_state:
                return "init"
            case button_pressed:
                return "pressed"
            case lever_pulled:
                return "pulled"
            case final_state:
                return "final"
        }
        return "unknown"
    }

You can also make default values for your enums by using the first value for the default like:

    const (
        Undefined State = iota
        init_state 
        button_pressed
        lever_pulled
        final_state
    )

Now you can do error checking for undefined values in `State`, like

    if current_state == Undefind {
        // some error
    }
