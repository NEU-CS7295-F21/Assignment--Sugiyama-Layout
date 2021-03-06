# Assignment — Sugiyama Layout

This repository is your starting point for the assignment and includes instructions below.

# Aim of the assignment

The goal of this assignment is to re-familiarize you with the classic Sugiyama layout algorithm for layered graph drawing, as well as help you get a more complete understanding of its intricacies. As the best way to learn all the ins and outs is to build it yourself, in this assignment you'll create your own implementation of Sugiyama.

# About GitHub Classroom

## Accepting an assignment

1. Click the **GitHub Classroom link** on the Canvas assignment to set up a git repository for you to work in.

    * The first time you accept an assignment for the course, you will need to connect your GitHub account with our roster imported from Canvas. If you do not have a GitHub account yet, you will need to [create one](https://github.com/join) before connecting it.

    * Your interface will look something like [this](https://github.blog/2020-03-18-set-up-your-digital-classroom-with-github-classroom/#what-your-students-see).

1. Accept the Assignment.

1. Wait for it to create a repository.

1. Click on the link to where the Assignment repository has been created.

## Assignment instructions

 Follow the instructions included in this `README.md` file at the root of your repository.

GitHub nicely displays this for you when you go to the repository online. Many text editors will also display previews for you. E.g., [Visual Studio Code](https://code.visualstudio.com/) has a nice [Markdown preview and extensions](https://code.visualstudio.com/docs/languages/markdown).


## Invitation links vs. forking

The [GitHub Classroom](classroom.github.com/) invitation link we provide is creating a copy of a [template repo](https://docs.github.com/en/free-pro-team@latest/github/creating-cloning-and-archiving-repositories/creating-a-template-repository) we created that gives you a starting place.

**Do not just fork this repo or use it as a template directly!** Instead, use the GitHub Classroom invitation link.

# Instructions

## Setup instructions

1. Clone the repo.

1. `CD` to the repo directory.

***Add your documentation here!***

## Run instructions

***Add your documentation here!***

## Implement

Write the code to implement Sugiyama's layout and visualize the result for a graph.

You're welcome to use any language you like for the algorithm and any visualization frontend (including printing a beautiful text version of the layout to the terminal), as long as you can get all the code into this repo.

### The algorithm

Here are three good references on how the algorithm works:

> Sugiyama (2002) Graph drawing and applications for software and knowledge engineers.
doi: [10.1142/4902](https://doi.org/10.1142/4902) [Canvas access-controlled PDF](https://northeastern.instructure.com/courses/90512/files/11199469?wrap=1). _In particular, starting page 61._

> Healy & Nikolov (2013) Hierarchical Drawing Algorithms. [Author PDF](https://cs.brown.edu/people/rtamassi/gdhandbook/chapters/hierarchical.pdf). _Mixed in with other methods._

> Sugiyama et al. (1981) Methods for visual understanding of hierarchical system structures. IEEE Transactions on Systems, Man, and Cybernetics. doi: [10.1109/TSMC.1981.4308636](https://doi.org/10.1109/TSMC.1981.4308636). _The original article_. 

Note that we expect you to implement all four steps of the algorithm:

I. Cycle removal
II. Layer assignment
III. Vertex ordering
IV. Final positioning

But you don't need to implement the best or optimal solution in each case! Do what you can. I.e., here are several of the approaches for each step. We suggest you try the #1 in each list.

#### I. Cycle removal options, sorted roughly easiest to hardest:

0. Remove them manually (only useful for testing)
1. Simple depth-first search approach. _See Sugiyama (2002), pp. 62._
2. Simple repeated maximal out-degree node removal. _See Sugiyama (2002), pp. 63._
3. Divide and conquer approach _See Sugiyama (2002), pp. 63; Healy & Nikolov (2013), pp. 414._
4. Exact ILP method. _See references at Healy & Nikolov (2013), pp. 417._

#### II. Layer assignment options, sorted roughly easiest to hardest:

0. Assign layers manually (only useful for testing)
1. Simple spanning tree approach. _See Healy & Nikolov (2013), pp. 419–420._
2. Longest path algorithm. _See pseudocode in Healy & Nikolov (2013), pp. 421; Sugiyama (2002), pp. 63–64._
3. Min-width algorithm. _See pseudocode in Healy & Nikolov (2013), pp. 423._

    Optionally, the vertex promotion heuristic can be used along with the longest path or min-width algorithms. _See pseudocode in Healy & Nikolov (2013), pp. 424–425._

#### III. Vertex ordering options, sorted roughly easiest to hardest:

1. Barycentric heuristic for multi-layer crossing minimization. _See Healy & Nikolov (2013), pp. 435, 438; Sugiyama (2002), pp. 73._

    Optionally, add Gansner et al.'s stopping criteria instead of the number of iterations. _(Citation GKNV93 in Healy & Nikolov (2013), pp. 438.)_

2. Try one of the optimal versions. _See Healy & Nikolov (2013), pp. 439._

#### IV. Final positioning options, sorted roughly easiest to hardest:

0. Assign first node in each layer to 0 coordinate and add each subsequent one some separation distance apart. Will result in left/top shifting the nodes. (Useful for testing.)
1. Quadratic programming method. _See Sugiyama (2002), pp. 75; Healy & Nikolov (2013), pp. 441._
2. Priority layout method. _See Sugiyama (2002), pp. 77; Healy & Nikolov (2013), pp. 441._
3. Gansner et al.'s exact or heuristic algorithm. _See citation GKNV93 in Healy & Nikolov (2013), pp. 441._


### Example data for testing

Please see the [/data](/data) folder for example data you can use in GraphML and GraphViz formats. The data is originally in GraphML from the [Rome-lib dataset](http://www.graphdrawing.org/download/rome-graphml.tgz). Your resulting visualization should have a layout something like this (if you used the `.gv` file, with nodes ids starting at 1):

![Sugiyama layout of test-graph-01.gv with Tulip](/data/test-graph-01.gv_Tulip-Sugiyama.png)

or like this (if you used the `.graphml` file, which has node ids starting at 0):

![Sugiyama layout of test-graph-01.graphml with Tulip](/data/test-graph-01.graphml_Tulip-Sugiyama.png)

The blue edges are part of a directed cycle.

These were generated using [Tulip](tulip.labri.fr/site/) and it's included Sugiyama layout from OGDF, described [here](http://cs.brown.edu/people/rtamassi/gdhandbook/chapters/ogdf.pdf).

Here's the same dataset (`.gv` file) shown using [GraphViz](https://graphviz.org/)'s dot layout via [Viz.js](https://github.com/mdaines/viz.js):
![dot layout of test-graph-01.gv with Viz.js](/data/test-graph-01.gv_graphviz-vizjs-dot.svg)


For testing, you're welcome to use other graphs from Rome-lib, or the exciting [Unix history graph](https://github.com/x64dbg/ogdf/blob/master/_examples/layout/hierarchical/unix-history.gml) (GML file, not the same as GraphML).

## Document

Add sufficient documentation to the top of this README.md file under Setup Instructions and Run Instructions so that we can install and run your code and view the output.

## Add a screenshot of the output

In case we can't run your code for some reason, take a screenshot of your output and include it in this `README.md` file here:

***Put your image here!***

## Commit and push your code

1. Make sure to add all your required files to the git repo, and not any temporary or unnecessary files. You can use a `.gitignore` file to avoid accidental commits.

2. Finally, commit all your local files and push them to the remote repository on GitHub which was generated by GitHub Classroom.

# Submission instructions

1. Ensure that:
    * all of your required files and your final image are pushed to the remote repository on GitHub which was generated by GitHub Classroom.

    We will grade based on what is available in that repository.

2. Submit the URL of **your GitHub Classroom-generated repository** (not a GitHub Page — we're not using it for this assignment anyway) to the associated assignment on Canvas. **Do not submit a link to a personal repository. It must be within our class GitHub organization.**


# Grading

Please see the rubric on Canvas.

# Late Policy

Partial credit up to 24 hours late as detailed on the syllabus.
