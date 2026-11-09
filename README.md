# Cisco ACI APIC API — Student Lab

This introductory lab uses Python scripts to explore the Cisco APIC REST API and the relationship between a tenant and its application policies. The scripts operate on an **ACME** example tenant in an authorised APIC lab or simulator.

## Learning outcomes

By the end of the lab, you should be able to:

- Describe how an APIC REST request creates or reads an ACI object.
- Explain the roles of a tenant, VRF, bridge domain, application profile and endpoint group (EPG).
- Run Python scripts in a virtual environment and interpret their API responses.
- Use inventory output to check what the APIC actually contains.
- Distinguish between reading configuration and making changes to it.

## Before you start

You need Python 3, Git, the `requests` package and access to an APIC simulator or an authorised lab fabric. Obtain the APIC URL and your lab credentials from your tutor. **Do not put credentials in Git commits, screenshots or submitted work.**

In PowerShell:

```powershell
git clone https://github.com/w42ren/APIC-Student.git
cd APIC-Student
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install requests
```

If PowerShell blocks activation, use `\.venv\Scripts\python.exe` instead of `python` in the commands below. Keep `.venv` out of the repository.

Before running a script, open it and identify where it gets its APIC URL, username and password. Set these for your assigned lab as directed by your tutor. Check whether the script prompts for values or expects them in variables; the scripts may not all use the same method. Never commit a file containing a real password or session token.

If an HTTPS certificate warning or connection error appears, record the exact message and check the URL, network reachability and lab certificate instructions. A simulator may use a self-signed certificate; bypassing certificate verification is appropriate only when explicitly authorised for this lab, not as a general solution.

## Files and suggested order

| File | Use in this lab |
| --- | --- |
| `create_ACME_tenant.py` | Create or inspect the basic ACME tenant setup. |
| `create_ACME_all.py` | Explore the broader ACME configuration created by one script. Inspect its planned changes before running it. |
| `tenent_inventory.py` | Retrieve and record the tenant inventory. The filename is intentionally shown as supplied. |
| `list_ACME_epgs.py` | List the ACME EPGs and compare them with the intended design. |
| `delete_tenent.py` | Optional clean-up **only with tutor permission**; inspect which tenant or objects it deletes first. The filename is shown as supplied. |

These are the actual script filenames, including `tenent` in two names. Use the filenames exactly as they appear in the repository. The two creation scripts may overlap: inspect them and follow your tutor's assigned sequence rather than assuming both must be run.

## Activity 1 — Read the code

Open one creation script and one inventory script. For each, identify:

1. The APIC endpoint and HTTP method used.
2. How the script authenticates and sends requests.
3. Which ACI objects it expects to create or retrieve.
4. How it reports success or an API error.

Sketch the relevant hierarchy using the objects you actually find in the code. For example, an EPG belongs to an application profile inside a tenant, and its bridge domain association determines its network context. Do not assume that every object in this example is created by every script.

## Activity 2 — Create and verify

With your tutor's lab APIC and assigned credentials, run the creation script specified for your group. For example:

```powershell
python .\create_ACME_tenant.py
```

If instructed to use the broader configuration, inspect it first and then run:

```powershell
python .\create_ACME_all.py
```

Record the HTTP status and response or error. A successful HTTP response is useful evidence, but verify the resulting objects with an inventory query or the APIC interface.

## Activity 3 — Inventory and compare

```powershell
python .\tenent_inventory.py
python .\list_ACME_epgs.py
```

Compare the returned tenant objects and EPGs with the script you ran. Explain any missing objects, unexpected names or permission errors. If an inventory script expects the tenant to exist first, run it again after creation and compare the results.

## Activity 4 — Explain the policy

In a short paragraph or diagram, explain the path from tenant to application profile and EPG in this lab. If the selected script also creates a VRF, bridge domain, subnet or contract, describe its role and show evidence from the code or APIC response. An EPG is a policy grouping; a contract controls permitted communication between EPGs when one provides it and another consumes it.

## Evidence to submit

- The script or scripts you ran, with passwords and tokens removed from any extracts.
- The relevant HTTP status or error, plus inventory output showing the resulting objects.
- A small diagram or table of the ACI objects you observed and their relationships.
- A brief explanation of one issue you encountered, how you investigated it, and what you concluded.

Use only your assigned lab environment. The clean-up script can remove shared work, so run it only when the tutor has confirmed the target and authorised clean-up.
