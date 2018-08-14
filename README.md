# Adopting Continuous Integration for Long-timescale Materials Simulation

**Hero Image:**

<img src='./hero.png' />

#### Contributed by [Richard Zamora](https://rjzamora.github.io "Rick Zamora's Github.io Profile")

#### Publication date: August 7th, 2018

**In order to push the scalability of accelerated molecular dynamics simulations, the EXAALT team is adopting continuous integration to improve their productivity.**

[EXAALT](https://www.exascaleproject.org/project/exaalt-molecular-dynamics-at-the-exascale-materials-science/), which stands for the *Exascale Atomistic capability for Accuracy, Length and Time*, is an [ECP](https://www.exascaleproject.org/)-funded materials modeling framework designed to leverage extreme-scale parallelism to produce high-performance molecular dynamics simulations. The end goal is to allow the user to access the most appropriate combination of accuracy, length, and time for the problem at hand, trading the costs of various forms of parallelism.  As shown in **Fig 1**, EXAALT is actually a collection of multiple packages, each having its own dependencies. At the heart of EXAALT is the Large-scale Atomic/Molecular Massively Parallel Simulator ([LAMMPS](https://lammps.sandia.gov/)), developed at Sandia National Laboratory (SNL). However, to enable simulations with *ab initio* accuracy and reaching unprecedented time scale, the framework also includes the [LATTE](https://github.com/lanl/LATTE) and [ParSplice](https://gitlab.com/exaalt/parsplice) packages, both developed at Los Alamos Nation Laboratory (LANL).

<!--- Image to illustrate the complexity of EXAALT --->
<img src='./dep-graph.png' />

**Fig 1.** Illustration of the EXAALT framework. The three main software components (LAMMPS, LATTE, and ParSplice) are represented as colored circles, while other libraries are represented as grey circles. Lines (graph edges) depict dependencies between the various software components.

In 2017, LANL focused its annual IS&T Co-Design Summer School program on the topic of Accelerated Molecular Dynamics (AMD).  The idea was to gather a small group of elite graduate students to help optimize the performance of ParSplice, the AMD driver of EXAALT.  During the early weeks of that summer, the developers of ParSplice quickly recognized that their rapidly-evolving code had become difficult for the typical (and even advanced) computational scientist to compile and run.  This was because the existing build system (or lack there of) was becoming prohibitively difficult to negotiate. 

The summer students overcame these technical difficulties, and accomplished great things.  However, their early challenges inspired the EXAALT team to be more proactive about future productivity issues.  That is, they decided to collaborate closely with local members of the ECP [IDEAS](https://ideas-productivity.org/ideas-ecp/) project, to adopt modern and sustainable software-development practices.  In the short term, this meant the implementation of a more user-friendly and portable build system (compared to the manual `Makefile`-based compilation of several different packages). In the long term, this meant the development of a continuous-integration (CI) pipeline to first automate the testing of the modern build system, and ultimately accelerate all quality-control efforts moving forward.  

<!--- Image to show build and test PSIP cards /> --->
<img src='./psip-ci-test.png' /> 
**Fig 2.** Summarized versions of PSIP process cards that were used for the EXAALT-IDEAS collaboration.  Note that some details about dependencies and timeline are excluded for clarity.

The ongoing EXAALT-IDEAS collaboration has proven mutually beneficial to both ECP teams: providing the EXAALT team with technical advice, and providing the IDEAS team with first-hand insight into the fundamental needs of an ECP application project. To help the IDEAS team map their collaboration efforts onto a manageable set of tasks, providing tangible benefits to the EXAALT team, they leveraged the [Productivity and Sustainability Improvement Planning (PSIP)](https://github.com/betterscientificsoftware/PSIP-Tools/blob/master/PSIP-Overview.md "PSIP Github README") process. For the first stage of the collaboration, the construction of a minimal end-to-end `CMake` build system for the entire framework, this process was implicitly used for project planning. For the second (and ongoing) stage, PSIP was specifically used to compile the *tracking cards*, shown in **Fig 2** (in summarized form).   

These PSIP cards were used to plan the minimal steps needed to lay the foundation for CI within the existing EXAALT [software repository](https://gitlab.com/exaalt), and to track the progress of these steps. Although the PSIP process can be used to manage the goals of many software projects, the details of the specific steps are project dependent.  In this case, after careful discussion between the application and productivity teams, it was decided that the CI pipeline in EXAALT would leverage four key technologies:

- [**CMake**](https://cmake.org/): To manage the end-to-end compilation and testing execution
- [**GitLab CI**](https://about.gitlab.com/features/gitlab-ci-cd/): To automatically build and test the software framework (using CMake) to validate new repository commits
- [**Docker**](https://www.docker.com/): To generate standard system images (with library dependencies) for use in GitLab CI
- [**Boost**](https://www.boost.org/): To implement and organize functionality tests (integration, regression, and unit)




<!---
Publish: No
Categories: reliability
Topics: testing
Tags: bssw-blog-article
Level: 2
Prerequisites: default
Aggregate: none
--->
