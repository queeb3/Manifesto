# Manifesto
    STRUCTURE FLOW FOW ALL LOGIC
    
USER:
    - data = input
    - system = state given from data
    - where = stored on stack per frame
    - when = instant and first
    - how = read from os IO or api that allows the same (glfw)
    - error = none because its strict controlled whats allowed to interact
SERVICE:
    - data = state or defaults
    - system = convert input data to data state change
    - where = long lived on heap or stack ouside frame refresh loop(top of main entry or app struct)
    - when = every new frame persistent += new change
    - how = function calls that process input to new data or mut data predictibly
    - error = return empty or no data change and move to next proc call
ACTIONS:
    - input
    - store data
    - process data
    - handle erros
    - change states
    - act on state (render or logic)
    - repeat
    
LAYERS:
    _layers depend on what kind of depth you are seeking or how high you wish to build instead of wideness
        in cases of wideness you get more bang for you buck due to being able to scale infinitely wide while
        still maintaining good performance but the taller you go the more indirection is introduced causing
        slow downs that are hard to reason about because logically the flow is the same but in the eyes of
        hardware you are introducing arbitrary steps it needs to take to get to where it needs to go_
    /prefer building bottom up instead of top down it will make your life much easier if you know what your
    lowest point will be before you dig yourself a pit that cannot be escaped with more depth\
    
    Key Layers:
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
                (composition = wideness | inheritence = depth at this level)
