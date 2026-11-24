# Up-to-Date Code

Work through these standards in order, on a branch (see [How to do this](../README.md#how-to-do-this)). Each one ends with **Done when**, which is how you know it is met. Words such as *flow* and *state* are defined in [Definitions](../definitions.md).

- [ ] **1. GitHub.** Make sure your module has a GitHub repository for all the code it uses.
  *Done when:* all code the module uses is in one GitHub repo.

- [ ] **2. Hide files and folders.** You can use a `.gitignore` file to keep output data out of the repository if you prefer. You must use it for any files containing secret keys.
  *Done when:* secret keys, and outputs if you prefer, are in `.gitignore` and aren't in the repo.

- [ ] **3. Readme.** Make sure your repository has a readme explaining how the code works and how it relates to the physical module. If you generate the readme with AI, read it through and make sure it is clear and realistic based on your understanding of the system.
  *Done when:* someone new can tell from the readme what each part of the code does and which hardware it controls.

- [ ] **4. Versions.** Record the exact versions of the software your code depends on, for example a requirements file with pinned versions or a conda environment file. Include any vendor software that's installed separately, and how to get it. Update the record when you upgrade.
  *Done when:* someone can install the exact versions on a new computer from your file, and any vendor software is listed with how to get it.

- [ ] **5. Simulation.** Your code must be able to run without talking to hardware. This lets orchestrators check workflow code for bugs without running anything. It should also be possible to make a simulated step fail on purpose (for example, a simulated motor fault), so you can check what your code does when something goes wrong.
  *Done when:* a full workflow runs with no hardware connected, and you can make one step fail on purpose.

- [ ] **6. Compartmentalization.** Structure your code into the following types of files. Don't mix them in the same file.
  *Done when:* each file is one of the types listed, and no file mixes two.

  | File type | What goes in it |
  |---|---|
  | Workflows | Code that runs an experiment by calling flows. |
  | Automation code | Primitives, unit operations and flows. |
  | Inventory files | Tracking of samples, containers, supplies and waste. |
  | State files | The module's current state (see [Definitions](../definitions.md)), for example what the gripper is holding or whether a tip is attached. |
  | YAML files | Physical distances, locations, offsets and other configurable, module-specific values. Don't hard-code these values in your automation code; read them from these files, so they can be changed without editing code. *Done when:* no positions, offsets or device settings are typed directly into the automation code. |
  | Output files | Data, logs, and other files generated during runs. |
  | Input files | Data that your workflow uses. |
  | Recommenders | Code that takes in (X, Y) labelled data and suggests new inputs (X) to try, e.g. Bayesian optimization. |
  | Analyzers | Code that processes data and produces graphs or other data. |

- [ ] **7. Primitives, unit operations and flows.** Organize your automation code so that each method is clearly one of these (see [Definitions](../definitions.md)), and build workflows from flows. Split any method that mixes them, for example a dispense that also picks up a tip and plots its data.
  *Done when:* each method in your automation code is a primitive, unit operation or flow, and each flow leaves the parts it uses ready.

- [ ] **8. Workflow tracking.** Give every workflow run a unique identifier, and when it finishes, save its result (complete, incomplete, etc.). Make it easy to find the data from that run: save the identifier with the data (for example, in the output folder) and record where the data was saved.
  *Done when:* every run has an ID and a saved result, and you can find its data from the ID.

- [ ] **9. Configuration files.** If your workflow has settings that change (e.g. batch size), generate a configuration file with every run and save it under the run's identifier, so no experimental metadata is lost.
  *Done when:* each run's settings are saved with its data, under its ID.

- [ ] **10. Sample tracking.** Every sample should have an identifier and a record of what it is and how it was made: what went into it, how much, and which run made it. Your code should write this record as the module works, not by hand afterwards, and save it with the run's data.
  *Done when:* for any sample, you can find what's in it and which run made it.

- [ ] **11. Error tracking.** Save a record of each hardware error that occurs (bugs in code can be left to normal debugging). Each record should include a short, stable error code (e.g. `MOTOR_FAULT`, not `ERROR_1`), the message, when it happened, what the module was doing, and what state it was left in or what a person needs to do. An error that only appears in a log or a pop-up isn't enough. Anything that has gone wrong could go wrong again; the more we track, the easier it is to fix.
  *Done when:* each hardware error leaves a saved record with its code, message, time, step, and what to do.

- [ ] **12. Safe stop.** Your code should have one way to bring the module to a safe state after an error or interrupt: for example, turn off heaters and pumps, park the robot, and return what it's holding where possible. It should then report what it couldn't do. Call this a "safe stop", not an "emergency stop", because software doesn't replace the physical E-stop button. After a safe stop, the module shouldn't restart on its own; a person decides.
  *Done when:* one function brings the module to a safe state after any error or interrupt, and reports what it couldn't do.

- [ ] **13. Inputs and outputs.** Each unit operation's inputs and outputs should state their units and allowed range in the code (for example `volume_mL`, between 0.001 and 1.0). A value out of range should be rejected before anything moves. If an input has a default, write it in the code next to the input and report the value used; don't fill in missing values silently.
  *Done when:* every unit operation states the units and ranges of its inputs and outputs, and rejects bad values before anything moves.
