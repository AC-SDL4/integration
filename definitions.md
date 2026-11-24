# Definitions

| Term | Meaning |
|---|---|
| **Module** | A set of equipment (a CNC machine with an indenter, for example) that is currently controlled mainly through a specific set of code unique to that module. Separate equipment with different purposes should generally be considered separate modules. If a piece of equipment only operates within a larger system, we consider it part of that module (e.g. a spin-coater inside a CNC platform). |
| **Sample** | An individual item produced by the module for analysis, for example a polymer in a vial, a resin in a well plate, or a film on a glass slide. |
| **Container** | Something that holds samples or other containers, for example a vial, a well plate, or a glass slide. |
| **State** | The condition of the module that determines whether it can carry out its next action: for example, whether the robot is parked, the gripper is empty, a tip is attached, the clamp is open, or an instrument is idle. A module is in the same state when it can perform the same actions as before. State does not include amounts of consumables or samples, such as tips remaining or the volume of liquid in a vial. |
| **Inventory** | What the module has on hand and where it is: samples, containers, supplies and waste, with amounts. For example, tips remaining, or the volume of liquid in each vial. |
| **Primitive** | The smallest action that a single instrument or piece of software exposes, such as moving the robot to a coordinate, opening the gripper, or taring the balance. Primitives are specific to one device and do not, on their own, accomplish a scientific task. |
| **Unit operation** | A combination of primitives that accomplishes one well-defined task, with clear inputs, outputs, and a clear success or failure result. For example, indenting a sample and measuring the force response, or dispensing liquid into the wells of a plate, which leaves the tip attached. A unit operation does not need to leave the module ready for its next task. |
| **Flow** | A combination of unit operations (and primitives where needed) that completes a procedure and is state-preserving: when it finishes, the parts of the module it uses are back in a known, ready state, or, if something goes wrong, stopped safely. For example, validating your dispense settings at the start of a workflow, or transferring liquid from a vial into a well plate, ending with the tip discarded and the vial returned. |
| **Workflow** | A sequence of flows, often with loops or branches, that achieves a complete scientific task. For example, formulating, curing, and indenting a set of samples. Because every flow leaves the module ready, the steps of a workflow can be reordered, repeated, or scheduled alongside other modules. |

These definitions follow Gottstein et al., "A foundational representation for an orchestrated lab" (ChemRxiv, 2026), and the UOroboros orchestrator.
