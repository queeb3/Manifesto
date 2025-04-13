# Manifesto
STRUCTURE FLOW FOR ALL CODE

A DoD look-about based on my personal journey learning how to code from scratch.

First to some who read this if any, DoD otherwise know as Data Oriented Design is a way
of thinking as well as a stylization for how to structure your code, it does not inheriently
prevent the use of OOP but it conflicts with the principles of OOD.

OOD or Object Oriented Design is the stylization most know, especially right out of college, and
is flawed in many ways that most do not grasp nor want to grasp because it would be like invalidating
years of their lifes work and money spent on a degree that teaches these principles. So, why is it flawed?

OOD operates on principles that encourages a tree like structure for defining the shape of your coding "world"
which provides the illusion that you are in fact coding a world to solve a problem, this means combining
data and logic together in the form of a class object with variables and methods. This sounds amazing on paper
and executes like sand paper, the reason being is that tree structure it enforces on you... Inheritance,
you want a tree object? inherit from foliage, which inherits from environmentItem, which inherits from
staticObject, which inherits from gameObject... I can go on but now lets throw a wrench in to this mess.
What happens if I want now a dynamic tree that can be cut, but some trees aren't allowed to be cut, because
game logic, now I need a "new tree path" for code that already exists in another path but with a inheritance
chain from DynamicObject instead of StaticObject. Like dude just make a tree struct that holds data relative
to the tree alone and add a bool or flag to it to determine if it can be cut... That is the difference between
DoD and OOD, you can still do this in OOP mind you, let me show you:

    class GameObject {}
    class StaticObj : GameObject {}
    class DynamicObj : GameObject {}
    class SEnviromentObj : StaticObj{}
    class DEnviromentObj : DynamicObj{}
    class TreeStatic : SEnvironmentObj {}
    class TreeDyn : DEnvironmentObj {}

You can see how the OOD logic falls apart here and of course people have "opinions" and think this is fine,
or they may offer "insight" as to a workaround that solves this issue... key word "workaround", why do you
need to sell me a workaround to something that can be so simply described especially since OOD and OOP are so
good and is the "industry standard". Now let me show you another way that achieves the same outcome with vastly
different qualities and performance boosts by nature:

    // again you can do DoD in OOP
    struct GameObjectData {
        bool IsStatic;
        int Id;
        // more stuff
    }
    struct EnvironmentalData {
        bool IsGatherable;
        bool IsDecoration;
    }
    class Tree {
        GameObjectData GD;
        EnvironmentalData ED;

        // Define custom logic or more data here VVVV

    }

Now with this implementation you can store just tree in its own state and work on only trees in a single loop
or many, your choice. Why would you not want to prefer the above when you can just expand the amount of data
by simply creating new structs/records/variables in place of inheritance. So what is the main advantage of this
style?

    func Cut_Tree(Player p, float range) {
        foreach(var tree in All_Trees) {
            if(tree.GD.Position - p.Pos < range) {
                p.cut(tree);
                return;
            }
        }
    }

This is of course a very rudamentory example but proves a point just as well, its isolated logic dedicated to
just a specific set of data and is only handled if the player tries to cut a tree. Of course nitpickers will
say this is inneficient because its scanning all trees, ITS an example, want it to be optimized provide a trees
in range check that constantly checks passively what trees the player is near and if any are cuttable add to
a smaller array and use that instead for whenever a player tries to cut. It's extremely simple and straightfoward,
no inheritance just logic and data defined explicitly for the use case and problem of cutting a tree.

In the beginning of this manifesto I stated that this was something I learned as progressed through coding for the
first time, let me clarify a summary of my journey to my current understanding to help envigorate you to maybe start
questioning the industries standards and best practices:

I started to learn how to be a programmer for the first time in Sept 2024, my goal? Make a fully dynamic stat generator
for a unity game idea I had for a stat collector style game that actually caused impact... Over some time working on it
I learned many things like the differences between structs and classes, how to properly use a enum, how to make a loop;
I was really entralled by the idea of being a programmer, however, every time I picked up coding again it felt tedious
to try and code using OOD it just always felt confusing even when I did start understanding some of it, this time felt
different for some reason, as if I knew a change was coming... After about a month of working I discovered a video on
ECS that talked about DoD for the first time in my life something made a little more sense with code speak, I do not
know why but what they were saying just made sense in my head and sounded logical and reasonable for how a copmuter
should act on and read data. So I started to change my stat system into a standalone ECS style stat generator, of course
I was still using OOP and OOD to do it because I didn't at the time fully grasp the usage concepts even though I knew
what they were saying. Iteration after iteration I coded for 8+ hours a night with many refactors, which I've grown to
love doing, and yet I just could not make the stat gen work and I gave up on the idea... I did NOT give up on programming
this time and instead I made a new project for just a ECS engine in C# and got the first generic based ECS working with
a shit ton of Dictionaries and Queues... it was shit and ran like it too, BUT I learned and decided to scrap it and start
over again... and again.... again, I made a total of 5 working ECS in C# and made small test games with them
(console+logic) and it was soooo much fun. My fifth implementation was my best so far utilizing unsafe code to make
custom allocators and byte based buffers with direct casting for the best cache locality I could attempt for my
knowledge. It was pushing logically 50 million plus entities a second with 10-15 components structs and this was with
AoS and not SoA beacuse of its generic nature without source generation.

So when I say "I learned how to program" I literally learned how to program in 6 months to that level with absolutely
0 formal eduction, no mentor aside from talks by Casey and Acton, and no tutorial EVER just sheer will and trial by fire,
*cough* "error", and to top it off I was using OOP because it was C# and OOP is enforced with C#, however I fully went
about internalizing and truly learning DoD in and out to make sure I was getting better.

So sorry for the long exposition, but as a notation to what I truly mean by learned to program, here is a comprehensive
understanding of MY understanding of what programming looks like in my head, as this is my manifesto to me and to
those who want to be on a journey to DoD enlightenment haha.


# USER
Pretty self explanatory... its the input you will recieve externally into your solution
to a problem you are solving for the user or client.

- data = input
- system = state given from data
- where = stored on stack per frame
- when = instant and first
- how = read from OS IO or api or packets, however you get data (ie. glfw)
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

    If OOP is so good, why is your class hierarchy slower, harder to refactor, and more error-prone than my
    flat struct with 4 floats?


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
