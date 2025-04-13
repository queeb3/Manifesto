# Manifesto
STRUCTURE FLOW FOR ALL CODE

# USER
Pretty self explainetory... its the input you will recieve externally into your solution
to a problem you are solving for the user or client.

- data = input
- system = state given from data
- where = stored on stack per frame
- when = instant and first
- how = read from os IO or api that allows the same (glfw)
- error = none because its strict controlled whats allowed to interact

# SERVICE
Services are the solution to the problem you are attempting to solve through programming.
Data acts as the state of the problem while systems are the helpers that alter the data,
to ensure data stays correct and current for the problem being given(input).

- data = state or defaults
- system = convert input data to data state change
- where = long lived on heap or stack ouside frame refresh loop(top of main entry or app struct)
- when = every new frame persistent += new change
- how = function calls that process input to new data or mut data predictibly
- error = return empty or no data change and move to next proc call

# ACTIONS
The course of flow on how an app or process should execute such that it causes minimal waste
for the hardware.

- input
- store data
- process data
- handle errors
- change states
- act on state (render and logic)
- repeat

# LAYERS
Layers depend on what kind of depth you are seeking or how high you wish to build instead of wideness
in cases of wideness you get more bang for you buck due to being able to scale infinitely wide while
still maintaining good performance but the taller you go the more indirection is introduced causing
slow downs that are hard to reason about because logically the flow is the same but in the eyes of
hardware you are introducing arbitrary steps it needs to take to get to where it needs to go.

prefer building bottom up instead of top down it will make your life much easier if you know what your
lowest point will be before you dig yourself a pit that cannot be escaped with more depth.

- Main = your entry point and where the stack begins

- Clean = save state and unload memory
- Loop = process all stored data based on input
- Load = load key data, can be things like config or file paths

- Process = systems that act on input to change data
- Store = where or how data is stored based on input
- Input = how you would like to recieve you data
- Data = what do you actually need to solve the problem you are working on
    - This can be as much and as many as you need or want but dont go any lower in depth for data or you
    run into making a chain of hierarchies which will start to hurt you in the long run, prefer putting
    other data inside new data if you need common functionality this can be through general purpose utility
    data that is meant to live in other data or one off variables with common relatives in other data.
    (composition = wideness | inheritence = depth at this level).

    Composition:

            struct XY { float x, y};

            struct Box {
                XY topRight;
                XY bottomLeft;
            };

    VS Inheritance:

            class Point { float x, y; }

            class Bounds { Point TopR, BottomLeft; }

            class Box : Bounds {} // <--- why prefer extra code
            class Circle : Bounds {} // <--- doesnt work in this case and needs new logic... more code


# LOGIC FLOW
Logic should always be handled top down towards the final process call that holds the highest mutation
count for individual data. when a  new frame is to start, ensure all data being processed is current and
accurate to intended state via combining threads at the end before the final call is issued for simulation
or rendering.

(Stream = thread or pipeline)

1. Recieve input data
2. Determine which stream it should follow
3. Grab any data that the new state will affect
    - This to can follow these steps for individual function calls as each function is a flow.
4. Mutate or make new data
5. Handle potential errors with return values or inline logic to correct corruption
6. Return or store transformations

# DATA STORAGE:


# MULTI-THREADING:


# ERROR HANDLING:
