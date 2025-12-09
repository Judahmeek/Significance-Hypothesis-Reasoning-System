# Significance-Hypothesis-Based-ARC-AGI-2-puzzle-solver
#### Desperately seeking feedback and contributors!!! I'm smart, but I'm not Einstein

This is a Draft Specification for a proof of concept for specifying how humans solve problem, restricted at the moment to ARC-AGI-2 puzzles. Implementation to begin probably today (First, I want to check the ARC-AGI Discord for solutions to the few puzzles that I couldn't solve, and then I'm considering running through the Solution Specification process for another puzzle before beginning implementation.) 

**Collaboration Platforms:**
**Slack:** Join me on [a dedicated Slack workspace](https://join.slack.com/t/shbarcagi2puz-int9037/shared_invite/zt-3k0qx6oly-SvinliPi8bjFCNjbP1AcJQ) to discuss this project  
**Github:** Join me on [Github](https://github.com/Judahmeek/Significance-Hypothesis-Based-ARC-AGI-2-puzzle-solver) to actually begin the process of implementing the puzzle solver and test suite.  
**Google Docs:** If you would like to just quickly view the Specification Document and send me some suggestions, you can do so through [Our Google Document](https://docs.google.com/document/d/1wYJyRsPdqNkTecePCfWnnby70mRbmoS4XpySJp_BhC0/edit?usp=sharing).

**Problem Domain:** 
Current artificial intelligence (AI) reasoning systems score low on ARC-AGI-2 because the challenge is specifically designed to expose their weaknesses in novel visual reasoning, compositional reasoning, and contextual rule application, whereas earlier versions of the benchmark were susceptible to brute-force methods and pattern matching from training data. Unlike ARC-AGI-1, every task in the newer benchmark is unique, demanding a deeper, human-like understanding of concepts rather than just recognizing or adapting pre-learned patterns.  
**Specific challenges of ARC-AGI-2**:

* Novelty: Every ARC-AGI-2 task is entirely unique, and models cannot solve them by finding similar patterns in their training data, a weakness that was exploited in ARC-AGI-1.  
* Complex composition: Tasks require applying multiple rules simultaneously, and even rules that interact with each other, which is something current systems struggle with.  
* Symbolic interpretation: AI models often fail to understand the symbolic meaning behind visual elements, only analyzing superficial patterns, as seen in tasks requiring the interpretation of symbols with semantic significance.  
* Contextual application: Systems have difficulty applying rules differently based on the context of the task, instead tending to apply a single rule in a fixed way.  
* Inability to adapt: The benchmark is designed to prevent models from overcoming problems with sheer computational power or brute-force approaches, forcing them to solve tasks efficiently and adapt to new situations in a way that mimics human problem-solving strategies.

**Intent:** Go through a number of the ARC-AGI-2 training set problems & document my personal organic solution process until the solution process can be abstracted into a competitive problem solver.  
Implement the abstracted solution process & test it on the remaining problems & ARC-AGI-2 evaluation set (and other similar significant benchmarks, such as those listed here: [https://news.ycombinator.com/item?id=45964748](https://news.ycombinator.com/item?id=45964748))

**Enlightening Human Tool Search Experience:** When trying to pull a stuck sock out of a vacuum hose, I searched for various tools after being able to think of an accessible version of the first, most obvious tool I thought of (a hook). After trying to use other tools (an umbrella to push the sock through the hose, a chopsticks like measuring device, a serrated knife, a two-pronged meat skewer, pliers which proved too wide for the hole, tweezers which were far too small), I expended more cognitive effort on possible hooks & realized that I had some appropriately shaped dental hygiene tools. (My search heuristics repeatedly swapped between searching specific locations for possible tools & searching possible locations for specific tools)

**Syntax:**

* **Significance Hypothesis**: a hypothesis that a relationship between two entities is significant to solving the puzzle  
* \~\~\~X\~\~\~ represents a meta TODO comment for improving this document  
* **Pattern Recognition (X)**: Basically a stubbed tool call for pattern recognition logic that is essential, but beyond me at the moment

**Glossary:**

* **Naivety Check Aspects:** number, directionality, color, proximity, preference for relationships not involving the puzzle borders, constants (If not for the guarantee of the puzzle graph itself or the guarantee of the density of the squares, I wonder how abstract we could get? 😂)  
* **Constant Colors**: a constant color is defined by the lack of any change in number or position of squares of the same value between input & output graphs  
* **Variable Colors**: a variable color is every color that is not constant, a.k.a. changes in number of position between input & output graphs  
* **Inputs**: squares of a variable color that exist in the input graph  
* **Outputs**: squares of a variable color that exist in the output graph  
* **Constants**: Inputs that match the general location & shape or relational constraints of a constant color piece in another example \~\~\~Still needs work\~\~\~  
* **Experimental Constraint**: a relationship that remains true across all examples or all example and test input graphs that may be encoded in our rules, reducing possible abstraction  
* **Belief**: a hypothesis with high significance, which is awarded to hypotheses that satisfy one or more predictions  
* **Isolate**: The prediction of application of all beliefs to a minimal group of inputs  
* **Piece**: a group of squares of the same color that are near each other, as defined by the relevant starting significance hypothesis

**Heuristics:**

* **Search**: From simple to more complex. For graph search specifically, top to bottom, left to right  
* **Relationship Complexity**:  
  * Order from simplest to most complex is aspects of a piece, equation of the aspect of a piece to the same aspect of another piece, etc…  
  * Determining the order from simplest to most complex will be an ongoing task.  
  * To avoid combinatorial explosion, search limits must be placed at each level as well as search limits on the number of levels to be visited before prior levels are revisited  
* **Problem Choice**:  
  * When presented with a choice of seemingly isolated problems, start with the problem with the fewest inputs and constants; tie-breakers are number of inputs, number of squares in said inputs, then the position & value of the first problem output diff found by our search heuristic  
  * My actual organic heuristic is to choose the simplest problem with the least amount of factors involved after identifying likely patterns

**Starting Significance Hypotheses:**

* **Significance Hypothesis**: relationships between squares with the same color are highly significant  
* **Significance Hypothesis**: squares can be grouped with adjacent & diagonally adjacent squares of the same color as a single “piece”  
  * At some point in a belief search, squares of the same color at greater distances from each other than immediate adjacency can be considered parts of the same piece

**Current Unsolved Problems**
There's at least three unsolved problems:
* Puzzle categorization (preferably by a model that can admit ignorance rather than hallucinate. Hierarchical temporal memory might work best, but requires specific training) 
* Hypothesis generation / search heuristic (Actually might have a solid draft that just needs to be fleshed out: breadth first with revisiting to dig deeper if solution not found at dynamic thresholds)
* Hypothesis abstract syntax tree (at the very least, replacing prepositional clauses with symbols)

**Puzzle Solutions:**  
1 of 120 Public Evaluation Set V2 [https://arcprize.org/play?task=1ae2feb7](https://arcprize.org/play?task=1ae2feb7)

* Identify constant colors (Example 1: red & pink, Example 3: red), constants (the red vertical piece in Example 2), inputs (everything left of the constant), & outputs (all the new blocks)  
* test relationships between everything (I mean everything, including the sizes of the example graphs) for significance (starting with the simplest relationships first)  
* **Problem Choice Heuristic**: Example 3 is selected with its minima of 3 inputs and 1 constant  
  * **Pattern Recognition (line)**: the restriction of same colored variables to a line from the input suggests a line pattern manipulation  
  * **Pattern Recognition (composition)**: each example contains multiple isolated patterns  
    * **Problem Choice Heuristic**: The grey line is selected for its minima of 1 square  
    * **Problem Considered Solved**: The grey line outputs can be predicted by the Line Pattern definition alone  
    * **Problem Choice Heuristic**: The blue line is selected for its minima of 2 squares  
  * **Pattern Recognition (repetition)**: the fact that the six blue outputs are separated by the same number of empty squares suggests a repeating pattern  
  * **Significance Hypothesis**: the number of squares separating the blue output squares is 1, therefore an equation of relationships between input & constant pieces in this line likely equal 1\.  
    * Check relationships between constant & input squares, starting with the simplest relationships first  
      * The length of the blue input \- 1 \= 1  
  * **Significance Hypothesis**: For each line, the length of an input \- 1 will equal the number of empty squares separating same colored outputs  
    * A test of this hypothesis will pass examples 1 & 3, but fail on example 2  
      * **Significance Indicator**: Passing two examples suggests that this hypothesis is in the right general ballpack. This hypothesis is now a “belief”.  
      * **Additional Rule**: The fact that Example 2 fails (Output state is not completely predicted) means that there is at least one additional rule  
        * **Significance Indicator**: Any variables that were unused in the prediction of passing examples are prioritized for determination of additional rules as every variable likely serves a purpose  
  * **Pattern Recognition (line)**: Each line pattern in Example 2 contains an unused variable  
    * **Significance Hypothesis**: An additional rule can be found in the relationship between the unused variable and either the used variable or the constant  
  * **Extrapolation**: If the unused variable is significant, then we must identify the confounding relationship by applying all beliefs in as much isolation as each rule allows. Each application is known as an “isolate".  
    * **Isolate Overlay**: After creating isolates, we combine them 1:1 to identify collision patterns and to confirm that an overlay accounts for all output variables  
      * **Significance Indicator**: The overlay does account for all output variables  
      * **Pattern Recognition (repetition)**: For each line, one input value wins each collision  
        * Determine a hypothesis based off the first line pattern & test that hypothesis by predicting the winning input value of contests in the other line pattern. As always, start the search for acceptable candidates  from top to bottom, left to right  
          * **Significance Hypothesis**: the input furthest to the right determines the winning input value  
            * This hypothesis, in combination with the first belief, successfully satisfies Example 2  
              * **Naivety Check**: With all examples solved, we examine all example input graphs for experimental constraints (see glossary), prioritizing the naivety checks aspects defined elsewhere in this document  
                * **Numbers**: There are never more than two inputs  
                * **Directionality**: All inputs are to the left of the constant  
                * **Constants**: There is only one constant group and only one constant value  
              * **Human Reasoning Fail**: While AI should be able to do an exhaustive search of experimental constraints, I definitely did not do so consciously the first time I walked through this puzzle. Instead, I examined the test input graphs for things that surprised me (The fact that I could be surprised suggests I did note some constraints subconsciously, however)  
              * **Abstraction of the second belief**:  
                * **Numbers**: “inputs are given priority in order of their relative distance from the left border”  
                * **Directionality**: “inputs are given priority in order of their relative distance from the closest border”  
                * **Borders**: A preference for relationships not involving the puzzle borders requires examining relationships more complex than just between inputs (we started with the simplest explanation and increase complexity as necessary): “inputs are given priority in order of their relative distance from the constant value”  
                * **Constants**: “inputs are given priority in order of how close they are to the nearest constant value (in their line?). Lowest constant value serves as tie breaker for equally near constants”

---

**Puzzles Awaiting Solution Specification:**
[**2 of 120**](https://arcprize.org/play?task=3e6067c3) **Public Evaluation Set V2** **Human Solution**: Recognize that the outputs link the inputs in the order of the single inputs that are not wrapped in rings of constants

[**3 of 120**](https://arcprize.org/play?task=16b78196) **Public Evaluation Set V2** **Human Solution**: Recognize that inputs get “plugged” into constant to full rectangular “limbs”

[**4 of 120**](https://arcprize.org/play?task=142ca369) **Public Evaluation Set V2** **Human Solution**: I actually had trouble with this puzzle because if the beams grow one square at a time, the examples suggest the beams could deflect off each other and then collide (same block), which would lead to a scenario that isn’t addressed by any of the examples

[**5 of 120**](https://arcprize.org/play?task=136b0064) **Public Evaluation Set V2**  
**Human Solution**: it’s a map puzzle\!

[**6 of 120**](https://arcprize.org/play?task=0934a4d8) **Public Evaluation Set V2**  
**Human Solution**: The size of the output graph is highly relevant here

[**7 of 120**](https://arcprize.org/play?task=135a2760) **Public Evaluation Set V2**  
**Human Solution**: simple? Pattern recognition

[**8 of 120**](https://arcprize.org/play?task=13e47133) **Public Evaluation Set V2**  
**Human Solution**: Serious abstraction exercise

[**9 of 120**](https://arcprize.org/play?task=1818057f) **Public Evaluation Set V2**  
**Human Solution**: It's all about the plus symbol.

[**10 of 120**](https://arcprize.org/play?task=195c6913) **Public Evaluation Set V2**  
**Human Solution**: another symbolism map

[**11 of 120**](https://arcprize.org/play?task=20270e3b) **Public Evaluation Set V2**  
**Human Solution**: linkage puzzle

[**12 of 120**](https://arcprize.org/play?task=20a9e565) **Public Evaluation Set V2**  
**Human Solution**: output graph size matters again

[**13 of 120**](https://arcprize.org/play?task=21897d95) **Public Evaluation Set V2**  
**Human Solution**: input & output graphs have inverted sizes

[**14 of 120**](https://arcprize.org/play?task=221dfab4) **Public Evaluation Set V2**  
**Human Solution**: making a trail? Line pattern for sure.

[**15 of 120**](https://arcprize.org/play?task=247ef758) **Public Evaluation Set V2**  
**Human Solution**: Does it fit?\!

[**16 of 120**](https://arcprize.org/play?task=269e22fb) **Public Evaluation Set V2**  
**Human Solution**: This one is fucking crazy. Got to figure out that the output graph is always the same except for color & orientation, which means comparing examples\!

[**17 of 120**](https://arcprize.org/play?task=271d71e2) **Public Evaluation Set V2**  
**Human Solution**: Lots of complex relationships in this one

[**18 of 120**](https://arcprize.org/play?task=28a6681f) **Public Evaluation Set V2**  
**Human Solution**: A water/liquid based puzzle

[**19 of 120**](https://arcprize.org/play?task=291dc1e1) **Public Evaluation Set V2**  
**Human Solution**: graph sizes are relevant again

[**20 of 120**](https://arcprize.org/play?task=2b83f449) **Public Evaluation Set V2**  
**Human Solution**: This puzzle contains a chronological element. No idea how to code that\! 😂

[**21 of 120**](https://arcprize.org/play?task=2ba387bc) **Public Evaluation Set V2**  
**Human Solution**: Seems like a simple? ordering puzzle

[**22 of 120**](https://arcprize.org/play?task=2c181942) **Public Evaluation Set V2**  
**Human Solution**: Seems like a simple? linking puzzle

[**23 of 120**](https://arcprize.org/play?task=2d0172a1) **Public Evaluation Set V2**  
**Human Solution**: Approximate a square? Fuck me.

[**24 of 120**](https://arcprize.org/play?task=31f7f899) **Public Evaluation Set V2**  
**Human Solution**: stacking is simple. Ordering maybe less so.

[**25 of 120**](https://arcprize.org/play?task=332f06d7) **Public Evaluation Set V2**  
**Human Solution**: basic maze puzzle

[**26 of 120**](https://arcprize.org/play?task=35ab12c3) **Public Evaluation Set V2**  
**Human Solution**: basic symbolism puzzle

[**27 of 120**](https://arcprize.org/play?task=36a08778) **Public Evaluation Set V2**  
**Human Solution**: basic liquid puzzle

[**28 of 120**](https://arcprize.org/play?task=38007db0) **Public Evaluation Set V2**  
**Human Solution**: basic liquid puzzle

[**29 of 120**](https://arcprize.org/play?task=3a25b0d8) **Public Evaluation Set V2**  
**Human Solution**: color fill

[**30 of 120**](https://arcprize.org/play?task=3dc255db) **Public Evaluation Set V2**  
**Human Solution**: This puzzle is simple, but I don’t have a simple description for it

[**31 of 120**](https://arcprize.org/play?task=409aa875) **Public Evaluation Set V2**  
**Human Solution**: bullet collisions

[**32 of 120**](https://arcprize.org/play?task=446ef5d2) **Public Evaluation Set V2**  
**Human Solution**: the symbol that communicate outer corner will be interesting to figure out

[**33 of 120**](https://arcprize.org/play?task=45a5af55) **Public Evaluation Set V2**  
**Human Solution**: lines to square

[**34 of 120**](https://arcprize.org/play?task=4a21e3da) **Public Evaluation Set V2**  
**Human Solution**: shape dissection

[**35 of 120**](https://arcprize.org/play?task=4c3d4a41) **Public Evaluation Set V2**  
**Human Solution**: piece displacement

[**36 of 120**](https://arcprize.org/play?task=4c416de3) **Public Evaluation Set V2**  
**Human Solution**: find the odd thing out

[**37 of 120**](https://arcprize.org/play?task=4c7dc4dd) **Public Evaluation Set V2**  
**Human Solution**: Puzzle \#1 looks to be filtering out the noise

[**38 of 120**](https://arcprize.org/play?task=4e34c42c) **Public Evaluation Set V2**  
**Human Solution**: another linking puzzle

[**39 of 120**](https://arcprize.org/play?task=53fb4810) **Public Evaluation Set V2**  
**Human Solution**: Beam cannons\!\!\!

[**40 of 120**](https://arcprize.org/play?task=5545f144) **Public Evaluation Set V2**  
**Human Solution**: Here, fishy, fishy, fishy

[**41 of 120**](https://arcprize.org/play?task=581f7754) **Public Evaluation Set V2**  
**Human Solution**: center line

[**42 of 120**](https://arcprize.org/play?task=58490d8a) **Public Evaluation Set V2**  
**Human Solution**: combining symbols

[**43 of 120**](https://arcprize.org/play?task=58f5dbd5) **Public Evaluation Set V2**  
**Human Solution**: combining symbols

[**44 of 120**](https://arcprize.org/play?task=5961cc34) **Public Evaluation Set V2**  
**Human Solution**: a two-step process

[**45 of 120**](https://arcprize.org/play?task=5dbc8537) **Public Evaluation Set V2**  
**Human Solution**: applying colors

[**46 of 120**](https://arcprize.org/play?task=62593bfd) **Public Evaluation Set V2**  
**Human Solution**: something about gravity

[**47 of 120**](https://arcprize.org/play?task=64efde09) **Public Evaluation Set V2**  
**Human Solution**: combining applied knowledge

[**48 of 120**](https://arcprize.org/play?task=65b59efc) **Public Evaluation Set V2**  
**Human Solution**: tik tak toe

[**49 of 120**](https://arcprize.org/play?task=67e490f4) **Public Evaluation Set V2**  
**Human Solution**: pick the right one & insert it

[**50 of 120**](https://arcprize.org/play?task=6e453dd6) **Public Evaluation Set V2**  
**Human Solution**: I love the color scheme for this puzzle

[**51 of 120**](https://arcprize.org/play?task=6e4f6532) **Public Evaluation Set V2**  
**Human Solution**: definitely can expect changing colors between tests & examples

[**52 of 120**](https://arcprize.org/play?task=6ffbe589) **Public Evaluation Set V2**  
**Human Solution**: This puzzle is unintuitive for me

[**53 of 120**](https://arcprize.org/play?task=71e489b6) **Public Evaluation Set V2**  
**Human Solution**: Identify packet loss

[**54 of 120**](https://arcprize.org/play?task=7491f3cf) **Public Evaluation Set V2**  
**Human Solution**: pattern fusion\!

[**55 of 120**](https://arcprize.org/play?task=7666fa5d) **Public Evaluation Set V2**  
**Human Solution**: fill in between the lines

[**56 of 120**](https://arcprize.org/play?task=78332cb0) **Public Evaluation Set V2**  
**Human Solution**: linking path

[**57 of 120**](https://arcprize.org/play?task=7b0280bc) **Public Evaluation Set V2**  
**Human Solution**: pathfinding puzzle

[**58 of 120**](https://arcprize.org/play?task=7b3084d4) **Public Evaluation Set V2**  
**Human Solution**: Go Go, Power Rangers\!

[**59 of 120**](https://arcprize.org/play?task=7b5033c1) **Public Evaluation Set V2**  
**Human Solution**: What. The. Fuck.

[**60 of 120**](https://arcprize.org/play?task=7b80bb43) **Public Evaluation Set V2**  
**Human Solution**: fix the broken path

[**61 of 120**](https://arcprize.org/play?task=7c66cb00) **Public Evaluation Set V2**  
**Human Solution**: breakdown & shelve the parts

[**62 of 120**](https://arcprize.org/play?task=7ed72f31) **Public Evaluation Set V2**  
**Human Solution**: regenerate missing half

[**63 of 120**](https://arcprize.org/play?task=800d221b) **Public Evaluation Set V2**  
**Human Solution**: ant nest puzzle

[**64 of 120**](https://arcprize.org/play?task=80a900e0) **Public Evaluation Set V2**  
**Human Solution**: pull signal from noise

[**65 of 120**](https://arcprize.org/play?task=8698868d) **Public Evaluation Set V2**  
**Human Solution**: holey, holey, holey

[**66 of 120**](https://arcprize.org/play?task=88bcf3b4) **Public Evaluation Set V2**  
**Human Solution**: whip slap

[**67 of 120**](https://arcprize.org/play?task=88e364bc) **Public Evaluation Set V2**  
**Human Solution**: levers & switches

[**68 of 120**](https://arcprize.org/play?task=89565ca0) **Public Evaluation Set V2**  
**Human Solution**: one hell of a simplication

[**69 of 120**](https://arcprize.org/play?task=898e7135) **Public Evaluation Set V2**  
**Human Solution**: combine parts, ignore rest

[**70 of 120**](https://arcprize.org/play?task=8b7bacbf) **Public Evaluation Set V2**  
**Human Solution**: flower the path

[**71 of 120**](https://arcprize.org/play?task=8b9c3697) **Public Evaluation Set V2**  
**Human Solution**: attach engines?

[**72 of 120**](https://arcprize.org/play?task=8e5c0c38) **Public Evaluation Set V2**  
**Human Solution**: remove asymmetries

[**73 of 120**](https://arcprize.org/play?task=8f215267) **Public Evaluation Set V2**  
**Human Solution**: count the small pieces

[**74 of 120**](https://arcprize.org/play?task=8f3a5a89) **Public Evaluation Set V2**  
**Human Solution**: draw the border

[**75 of 120**](https://arcprize.org/play?task=9385bd28) **Public Evaluation Set V2**  
**Human Solution**: with our powers combined\!

[**76 of 120**](https://arcprize.org/play?task=97d7923e) **Public Evaluation Set V2**  
**Human Solution**: pick sticks by length

[**77 of 120**](https://arcprize.org/play?task=981571dc) **Public Evaluation Set V2**  
**Human Solution**: no idea, but sure is colorful

[**78 of 120**](https://arcprize.org/play?task=9aaea919) **Public Evaluation Set V2**  
**Human Solution**: stacking pots?

[**79 of 120**](https://arcprize.org/play?task=9bbf930d) **Public Evaluation Set V2**  
**Human Solution**: two lines \= path

[**80 of 120**](https://arcprize.org/play?task=a251c730) **Public Evaluation Set V2**  
**Human Solution**: why the fields of flowers?

[**81 of 120**](https://arcprize.org/play?task=a25697e4) **Public Evaluation Set V2**  
**Human Solution**: sticking the right end in the hole

[**82 of 120**](https://arcprize.org/play?task=a32d8b75) **Public Evaluation Set V2**  
**Human Solution**: combining four different symbols

[**83 of 120**](https://arcprize.org/play?task=a395ee82) **Public Evaluation Set V2**  
**Human Solution**: clone a template

[**84 of 120**](https://arcprize.org/play?task=a47bf94d) **Public Evaluation Set V2**  
**Human Solution**: separating interlocked, same value pieces

[**85 of 120**](https://arcprize.org/play?task=a6f40cea) **Public Evaluation Set V2**  
**Human Solution**: predict what is hidden

[**86 of 120**](https://arcprize.org/play?task=aa4ec2a5) **Public Evaluation Set V2**  
**Human Solution**: make a face\!

[**87 of 120**](https://arcprize.org/play?task=abc82100) **Public Evaluation Set V2**  
**Human Solution**: seems simple enough

[**88 of 120**](https://arcprize.org/play?task=b0039139) **Public Evaluation Set V2**  
**Human Solution**: What. The. Fuck.

[**89 of 120**](https://arcprize.org/play?task=b10624e5) **Public Evaluation Set V2**  
**Human Solution**: generalize features

[**90 of 120**](https://arcprize.org/play?task=b5ca7ac4) **Public Evaluation Set V2**  
**Human Solution**: separate by category

[**91 of 120**](https://arcprize.org/play?task=b6f77b65) **Public Evaluation Set V2**  
**Human Solution**: removing colors

[**92 of 120**](https://arcprize.org/play?task=16de56c4) **Public Evaluation Set V2**  
**Human Solution**: basic line patterns

[**93 of 120**](https://arcprize.org/play?task=b99e7126) **Public Evaluation Set V2**  
**Human Solution**: blanket pattern?

[**94 of 120**](https://arcprize.org/play?task=b9e38dc0) **Public Evaluation Set V2**  
**Human Solution**: pour out the bag

[**95 of 120**](https://arcprize.org/play?task=bf45cf4b) **Public Evaluation Set V2**  
**Human Solution**: clone the template according to the symbol

[**96 of 120**](https://arcprize.org/play?task=c4d067a0) **Public Evaluation Set V2**  
**Human Solution**: extending a template according to symbols

[**97 of 120**](https://arcprize.org/play?task=c7f57c3e) **Public Evaluation Set V2**  
**Human Solution**: abstract templates (ignore size) or link pieces by color

[**98 of 120**](https://arcprize.org/play?task=cb2d8a2c) **Public Evaluation Set V2**  
**Human Solution**: decoding traffic signal

[**99 of 120**](https://arcprize.org/play?task=cbebaa4b) **Public Evaluation Set V2**  
**Human Solution**: linking puzzle

[**100 of 120**](https://arcprize.org/play?task=d35bdbdc) **Public Evaluation Set V2**  
**Human Solution**: only flower the end of the path

[**101 of 120**](https://arcprize.org/play?task=d59b0160) **Public Evaluation Set V2**  
**Human Solution**: filter sets by key

[**102 of 120**](https://arcprize.org/play?task=d8e07eb2) **Public Evaluation Set V2**  
**Human Solution**: areSymbolsInLine?

[**103 of 120**](https://arcprize.org/play?task=da515329) **Public Evaluation Set V2**  
**Human Solution**: I have no fucking clue

[**104 of 120**](https://arcprize.org/play?task=db0c5428) **Public Evaluation Set V2**  
**Human Solution**: inverse explosion

[**105 of 120**](https://arcprize.org/play?task=db695cfb) **Public Evaluation Set V2**  
**Human Solution**: crossing lines

[**106 of 120**](https://arcprize.org/play?task=dbff022c) **Public Evaluation Set V2**  
**Human Solution**: Solve the color swirl

[**107 of 120**](https://arcprize.org/play?task=dd6b8c4b) **Public Evaluation Set V2**  
**Human Solution**: prioritization

[**108 of 120**](https://arcprize.org/play?task=de809cff) **Public Evaluation Set V2**  
**Human Solution**: packet loss identification

[**109 of 120**](https://arcprize.org/play?task=dfadab01) **Public Evaluation Set V2**  
**Human Solution**: looks like the real test intent here is avoiding contamination from the output pieces that are in the input graph

[**110 of 120**](https://arcprize.org/play?task=e12f9a14) **Public Evaluation Set V2**  
**Human Solution**: colliding beams

[**111 of 120**](https://arcprize.org/play?task=e3721c99) **Public Evaluation Set V2**  
**Human Solution**: color by hole

[**112 of 120**](https://arcprize.org/play?task=e376de54) **Public Evaluation Set V2**  
**Human Solution**: average length

[**113 of 120**](https://arcprize.org/play?task=e8686506) **Public Evaluation Set V2**  
**Human Solution**: another combination puzzle

[**114 of 120**](https://arcprize.org/play?task=e87109e9) **Public Evaluation Set V2**  
**Human Solution**: symbols to directions

[**115 of 120**](https://arcprize.org/play?task=edb79dae) **Public Evaluation Set V2**  
**Human Solution**: shape & color from different symbols

[**116 of 120**](https://arcprize.org/play?task=eee78d87) **Public Evaluation Set V2**  
**Human Solution**: XOR combined with static output

[**117 of 120**](https://arcprize.org/play?task=f560132c) **Public Evaluation Set V2**  
**Human Solution**: another color swirl

[**118 of 120**](https://arcprize.org/play?task=f931b4a8) **Public Evaluation Set V2**  
**Human Solution**: grid size & symbols

[**119 of 120**](https://arcprize.org/play?task=faa9f03d) **Public Evaluation Set V2**  
**Human Solution**: fix the paths

[**120 of 120**](https://arcprize.org/play?task=fc7cae8d) **Public Evaluation Set V2**  
**Human Solution**: rotate or flip according to color

**Non-exhaustive list of Pattern Manipulations:** (for convenient reference)  
Great — you're asking about **math visual logic pattern manipulations** — which covers how **patterns are transformed** in mathematical, visual, or logical contexts. This includes **symmetry operations, geometric transformations, and logical modifications** that can be applied to sequences, shapes, or grids.

Here's a **comprehensive list** of **mathematical and visual logic pattern manipulations**, grouped by category:

---

## **🔁 1\. Geometric Transformations**

These change the position, orientation, or size of a shape or pattern.

| Manipulation | Description |
| :---- | :---- |
| **Translation** | Shifting a pattern along x/y (or in 3D, z) axes. |
| **Rotation** | Rotating the pattern around a fixed point. |
| **Reflection** | Flipping a pattern across an axis (mirror image). |
| **Glide Reflection** | A reflection followed by a translation. |
| **Scaling (Dilation)** | Making a pattern larger or smaller while keeping proportions. |
| **Shearing (Skewing)** | Slanting the shape — distorting angles but keeping parallelism. |
| **Inversion** | Reflecting points through a circle (used in advanced geometry). |

---

## **🔄 2\. Symmetry Operations**

Focuses on repeating patterns and balance.

| Manipulation | Description |
| :---- | :---- |
| **Rotational Symmetry** | Pattern looks the same after certain rotations. |
| **Reflectional Symmetry** | Mirror symmetry along an axis. |
| **Translational Symmetry** | Repeats over intervals (tiling, frieze patterns). |
| **Glide Symmetry** | Combination of reflection and translation. |
| **Point Symmetry (Central Symmetry)** | Rotation by 180° around a point. |

---

## **🔢 3\. Numerical / Sequence Pattern Manipulations**

Logical transformations applied to sequences or grids.

| Manipulation | Description |
| :---- | :---- |
| **Arithmetic Progression** | Add/subtract a constant to generate sequence. |
| **Geometric Progression** | Multiply/divide by constant. |
| **Modular Repetition** | Applying mod n logic to repeat elements. |
| **Alternation** | Switching between two or more patterns (e.g. ABAB). |
| **Recursive Patterns** | Using output as input for the next step. |
| **Shifting** | Offset elements in a sequence (e.g. time delay, phase shift). |
| **Permutation** | Rearranging elements. |
| **Mirror/Reverse** | Inverting a sequence. |

---

## **🎨 4\. Tiling & Tessellation**

Used in both geometry and visual logic pattern creation.

| Manipulation | Description |
| :---- | :---- |
| **Regular Tessellation** | Repeating one shape (e.g., equilateral triangle). |
| **Semi-Regular Tessellation** | Repeating multiple regular polygons in a pattern. |
| **Irregular Tessellation** | Repeating non-standard shapes. |
| **Non-Periodic Tiling** | Like Penrose tiling — patterns that never repeat exactly. |
| **Fractals / Self-Similarity** | Zoomed-in versions look like the whole. |

---

## **🧠 5\. Logical Pattern Manipulations**

From visual puzzles, IQ tests, and logic games.

| Manipulation | Description |
| :---- | :---- |
| **Progression (Stepwise change)** | Gradual transformation of shape/number. |
| **Pattern Completion** | Filling in the next item or missing piece. |
| **Analogical Mapping** | A:B :: C: ? — find logical similarity. |
| **Rotation in Steps** | Rotating shape a fixed amount between steps. |
| **Color / Shade Shifts** | Gradual change in tone or color pattern. |
| **Grid-Based Transformations** | Changing rows/columns based on rules. |

---

## **📐 6\. Topological Manipulations (Advanced/Abstract)**

Patterns considered under continuous deformation.

| Manipulation | Description |
| :---- | :---- |
| **Stretching/Shrinking** | Without tearing — preserves connectivity. |
| **Twisting (e.g., Möbius strip)** | Introducing topological twists. |
| **Knots and Links** | Patterns involving loops and entanglement. |

---

### **✅ Summary: Key Math Visual Logic Pattern Manipulations**

* **Transformations:** translation, rotation, reflection, scaling, shearing  
    
* **Symmetry:** rotational, reflectional, translational, glide  
    
* **Sequences:** arithmetic, geometric, recursive, permutation  
    
* **Tessellation:** regular, semi-regular, fractal, non-periodic  
    
* **Visual logic:** alternation, analogy, stepwise rotation, shading  
    
* **Topology (advanced):** twisting, deformation, knotting

---

Would you like visual examples for any of these? Or are you working on something specific like an IQ test, art, or puzzle design?  
