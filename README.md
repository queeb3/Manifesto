# Manifesto + Bio
STRUCTURE FLOW OF ALL CODE FOR DATA NOT OBJECTS

## Intro
A DOD look-about based on my personal journey learning how to code from scratch along with the
lessons ive learned about code along the way through trial and error.

This is first and foremost a manifesto to myself and to those who want to adopt a
better way of thinking about code and hardware as one entity together rather than obfuscating
and abstracting as far away as possible from the very thing that runs your damn code.

### DOD OOP OOD:
First to some who read this if any, DOD or Data Oriented Design is a way of thinking as well
as a stylization for how to structure your code, it does not inheriently prevent the use
of OOP but it conflicts with the principles of OOD.

DOD is a focus on data specifically what, how and where... We are first problem solvers above all else,
when we write code or program we are being very intentional in what it is we wish to accomplish.

So when you look at the issue and want to find a solution under DOD you first determine what the problem
is and what data that problem represents. If a problem is really large? If you came from college you should
know about making larger problems into smaller ones that are easier to understand and decide what to do with,
DOD is basically that but on crack for data.

OOP is what pretty much everyone in the industry uses and understands, for those who are new, here is a quick
understanding. You are to define and describe in code what an object is, this is done through determining the
problem and deriving objects you think you'll need through data and logic and this will be placed inside of
a class which is stored on the heap in most languages.

OOP is compatible with DOD, however, most people do not use it with DOD in mind they'd rather fuse data and
logic into an object parading itself as a "Real world noun" that represents what it defines itself to be,
self containing all logic and all its own personal data, this is called OOD and it causes a massive
issue for the hardware.

OOD or Object Oriented Design is the stylization most know, especially right out of college because it gets
bundled as required for OOP to work, this is a lie.

OOD is flawed in many ways that most do not grasp nor want to grasp because it would be like invalidating
years of their lifes work and money spent on a degree that teaches these principles. So, why is it flawed?

### The Underlying Issues
OOD operates on principles that encourages a tree like structure for defining the shape of your coding "world"
which provides the illusion that you are in fact coding a world to solve a problem, this means combining
data and logic together in the form of a class object with variables and methods. This sounds amazing on paper
and executes like sand paper, that tree structure it enforces on you is called...

### Inheritance (Tree Class Graph)
Inheritance,you want a tree object? inherit from foliage, which inherits from environmentObj, which inherits from
staticObject, which inherits from gameObject... I can go on but now lets throw a wrench in to this mess.

What happens if I want now a dynamic tree that can be cut, but some trees aren't allowed to be cut, because
game logic, now I need a "new tree path" for code that already exists in another path but with a inheritance
chain from DynamicObject instead of StaticObject. Like dude just make a tree struct that holds data relative
to the tree alone and add a bool or flag to it to determine if it can be cut...

That is the difference between DOD and OOD, you can still use OOP for DOD mind you, let me show you some versus examples:
```C#
class GameObject {}
class StaticObj : GameObject {}
class DynamicObj : GameObject {}
class SEnviromentObj : StaticObj{}
class DEnviromentObj : DynamicObj{}
class TreeStatic : SEnvironmentObj {}
class TreeDyn : DEnvironmentObj {}
```
You can see how the OOD logic falls apart here and of course people have "opinions" and think this is fine,
or they may offer "insight" as to a workaround that solves this issue...

Key word "workaround", why do you need to sell me a workaround to something that can be so simply
described especially since OOD and OOP are so good and is the "industry standard".

Now let me show you another way that achieves the same outcome with vastly different qualities and performance
boosts by nature:

### DOD (Composition data only)
```c++
// again you can do DOD in OOP
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
```

---

Now with this implementation you can store just tree in its own state and work on only trees in a single loop
or many, your choice.

Why would you not want to prefer the above when you can just expand the amount of data by simply creating
new structs/records/variables in place of inheritance.

#### Example Loop Func
So what is the main advantage of this style?
```c++
void Cut_Tree(Player p, float range) {
    foreach(var tree in All_Trees) {
        if(tree.GD.Position - p.Pos < range) {
            p.cut(tree);
            return;
        }
    }
}
```

This is of course a very rudamentory example but proves a point just as well, its isolated logic dedicated to
just a specific set of data and is only handled if the player tries to cut a tree.

Of course nitpickers will say this is inneficient because its scanning all trees, ITS an example, want it to
be optimized provide a trees in range check that constantly checks passively what trees the player is near and
if any are cuttable add to a smaller array and use that instead for whenever a player tries to cut.

It's extremely simple and straightfoward, no inheritance just logic and data defined explicitly for the use case
and problem of cutting a tree.
---
Some closing statements before we move on.

### What DOD is not:
- It's not procedural.
- It's not anti-OOP.
- It's not an immediate fix. (you still need to write good code)
- It's definitely not "less readable".
- It's not just performance, it's controlling flow for performance.
- And it does not scale poorly at size or make code harder to maintain, quite the opposite.

DOD is great but its only as good as you make your flow and how tightly you can control where and how you
data is accessed in your program. This does not make it hard, even if it feels like it at first if you are
coming from OOD, but I promise you the moment you get it, you get it forever and you won't be going back.

If you are ready to shift your perspective and dive deeper into the rabbit hole I highly encourage researching
blogs and videos on it. Personally I was deeply inspired to pick up coding again because of a cppcon talk by
Mike Acton where he discusses DoD and ECS in great detail and everytime I go back to rewatch I always come away
with some new knowledge that was hidden under the insights he had to offer.

Now I would like to provide some background as to how I even got started down this path, a time frame dislaimer,
I have "coded" before but in reality I was just a unity script kiddy that jumped between projects every other year.
I first learned of code through GameMaker Studio way back when I was in middle school and had been infatuated since...

Anyways, you don't care about my personal history, you are here for how I can so boldy claim to make a manifesto
when I have no background. So I say to that...


```
*Disclaimer*: I am not claiming to be a god of programming nor a "good programmer" just highlighting objective
observations I made during my journey and how its shaped my mind and perspectives around code.
```
# My Journey to understanding and becoming a Programmer
In the beginning of this manifesto I stated that this was something I learned as progressed through coding for the
first time, let me clarify my journey to my current understanding to help invigorate you to maybe start
questioning the industries standards and best practices:

## The Start
#### Month Sept 2024
I started to learn how to be a programmer for the first time in Sept 2024, my goal? Make a fully dynamic stat generator
for a unity game idea I had for a stat collector style game that actually caused impact... Over some time working on it
I learned many things like the differences between structs and classes, how to properly use an enum, how to make a
"proper loop" heh.

I was really entralled by the idea of being a programmer, however, every time I picked up coding again it felt tedious
to try and code it just always felt confusing even when I did start understanding some of it, this time though, felt
different for some reason, as if I knew a change was coming...

#### November
After roughly a month of working I discovered a video on ECS that talked about DOD for the first time in my life
something made a little more sense with code speak, I do not know why but what they were saying just made sense in my
head and sounded logical and reasonable for how a computer should act on and read data. So I started to change my stat
system into a standalone ECS style stat generator, of course I was still using OOP and OOD to do it because I didn't at
the time fully grasp the usage concepts even though I knew what they were saying.

Iteration after iteration I coded for 8+ hours a night with many refactors, which I've grown to love doing, and yet I
just could not make the stat gen work and I gave up on the idea...

Notable Learning:
- enum as flags
- differences between class/struct/record
- separation of concerns
- funny but, preplanning system architecture

#### Nov -> 2025
I did NOT give up on programming this time and instead I made a new project for just a ECS engine in C# and got the first
generic based ECS working with a shit ton of Dictionaries and Queues...

It was shit and ran like it too, BUT I learned and decided to scrap it and start over again...
and again.... again, I made a total of 5 working ECS in C# and made small test games with them (console+logic)
and it was soooo much fun.

Notable Learning:
- bitwise operations
- struct only as data
- got rid of all inheritence
- honed in scope creep
- store all like data in one array per type
- structure a pipeline of logic flow
- dependency injection
- Array of structs vs Struct of arrays
- Cache layouts/lines/locality
- CPU L1/L2/L3 vs RAM access
- hot and cold paths
- hot data needs to be isolated from any cold data
- meta categorizing through id and bi directional lookups
- some reflection
- i hate generics in c#
- GC overhead and managed vs unamanged
- there are more but ill save it...

these are not buzzwords this is literally what i learned during this timeframe.

#### Start of Feb
My fifth implementation was my best so far utilizing unsafe code to make custom allocators and byte based buffers with
direct casting for the best cache locality I could attempt for my knowledge.

