## Syncing OSCAL Content

#### Prerequisites

- Populate $trestle-workspace/
- Clone ComplianceAsCode/content locally 
- Install dependencies 

#### Procedure for testing

1. Run commands via trestle-bot CLI

**Commands**

**Transforming CaC content to an OSCAL Catalog**

**`sync-cac-content catalog`** command
```bash
poetry run trestlebot sync-cac-content catalog
--oscal-catalog cis_rhel8 --cac-policy-id cis_rhel8
--cac-content-roote ~/CaC/forked_content/content --repo-path ~/demos/tmp-trestle-demos
--committer-name hbraswelrh --committer-email test@redhat.com 
--branch main --dry-run
```

**Transforming CaC content to an OSCAL Profile**

**`sync-cac-content profile`** command
```bash
poetry run trestlebot sync-cac-content profile
--repo-path ~/demos/tmp-trestle-demos/ --product rhel8
--cac-content-root ~/CaC/forked_content/content --cac-policy-id cis_rhel8
--committer-name hbraswelrh --committer-email test@redhat.com --branch main 
--dry-run
```

**Transforming CaC content to an OSCAL Component Definition**

**`sync-cac-content component-definition`** command

- This command requires an update in the component-definition.json to test the results of the sync-oscal-content command. If changing a set of rules, there will be standard output print messages of the control files that were impacted. 
```bash
poetry run trestlebot sync-cac-content component-definition --repo-path ~/demos/tmp-trestle-demos
--cac-content-root ~/CaC/forked_content/content --cac-profile cis_server_l1
--oscal-profile cis_rhel9-l1_server --branch main --committer-name hbraswelrh
--committer-email test@redhat.com --component-definition-type software --product rhel8 --dry-run
```

**Transforming CaC content that has been updated based on changes to the `component-definition.json`**

**`sync-oscal-content component-definition`** command 

- This command requires an update in the component-definition.json to test the results of the sync-oscal-content command. If changing a set of rules, there will be standard output print messages of the control files that were impacted. 
- Updates made to the `component-definition.json` will be reflected in standard output as updates, but additionally as a comment in your `--cac-content-root` referenced repository. 
```bash
poetry run trestlebot sync-oscal-content component-definition --repo-path ~/demos/tmp-trestle-demos
--committer-email test@redhat.com --committer-name hbraswelrh --branch master
--cac-content-root ~/CaC/forked_content/content --product rhel8 --oscal-profile cis_rhel9-l1_server
--dry-run
```
2. While these commands are used to transform CaC/content to OSCAL Content, it is notable that updates to the OSCAL Content must be synced with the ComplianceAsCode repository. The contents are updated and will reflect the state of the OSCAL Component Definition. 
