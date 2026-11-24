# Information Required

Write these sections in `docs/MODULE_INFO.md` in your repository, starting from the [template](../template/MODULE_INFO.md). See the [Lash-E example](../examples/lash-e/MODULE_INFO.md) for how a finished one looks. Words such as *sample*, *container* and *flow* are defined in [Definitions](../definitions.md).

## Maintenance Tasks

List the maintenance tasks this module requires, for example cleaning parts or changing oil in a pump. For each, give a short description of the task, how often it is required, what its purpose is, and whether it is done by a person or by software.

## Known Issues

List the hardware and communication errors that can occur on this system. Explain what you believe causes each error and how you believe it is fixed, or say that you don't know. For each, say how serious it is:

| Severity | Meaning |
|---|---|
| High | Stops the run, and a person must fix it. |
| Medium | Can spoil a sample or a run, but the module keeps working. |
| Low | Fixed or worked around in code; watch for it. |

## Supplies and Waste

List any consumables this module uses and discards, such as pipette tips. Don't include samples or containers (such as well plates). Explain how each supply is loaded and how each type of waste is removed. If a supply is specific, include a link to order it, with enough detail to find it again if the link expires. For each supply, also say how often you restock it (for example, every 2–3 months) and how long it takes to arrive, so we know when to reorder.

## Samples and Containers

Describe the kinds of containers and samples (see [Definitions](../definitions.md)) the module uses or produces.

- **Containers:** be specific about the size, and say exactly where to buy them. If they are custom, link to the design file. Say how many of each the module can hold at once, and, for containers you buy, how often you restock them.
- **Samples:** be specific about their state (solid, liquid, etc.), and describe the types of samples produced so far.
- **For both:** say how they are loaded into the module, by hand or by a robot.

## Module Constraints

Describe any known constraints on the module, such as the viscosity limit for liquids and which solvents it can handle. These should be about the module itself, not its individual parts. For example, a plastic well plate being incompatible with toluene is a constraint of the container, not of the module.

## Module Unit Operations and Flows

List and briefly describe the module's unit operations and flows (see [Definitions](../definitions.md)). In short: a unit operation does one task with clear inputs and outputs; a flow combines them and leaves the module ready for its next task.

- **For each unit operation:** its inputs and outputs, with units.
- **For each flow:** its inputs, which parts of the module it keeps busy while it runs (so other flows can use the rest), and what it needs on hand before it starts, such as supplies or a sample in place.

Don't include primitives or workflows.

## Data Storage

Describe how your module tracks experiments, samples and the data generated during workflows. For each sample, say what you record about it (for example, what it contains and how it was made) and where that record is kept. What kind of data is generated: files, images? How much space have your experiments needed so far?