It was pushing logically 50 million plus entities a second with 10-15 components of varying byte size and this was with
AoS and not SoA beacuse of its generic nature without source generation.

##### End of Feb -> April
This can be bullet pointed because it combines most of what i did in Feb through early April.

Notable Learning:
- Unsafe C#
- Pointer arithmatic
- pointers vs addresses
- pointer casts to ref conversion
- type reinterpretation
- void* buffers manually heap allocated with marshal
- controlled memory
- arena/allocators/stack buffers(struct with fixed[])
- literally made a custom flat dictionary with custom hash logic and flat arrays indexed with bitwise indexing
    using an encoder/decoder based on array of ulongs where each bit represented a occupied index in another array :D
- decided fighting C# language limitations wasnt worth my headaches and switch to C++, best decision ever...
- "learned" general C++ in a week and started making a UI Engine for a txt editor app with glad and glfw to
    read input and render text and backgrounds. 60% finished just need rendering side and some textures.

Till today now a little under 7 months from starting to program... like actually start this time.
---

### Finish
So when I say "I learned how to program" I literally learned how to program in 6 months to that level with absolutely
0 formal eduction, no mentor aside from talks by Casey and Acton, and no tutorial EVER just sheer will and trial by fire,
*cough* "error", and to top it off I was using OOP because it was C# and OOP is enforced with C#, however I fully went
about internalizing and truly learning DOD in and out to make sure I was getting better.

I didn’t follow a course, I followed my curiosity, Every failure taught me something specific, new and tuned to what I
wanted to acheive as a programmer. (trial by error)

Every rebuild made it cleaner, Every limitation pushed me into deeper waters always forcing me to rethink EVERYTHING,
all the time. (my refactors)

If I had waited for the perfect time or right amount of watching youtube, I wouldn’t have started I would've just sat
in my void of space endlessly watching something I was passionate about without any pursuit.

It was and still is my obsession to write good, clean and most of all performant code by thinking like a CPU...D.O.D


## The Jounery's Lessons Taught
So sorry for the long exposition, but as a notation to what I truly mean by learned to program, here is a comprehensive
understanding of MY understanding of what programming looks like in my head, as this is my manifesto to me and to
those who want to be on a journey to DOD enlightenment haha.

I would like to add I actually got fed up with dealing with OOP limitations and specifically the limitations of C#
I ended up switching my main language to C++, which I instantly started making a UI engine as my first project.

This is why you will see C# and C++ code snippets but for the most part the snippets are interchangable.

# USER/PROBLEM
Pretty self explanatory... its the input you will receive externally into your solution
to a problem you are solving for the user or client.

## Data
The input given by the user or some way or another acquired through any means.

This represents a change in some state that the user wishes to impact, in terms of gameplay logic:
- User wants to move a character so they will input Key_W
- User wants to sprint and jump over a hole, input is Key_Shift && Key_W && Key_Space

This can also be applied to any input... ie UI:
- Press button: input = mouse position, is hovering, has pressed, button visible, button released -> do logic

It is your job to take in this input and process it to allow the intended functionality to occur,
this is your problem that you must solve.

#### Side Note
You can also be the user defining your own problem and solving it, this is what you create when you
have explicit functionality inside a product or app, a user wont know there is a bounds or position to a button,
but you know you need that data so you created it to allow it to be rendered at some spot in screen space for
your app.

## System
The logic you implement to convert input to state data that will cause a change in state for the program's
memory.

This can be be converting the mouse movement on screen to camera movement in a game, this is a change in state
for the camera position and angle, as well as a change in render state which is further down the flow.

## Where
Prefer keeping input state as a per frame state, this will allow modifications to proceed smoothly without
worrying about corrupting internal memory as all new input overrides all old inputs.

There are circumstances where input data translates to stored data without causing a change in state, in these
cases you have something called a database :D, where the state reflected is the state captured upon input and
most likely will get pushed to disk by some save state call.

If you are working in realtime apps that run in a loop and not a on demand basis, if you must store input
states through frames, I would recommend creating a in function buffer, queue, or stack that simply holds
X number amount of past frame states preferably stack only without pushing frame states to heap to avoid
fragmentation and CPU churn.

Summary of where's, as most prefered to least:
- Per frame
- In entry point as single or buffer of history snapshots (stack alloc)
- Heap only if it is state that must be captured for long life executions
- Disk you are probably making a database

## When
This is the first thing you do in your loop aside from if you are using external tools that require priority.

Input is always the first piece of data to enter and last to change because its the mutation factor altering
your stored data.

I would like to add in the case of input data becoming stored data, they are mainly three different things:
- Incoming data is stored as the main data or used to alter the data already stored.
- Stored data is data given, saved for later use directly from input.
- Outgoing data is previously input state data that has been requested, does not always mean destroyed.

## How
This depends on what program/problem you are trying to solve, which leaves this quite ambiguous but I can offer some
insight into how to handle receiving input.

Methods of input:
- Hardware
- Service
- Packets
- API requests
- Database Queries
- Disk IO
- many many many more ways to receive data

In all these cases your job is to find out what the best AND smallest representation of that data you can make.

Some data may come fully packaged already and all you need to do is parse the pieces you need, why store what you aren't
using after all. Make a struct and add the parameters you wish to keep and call it UsefulInputdata or something based on
your desired naming conventions.

Then you would want to start pushing it through your logic pipeline to extract, store, process all the little pieces of the
important bits that you care about and that is the end of the life cycle for this specific input.

#### Simplified
- data = input
- system = state given from data
- where = stored on stack per frame (prefer)
- when = instant and first
- how = read from OS IO or api or packets, however you get data (ie. glfw)
- error = none because it should be strictly controlled whats allowed in your solution at the get-go

# SERVICE/SOLUTION
Services are the solution to the problem you are attempting to solve through programming.

Data acts as the state of the problem while systems are the helpers that alter the data,
to ensure data stays correct and current for the problem being given(input).

A service is basically a flow of logic through functions that take in input as parameters and
gives you an output or alters already existing data to an outcome you can use and deliver as
the solution.

## Data
Services take in data rather that hold data for long term. The data received depends on what
the service you are making is meant to work on.

Your entire program is a service but at a large scale, if you shrink all problems down to their
smallest form you get a few different types of services.

Here are a few examples:

#### App
```c++
int main(){
    App app;

    app.Load();
    while (app.Active)
    {
        // insert any higher priority api here
        app.Process();
    }

    app.Unload();
    return 0;
}

```
#### Pipeline
```c++
struct App{
    Input in;
    Data data;
    RenderPipe rp;

    bool Load(const Input &i);
    void Process();
    void Unload();
};

struct Data{ // AoS style storage of multiple data streams
    Buffer SomeData[];
    Buffer OtherData[];
    Buffer MetaData[];
    Buffer RenderData[];

    bool Init_Data();
    void Update();
};

struct RenderPipe{
    Buffer renderthese[];
    Buffer commands[];

    bool Init_Render();
    void Render();
};
```
#### Function
```c++
void App::Process()
{
    in.mouse.Update();
    in.keyboard.Update();

    data.Update(in.mouse.state, in.keyboard.states);
}
```
#### Read Write
```c++
bool Data::Init_Data()
{
    // read some defaults or config or set inital states

    SomeData = config.somedef;
    OtherData = other.Load();
    MetaData = SomeData.GetMeta();
    RenderData = SomeData.GetRenderData();

    // alternatively populate with file reads from source directory or database
}
```

## System


## Where


## When


## How


## Errors


#### Simplified
- data = state or defaults
- system = convert input data to data state change
- where = long lived on heap or stack ouside frame refresh loop(top of main entry or app struct)
- when = every new frame persistent += new change
- how = function calls that process input to new data or mut data predictibly
- error = return empty or no data change and move to next proc call

# ACTIONS
The course of flow on how an app or process should execute such that it causes minimal waste
for the hardware.



#### Simplified
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





#### Simplified
- Main = your entry point and where the stack begins

- Clean = save state and unload memory
- Loop = process all stored data based on input
- Load = load key data, can be things like config or file paths

- Process = systems that act on input to change data
- Store = where or how data is stored based on input
- Input = how you would like to receive you data
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



#### Simplified
(Stream = thread or pipeline)

1. receive input data
2. Determine which stream it should follow
3. Grab any data that the new state will affect
    - This to can follow these steps for individual function calls as each function is a flow.
4. Mutate or make new data
5. Handle potential errors with return values or inline logic to correct corruption
6. Return or store transformations

# DATA STORAGE:


# MULTI-THREADING:


# ERROR HANDLING:
