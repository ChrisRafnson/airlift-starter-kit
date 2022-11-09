# ✈️ Airlift Challenge Starter Kit

This starter kit is part of the Airlift Challenge, a competition in which participants must design agents that can plan and execute an airlift operation.
Quick decision-making is needed to rapidly adjust plans in the face of disruptions along the delivery routes.
The decision-maker will also need to incorporate new cargo delivery requests that appear during the episode.
The primary objective is to meet the specified deadlines, with a secondary goal of minimizing cost.
Solutions can incorporate machine learning, optimization, path planning heuristics, or any other technique.

This repository provides a template for you to create your own solution, test it, and prepare a submission.

# Important links
* For more information about the competition: see the [documentation](https://airlift-challenge.github.io/).
* The simulator can be found [here](https://github.com/airlift-challenge/airlift)
* For submissions and to participate in the discussion board: see the [competition platform on CodaLab](https://codalab.lisn.upsaclay.fr/competitions/0000)

# Getting Started

## 1) Setup prerequisites

A) Install [Anaconda](https://www.anaconda.com/distribution/).
We use Anaconda to create a virtual environment.

B) Clone the starter kit repo.
```bash
$ git clone https://github.com/airlift-challenge/airlift-starter-kit
$ cd airlift-starter-kit
```

C) Create the `airlift-solution` Anaconda environment:
```bash
$ conda env create -f environment.yml
$ conda activate airlift-solution
```
Optionally, you may want to install the core airlift simulator code from source to allow for easier debugging.
This can be done by commenting out the simulator pip requirement in [environment.yml](environmnent.yml), and installing from source aa described in the [Airlift Simulator README](https://github.com/airlift-challenge/airlift/README.md#Installing-with-pip). 

## 2) Write your solution code

We provide a [Solution class](https://airlift-challenge.github.io/chapters/API/essential_api.html#solutions) that you can extend to build your own solution.
You need to fill in two methods:
1) *`reset`*. Resets the solution code in preparation for a new episode.
2) *`policies`*. A method which takes in a set of observations for all agent and returns a set of actions for each.
It is important that your solution only rely on the information found in the observation and not attempt to access internal environment attributes. 

The starter kit provides an [example random agent solution](solution/mysolution.py) which you can modify to produce your solution.
You may also want to reference our [baseline](https://github.com/airlift-challenge/airlift/solution/baselines.py) which implements a simple agent that follows a shortest path.

For more information, you can view the following sections in the [documentation](https://airlift-challenge.github.io/).
* *[Model](sec_model)*. Formulates the model implemented by the simulator.
* *[Interface](sec_interface)*. Provides information regarding the observation and action spaces, as well as rewards and metrics.
* *Essential API*. Documents key classes and methods you may need to interact with.
* *[Solutions](sec_solutions)*. Provides some background on previous solutions to the airlift and other related problems.
* *Simulator Code Documentation*. Although you do not need to understand the internals of the simulator to write a solution, it could help with debugging.

## 3) Test your solution

### Evaluate your solution against the test set
Download the [test scenarios](https://airlift-challenge.github.io/scenarios/scenarios_test.zip) and unzip the contents into the `/scenarios` folder.
Then, perform the evaluation by running:
```bash
$ ./eval.sh
```
Optionally, you may specify a different scenario folder by passing the folder name as a parameter:
```bash
$ ./eval.sh scenariofolder
```
The test set is similar to the hidden scenarios that will be used for the final evaluation.

The evaluator will output two csv files:
* *`reakdown_results.csv`.* Provides details regarding each episode.
* *`results_summary.csv`.* Provides a summary of the overall evaluation and score.

We also provide a set of simpler [development scenarios](https://airlift-challenge.github.io/scenarios/scenarios_dev.zip) for building and debugging your agent.
You may build your own set of evaluation scenarios as well. See [Generating Scenarios page](https://airlift-challenge.github.io/chapters/ch5_gen/main.html) for more information.


### Run the solution with a custom-built environment
Rather than running the environment against a set of pre-generated scenarios, you may also instantiate an environment in Python with custom scenario parameters.
This can be useful for debugging (to avoid the overhead of generating scenario files), as well as for generating training scenarios for a machine learning solutions.
An example is provided in [run_custom_scenario.py](run_custom_scenario.py), which can be run with the following command:
```bash
$ python run_custom_scenario.py
```
More information on parameterizing the scenarios can be found in [Generating Scenarios page](https://airlift-challenge.github.io/chapters/ch5_gen/main.html).

## 4) Submission
Once you are finished with your solution code, you can produce a zip file archive and make a submission at the [competition platform on CodaLab](https://codalab.lisn.upsaclay.fr/competitions/0000).
Your submission should contain the following files: 

**File/Directory** | **Description**
--- | ---
[`postBuild`](postBuild) | Specify any additional commands that need to be run when building the Docker image.
[`environment.yml`](environment.yml) | File containing the list of python packages you want to install for the submission to run. This should instantiate a conda environment named `airlift-solutions`.
[`apt.txt`](apt.txt) | File containing the list of OS packages you want to install for submission to run.
[`eval.sh`](evaluator) | **Submission entrypoint** - Use this as the entrypoint to run your code using the local evaluator.


Distribution Statement A: Approved for Public Release; Distribution Unlimited:
Case Number: AFRL-2022-5074, CLEARED on 19 Oct 2022