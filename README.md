# ShopFloor Fix

**An AI maintenance assistant that helps small Michigan manufacturers get broken machines running again faster, and keeps their senior techs' know-how in the building when those techs retire.**

Built for the Michigan DevFest + AI Hackathon 2026 (November 13, 2026) with IBM watsonx Orchestrate. No-code build.

## The problem

When a machine breaks at a small manufacturer, production stops. Estimates put lost production for a small manufacturer at $1,000 to $3,000 per hour ([MRPeasy](https://www.mrpeasy.com/blog/production-downtime)), and more than half of U.S. manufacturers reported unplanned downtime in the past year ([Fluke study via SDCExec](https://www.sdcexec.com/sourcing-procurement/manufacturing/news/22953487/fluke-corporation-unplanned-downtime-costs-us-manufacturers-up-to-207m-study)).

The fix often lives in one senior tech's head, and those techs are retiring. U.S. manufacturing will need about 2.8 million workers by 2033 just to replace retirements ([Deloitte and The Manufacturing Institute](https://www2.deloitte.com/us/en/pages/about-deloitte/articles/press-releases/us-manufacturing-could-need-new-employees-by-2033.html)). Small Tier 2 and Tier 3 suppliers can't afford the sensor-based systems big automakers use.

## Who it's for

Jordan, a CNC operator at a small auto supplier in Sterling Heights, Michigan. Mill 3 just stopped, and Dave, the senior tech who knows the fix, is across the plant.

## What it does

An operator types the machine and the alarm code or symptom. ShopFloor Fix:

1. **Checks safety first.** No repair steps until the machine is locked out and tagged out. Anything unsafe goes to the maintenance lead.
2. **Finds the fix.** Searches the shop's own repair history first, then the machine's manual, and names its source.
3. **Warns about repeat problems.** Points out when the same machine keeps failing the same way and recommends a preventive check.
4. **Finds the right person.** Names the tech who fixed it before, checks their shift and writes a message to send them.
5. **Guides the repair.** Walks the tech through it one step at a time on request.
6. **Remembers what worked.** Writes a clean fix-log entry after each repair, so the next person gets that fix first.

It answers only from the shop's files, never guesses, and sends anything unsafe or unknown to a person.

## How it's built (IBM tools)

| Tool | What it does in ShopFloor Fix |
| --- | --- |
| IBM watsonx Orchestrate, Agent Builder | Hosts the agent and its instructions: safety rules, fix ranking, repeat warnings, guided repairs and fix capture |
| watsonx Orchestrate knowledge | Retrieval over the machine manuals, shop fix log and tech roster, so answers come only from these files |
| Model | The large language model provided by default in the hackathon's watsonx Orchestrate environment (GPT-OSS 120B). It understands each question and writes the answer from what the knowledge base returns. |

## What's in this repo

- `ARCHITECTURE.md`: diagrams of how the agent, knowledge and instructions fit together, and how one conversation flows
- `knowledge/01_Shop_Fix_Log.txt`: sample repair history (fictional)
- `knowledge/02_Tech_Roster.txt`: sample team and shifts (fictional)
- `agent/03_Agent_Instructions.txt`: the agent's full instructions
- `testing/04_Demo_Story_and_Test_Script.txt`: the demo story and test checks
- `screenshots/`: the agent setup and a working demo chat

### Machine manuals used (not included here; owned by their publishers)

- [Haas spindle drive troubleshooting guide](https://www.haascnc.com/service/troubleshooting-and-how-to/troubleshooting/spindle-drive---how-it-works-and-troubleshooting-guide.html)
- [Haas 30T/40T spindle motor troubleshooting guide](https://haascnc.com/service/troubleshooting-and-how-to/troubleshooting/30t-40t-spindle-motor---troubleshooting-guide---ngc.html)
- [Dake hand-operated hydraulic press manual](https://docs.travers.com/assets/pdf/87-112-002_manual.pdf) (Dake Corporation, Grand Haven, Michigan)
- [Teknor Apex injection molding troubleshooting guide](https://teknorapex.com/content/dam/teknorapex/en-us/pdf/processing-guides/Teknor_Color_Injection_Molding_Trouble_Shooting_Guide.pdf)

## Sample data notice

Great Lakes Fixture & Part Co., its technicians and its repair history are fictional, created for this demo. No personal or confidential information is used. The machine manuals are real public documents.

## What I didn't solve (yet)

- Messages to techs aren't sent automatically; the agent writes them for the operator to send.
- Fixes are written up in chat, not saved straight into a shared log.
- No live machine sensor data. It works from manuals and repair history only.

## What's next

With one more week: use IBM Bob to build Python tools for the same agent (`send_teams_message`, `save_fix_to_log` and `check_parts`) so it can message techs through Microsoft Teams, save fixes to a shared log, and check spare parts with reorders drafted to Michigan suppliers. Also add Spanish and Arabic support. See [ARCHITECTURE.md](ARCHITECTURE.md#next-week-tools-built-with-ibm-bob). Later, connect sensor data for early warnings.

## Why Michigan

Michigan's auto supply chain depends on small suppliers. ShopFloor Fix helps them keep machines running and contracts in-state, makes current workers more capable instead of replacing them, and turns real repairs into training for the next generation of skilled trades.
