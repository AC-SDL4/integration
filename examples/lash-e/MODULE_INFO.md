# Lash-E (North + Cytation module): module information

> **This is an example, not a requirement.** It shows a finished hand-in for one module, Lash-E, so you can see what yours should look like. Your module's details will be different. All of the requirements are in [requirements/](../../requirements/); nothing here adds to them.

**Repository:** https://github.com/AccelerationConsortium/North-Cytation

**Module description:** Lash-E can simulate basic reactors with heat and illumination; it can dispense liquids using AI-calibrated parameters; it can dispense solids; it can prepare thin films; it can cap and uncap vials and move them around; it can measure mass on a clamp; it can measure absorbance, fluorescence and imaging with the Cytation 5; and it can transport well plates to and from the Cytation and a waste/source stack with a track. In theory, the Cytation 5 could be its own module, but for now they are coupled.

## Maintenance Tasks

| Task | How often | Purpose | Done by |
|---|---|---|---|
| Empty water from the compressor | Weekly | Keeps the compressor from filling with water and breaking | By hand |
| Check the deck positions are correct | Monthly | Makes sure nothing has drifted, which prevents automation errors | By hand |
| Calibrate the Cytation 5 (method to be confirmed) | Yearly | Keeps readings accurate | By hand |
| Change the compressor oil | Every 6 months | General compressor maintenance | By hand |
| Oil the z-axis | Every 6 months | Prevents friction and squeaking | By hand |
| Strip, clean and regrease the gripper | Every 6 months | The gripper has stopped gripping properly in the past | By hand |
| Check the track grip pads | Monthly | They grip the well plates and wear out | By hand |
| Replace the track grip pads | Every 6 months | They wear out with use | By hand |

## Known Issues

| Issue | Severity | Cause | Fix |
|---|---|---|---|
| Motor fault (robot stops with IO: MOTOR FAULT) | High | A collision. Usually a symptom of another issue: a small tip pulling a vial out, a vial moved in the clamp, the gripper slipping, a vial not placed back correctly, or a location being off. | Power-cycle the controller, fix the cause, then use Reset Robot. |
| Cytation not connected at startup | High | Unknown. | Power-cycle the Cytation (about 5 minutes). Once it connects at the start, it doesn't lose the connection. |
| Cytation plate read error | High | Usually a problem with the Gen5 protocol, for example the plate type is mis-specified. | Check the Gen5 protocol. The plate is left in the Cytation. |
| Small tip catches on retraction | High | The robot wasn't designed for small tips. When a vial is low, the tip can catch in an open cap on retraction and pull the vial out. The small tip only reaches the bottom without banging at positions 42–47, heater 2, 5 and 8, clamp and clamp_2. | Worked around in code: workflows stage vials before dispensing small volumes and refill them before they get too empty, both decided from the volume left in each vial. The clamp vial is usually ok down to about 0.5 mL. |
| Vial drift at clamp | Low | The gripper can nudge vials at the clamp when it retracts, so they can't be gripped. | Fixed: vials left at the clamp are held by the clamp, then released after the robot retracts. |
| Gripper slipping while grabbing a vial | Medium | Usually one of: the gripping position is off; the gripper head needs to be removed, cleaned and regreased; or its metal parts are worn or failing. | Correct the gripping position, or service or replace the gripper head. |
| Tips knocked on the rack | Medium | The robot has knocked large tips when grabbing another tip. | Fixed with a wiggle routine on retract. Watch for tips that end up in the middle of a rack after runs. |
| Vials not placed back correctly | Low | The gripper needed maintenance: it was missing a fastening screw. | Fixed once the part was replaced. |
| Capping problems (vials loose after capping, or grinding) | Medium | Can be caused by using different caps. | More careful positioning and adjusting the number of revolutions in the capping cycle. Test capping periodically. |

## Supplies and Waste

| Supply | Where to buy | Shipping time | How often to restock |
|---|---|---|---|
| Pipette tips, 250 µL | Mettler Toledo, product 17014397 | ~2 weeks | Every 2–3 months |
| Pipette tips, 1000 µL | Mettler Toledo, product 17014398 | ~2 weeks | Every 2–3 months |
| Open cap lids, 8 mL | Sigma, product 27054 | ~7 days | Every 6 months |
| Reservoirs | TBD | TBD | TBD |

**How supplies are loaded:** all by hand.

**Waste, and how it is removed:** mixed pipette tips, well plates and used vials, all removed by hand.

## Samples and Containers

**How containers are loaded:** all by hand.

| Container | Holds at once | Where to buy | Shipping time | How often to restock |
|---|---|---|---|---|
| 96-well plates, clear | About 8 plates in total, of all types | Medstores, SKU 83.3924.300 | ~5 days | Every 2–3 months |
| 96-well plates, black (fluorescence) | About 8 plates in total, of all types | Sigma, product CLS353219 | ~1 week | Every 2–3 months |
| 24- and 48-well plates; 96-well quartz plates | About 8 plates in total, of all types | TBD | TBD | TBD |
| Vials, 8 mL, open or closed caps | 48 in the rack, 12 on the heater, 1 in the photoreactor | Chemstores | Picked up on demand | TBD |
| Vials, 20 mL, no caps (liquid storage) | 4 | Chemstores | Picked up on demand | TBD |

**Samples:** solutions in vials, and solutions in well plates.

## Module Constraints

| Constraint | Limit |
|---|---|
| Temperature | Up to 100 °C for vials; no cooling. |
| Pressure | Atmospheric pressure only. |
| Liquids | Viscosity up to about 1500 cP; pipetting from 5 µL to 1 mL per aspiration. |
| Solvents | Water, DMSO, glycols and most common organic solvents. Currently not under a fume hood, so volatile or toxic solvents need extra care. |

## Module Unit Operations and Flows

Examples only; the full list is in `docs/platform/automation_catalog.md` in the North-Cytation repository.

| Unit operation | Inputs | Outputs / result |
|---|---|---|
| `get_pipet` | tip size (small or large) | Tip attached |
| `dispense_into_wellplate` | wells; volume per well (mL); liquid name | Liquid in the wells; tip still attached |
| `dispense_powder_mg` | target mass (mg); powder channel | Powder dispensed; returns the mass dispensed (mg) |
| `monitor_weight_over_time` | time (s) | Mass readings (g) over time; module unchanged |

| Flow | Inputs | Busy while running | Needs on hand |
|---|---|---|---|
| `dispense_from_vial_into_vial` | source vial; destination vial; volume (mL); liquid name | robot arm, clamp | a tip; enough liquid in the source vial |
| `measure_wellplate` | Gen5 protocol file; wells | track, Cytation | a plate on the deck |
| `mass_dispense_into_vial` | vial; target mass (mg); powder channel | robot arm, clamp, powder dispenser | powder loaded in that channel |

## Data Storage

| What | Where | What's recorded |
|---|---|---|
| Runs | `experiment_tracking/experiment_runs.csv` | Every run gets an ID and one row: workflow, start and end time, result, and where its config and data were saved. |
| Data | `output/` (one folder per run) | Measurements as CSV (Cytation reads, masses), plots as PNG, and the run's ID and config. |
| Logs and errors | `logs/` | A log file per run, plus an error record for each failed run. |
| Sample positions and volumes | `status/*.csv` (vial status files) | Each vial's position and volume. |
| Sample contents | `status/container_contents.csv` | What's in each vial and well (each material and its concentration), updated at every transfer. |
| Transfers | `status/transfers.csv`, with a copy per run under `output/sample_tracking/` | Every transfer. |

**Space used so far:** about 25 GB on the lab PC (about 17 GB of outputs and 5 GB of logs), mostly CSV data and PNG plots.

## Up-to-Date Code: where to look

| Standard | Status | Where to look |
|---|---|---|
| GitHub | Met | The [North-Cytation](https://github.com/AccelerationConsortium/North-Cytation) repo holds all of Lash-E's code. |
| Hide files | Met | `.gitignore` blocks the secrets file, run outputs (`output/`), logs and the live state files, so only code and settings are shared. |
| Readme | Met | `README.md` lists the hardware and which code controls each part, the main folders, and how to run without hardware. |
| Versions | Met | `environment.yml` and `requirements-lock.txt` were exported from the lab PC, so the exact versions can be installed on a new computer. |
| Simulation | Met | Every workflow runs with `SIMULATE = True`, which swaps the robot controller for a stand-in. `scheduler/fault_injection.py` makes that stand-in fail on purpose; for example, `NORTH_SIM_FAULT=C9_MOTOR_FAULT:3` gives a motor fault on the 3rd move. |
| Compartmentalization | Partly met | Workflows are in `workflows/` (new ones start from `workflow_template.py`). Automation code is in `North_Safe.py` and `master_usdl_coordinator.py`. Inventory is in `status/`, state is in `robot_state/robot_status.yaml`, and positions and settings are in the other `robot_state/*.yaml` files. Then `inputs/`, `output/`, `recommenders/` and `analysis/`. One position limit is still in the code rather than a YAML file. |
| Primitives, unit operations and flows | Partly met | `docs/platform/automation_catalog.md` sorts each method in `North_Safe.py` and `master_usdl_coordinator.py` into one of the three, and new workflows start from `workflow_template.py`, which uses flows. Four methods, such as `aspirate_from_vial`, still mix a task with other steps and analysis, and older workflows call unit operations directly. |
| Workflow tracking | Met | `experiment_tracking/experiment_run_logger.py` gives each run an ID and writes one row to `experiment_runs.csv`: the workflow, its times, its result and its output folder. |
| Configuration files | Met | `workflow_configs/` holds each workflow's settings. `save_run_info()` in `master_usdl_coordinator.py` copies them, with the run ID, into the run's output folder. |
| Sample tracking | Met | `experiment_tracking/sample_tracking.py` logs every transfer in `status/transfers.csv`, and `sample_contents.py` keeps what each container holds in `status/container_contents.csv`. Each run saves a copy under `output/sample_tracking/`. |
| Error tracking | Met | When a run fails, `experiment_tracking/error_records.py` writes a record to `logs/experiment_run_errors/`. The codes, and what to do for each, are listed in `error_codes.yaml`. |
| Safe stop | Met | `safe_stop()` in `master_usdl_coordinator.py` turns instruments off, parks the track and robot, drops the tip, returns vials home, and reports what it couldn't do. |
| Inputs and outputs | Not met yet | The closest is `dispense_from_vials_into_wellplate` in `North_Safe.py`, which checks the whole plan against the limits in `robot_state/wellplates.yaml` and refuses it before anything moves. |
